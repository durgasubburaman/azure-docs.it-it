---
title: 'Creare certificati autofirmati per connessioni da punto a sito: PowerShell: Azure | Microsoft Docs'
description: Questo articolo contiene i passaggi per creare un certificato radice autofirmato, esportare la chiave pubblica e generare certificati client con PowerShell in Windows 10.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: cherylmc
ms.translationtype: Human Translation
ms.sourcegitcommit: 5e92b1b234e4ceea5e0dd5d09ab3203c4a86f633
ms.openlocfilehash: 1bfcb8683669770d6dd927cbde53a683bbc1d56e
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017


---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell"></a>Generare ed esportare i certificati per le connessioni da punto a sito usando PowerShell

Questo articolo mostra come creare un certificato radice autofirmato e generare i certificati client. Il presente articolo non contiene le istruzioni di configurazione da punto a sito o le domande frequenti relative alla configurazione da punto a sito. Tali informazioni sono reperibili selezionando dall'elenco uno dei seguenti articoli relativi alla configurazione da punto a sito:

> [!div class="op_single_selector"]
> * [Create self-signed certificates - PowerShell](vpn-gateway-certificates-point-to-site.md) (Creare certificati autofirmati - PowerShell)
> * [Create self-signed certificates - Makecert](vpn-gateway-certificates-point-to-site-makecert.md) (Creare certificati autofirmati - MakeCert)
> * [Configure Point-to-Site - Resource Manager - Azure portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md) (Eseguire una configurazione da punto a sito - Resource Manager - Portale di Azure)
> * [Configurazione da punto a sito - Gestione risorse - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Configure Point-to-Site - Classic - Azure portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md) (Eseguire una configurazione da punto a sito - Classica - Portale di Azure)
> 
> 

Le connessioni da punto a sito usano certificati per l'autenticazione. Quando si configura una connessione da punto a sito è necessario caricare la chiave pubblica (file con estensione .cer) di un certificato radice in Azure. I certificati client, inoltre, sono generati dal certificato radice e installati in ogni computer client che si connette alla VNet. Il certificato client permette al client di autenticarsi.


> [!NOTE]
> È necessario eseguire i passaggi descritti in questo articolo in un computer che esegue Windows 10. I cmdlet PowerShell necessari per generare i certificati fanno parte del sistema operativo Windows 10 e non funzionano in altre versioni di Windows. Questi cmdlet sono necessari solo per la generazione dei certificati. Dopo aver generato i certificati, è possibile installarli in qualsiasi sistema operativo client supportato. Se non si ha accesso a un computer con Windows 10, è possibile usare MakeCert per generare i certificati. I certificati generati con MakeCert, tuttavia, sono compatibili con le connessioni da punto a sito ma non con SHA-2. Per istruzioni su MakeCert, vedere [Create certificates using makecert](vpn-gateway-certificates-point-to-site-makecert.md) (Creare certificati mediante MakeCert). I certificati creati usando PowerShell o MakeCert possono essere installati in qualsiasi [sistema operativo client supportato](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq), non solo nel sistema operativo usato per crearli.
> 
>

## <a name="rootcert"></a>Creare un certificato radice autofirmato

La procedura seguente mostra come creare un certificato radice autofirmato usando PowerShell in Windows 10. I cmdlet e i parametri utilizzati in questi passaggi fanno parte del sistema operativo Windows 10 e non di una versione di PowerShell. Questo non significa che i certificati creati possono essere installati solo su Windows 10. Possono essere installati in qualsiasi client supportato. Per informazioni sui client supportati, vedere le [Domande frequenti sulla configurazione da punto a sito](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq).

1. Da un computer che esegue Windows 10 aprire una console di Windows PowerShell con privilegi elevati.
2. Usare l'esempio seguente per creare il certificato radice autofirmato. L'esempio seguente crea un certificato radice autofirmato denominato "P2SRootCert" che viene installato automaticamente in "Certificati-Utente corrente\Personale\Certificati". È possibile visualizzare il certificato aprendo *certmgr.msc* o *Gestire i certificati utente*.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>Esportare la chiave pubblica (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Il file exported.cer deve essere caricato in Azure. Per istruzioni, vedere [Configurare una connessione da punto a sito](vpn-gateway-howto-point-to-site-rm-ps.md#upload).

### <a name="export-the-self-signed-root-certificate-and-public-key-to-store-it-optional"></a>Esportare il certificato radice autofirmato e la chiave pubblica per archiviarli (facoltativo)

Si consiglia di esportare il certificato radice autofirmato e archiviarlo in un percorso sicuro. Se necessario, in seguito è possibile installarlo su un altro computer e generare altri certificati client oppure esportare un altro file.cer. Per esportare il certificato radice autofirmato come file .pfx, selezionare il certificato radice ed eseguire la stessa procedura descritta in [Esportazione di un certificato client](#clientexport).

## <a name="clientcert"></a>Generazione di un certificato client

Ogni computer client che si connette a una rete virtuale usando la soluzione Da punto a sito deve avere un certificato client installato. È possibile generare un certificato client da un certificato radice autofirmato, quindi esportare e installare il certificato client. Se il certificato client non è installato, l'autenticazione ha esito negativo. 

I passaggi seguenti illustrano come generare un certificato client da un certificato radice autofirmato. È possibile generare più certificati client dallo stesso certificato radice. Quando si generano certificati client con la procedura seguente, il certificato client viene installato automaticamente nel computer che è stato usato per generare il certificato. Se si vuole installare un certificato client in un altro computer client, è possibile esportare il certificato.

Per generare certificati client tramite la seguente procedura con PowerShell, è richiesto Windows 10. I cmdlet e i parametri utilizzati in questi passaggi fanno parte del sistema operativo Windows 10 e non di una versione di PowerShell. Questo non significa che i certificati creati possono essere installati solo su Windows 10. Per informazioni sui client supportati, vedere le [Domande frequenti sulla configurazione da punto a sito](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq).

### <a name="example-1"></a>Esempio 1

Questo esempio usa la variabile dichiarata "$cert" della sezione precedente. Se è stata chiusa la console di PowerShell dopo aver creato il certificato radice autofirmato o si stanno creando i certificati client aggiuntivi in una nuova sessione della console di PowerShell, attenersi alla procedura nell'[esempio 2](#ex2).

Modificare ed eseguire l'esempio per generare un certificato client. Se si esegue l'esempio seguente senza modificarlo, il risultato è un certificato client denominato "P2SChildCert".  Se si desidera assegnare un nome diverso al certificato figlio, modificare il valore CN. Non modificare il TextExtension quando si esegue questo esempio. Il certificato client generato viene installato automaticamente in "Certificati-Utente corrente\Personale\Certificati" nel computer in uso.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>Esempio 2

Se si creano certificati client aggiuntivi o non si usa la stessa sessione di PowerShell utilizzata per creare il certificato radice autofirmato, usare la procedura seguente:

1. Identificare il certificato radice autofirmato che viene installato nel computer. Questo cmdlet restituisce un elenco dei certificati installati nel computer in uso.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. Individuare il nome dell'oggetto nell'elenco restituito e quindi copiare in un file di testo l'identificazione personale che si trova accanto a esso. Nell'esempio seguente ci sono due certificati. Il nome CN è il nome del certificato radice autofirmato da cui si desidera generare un certificato figlio. In questo caso "P2SRootCert".

        Thumbprint                                Subject

        AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
        7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert


3. Dichiarare una variabile per il certificato radice usando l'identificazione personale del passaggio precedente. Sostituire THUMBPRINT con l'identificazione personale del certificato radice autofirmato da cui si desidera generare un certificato figlio.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  Ad esempio, usando l'identificazione personale per P2SRootCert nel passaggio precedente, la variabile è simile alla seguente:

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```    

4.  Modificare ed eseguire l'esempio per generare un certificato client. Se si esegue l'esempio seguente senza modificarlo, il risultato è un certificato client denominato "P2SChildCert". Se si desidera assegnare un nome diverso al certificato figlio, modificare il valore CN. Non modificare il TextExtension quando si esegue questo esempio. Il certificato client generato viene installato automaticamente in "Certificati-Utente corrente\Personale\Certificati" nel computer in uso.

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>Esportare un certificato client   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]
    

## <a name="install"></a>Installare un certificato client esportato

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Passaggi successivi

Continuare con la configurazione da punto a sito. 

* Per i passaggi del modello di distribuzione di **Resource Manager**, vedere l'articolo relativo a come [configurare una connessione da punto a sito a una rete VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md). 
* Per i passaggi del modello di distribuzione **classico**, vedere [Configurare una connessione VPN da punto a sito a una rete virtuale (classico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
