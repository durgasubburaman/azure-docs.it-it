---
title: Guida introduttiva a Storage Explorer (anteprima) | Microsoft Docs
description: Gestire le risorsa di archiviazione di Azure con Storage Explorer (anteprima)
services: storage
documentationcenter: na
author: TomArcher
manager: douge
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: tarcher
ms.translationtype: Human Translation
ms.sourcegitcommit: a3ca1527eee068e952f81f6629d7160803b3f45a
ms.openlocfilehash: fbcd35529c5d2360f5b0c9de4d3c9c4a08a0cc8f
ms.contentlocale: it-it
ms.lasthandoff: 04/27/2017


---
# <a name="get-started-with-storage-explorer-preview"></a>Guida introduttiva a Storage Explorer (anteprima)
## <a name="overview"></a>Panoramica
Azure Storage Explorer (anteprima) è un'app autonoma che consente di usare facilmente dati di Archiviazione di Azure in Windows, macOS e Linux. Questo articolo illustra diversi modi per connettersi agli account di archiviazione di Azure e per gestirli.

![Microsoft Azure Storage Explorer (anteprima)][15]

## <a name="prerequisites"></a>Prerequisiti
* [Scaricare e installare Storage Explorer (anteprima)](http://www.storageexplorer.com)

## <a name="connect-to-a-storage-account-or-service"></a>Connettersi a un account o a un servizio di archiviazione
Storage Explorer (anteprima) offre numerosi modi per connettersi agli account di archiviazione. Ad esempio, è possibile:
* Connettersi agli account di archiviazione associati alle sottoscrizioni di Azure.
* Connettersi agli account e ai servizi di archiviazione condivisi da altre sottoscrizioni di Azure.
* Connettersi alla risorsa di archiviazione locale e gestirla usando l'emulatore di archiviazione di Azure. 

Inoltre, è possibile usare gli account di archiviazione in Azure globale e nazionale:

* [Connettersi a una sottoscrizione di Azure](#connect-to-an-azure-subscription): gestire le risorse di archiviazione appartenenti alla sottoscrizione di Azure.
* [Usare la risorsa di archiviazione locale](#work-with-local-development-storage): gestire la risorsa di archiviazione locale usando l'emulatore di archiviazione di Azure.
* [Collegarsi a una risorsa di archiviazione esterna](#attach-or-detach-an-external-storage-account): gestire le risorse di archiviazione appartenenti a un'altra sottoscrizione di Azure o ai cloud di Azure nazionale usando il nome, la chiave e gli endpoint dell'account di archiviazione.
* [Collegare un account di archiviazione usando la firma di accesso condiviso](#attach-storage-account-using-sas): gestire le risorse di archiviazione appartenenti a un'altra sottoscrizione di Azure usando una firma di accesso condiviso.
* [Collegare un servizio usando la firma di accesso condiviso](#attach-service-using-sas): gestire un servizio di archiviazione specifico (contenitore BLOB, coda o tabella) appartenente a un'altra sottoscrizione di Azure usando una firma di accesso condiviso.

## <a name="connect-to-an-azure-subscription"></a>Connettersi a una sottoscrizione di Azure.
> [!NOTE]
> Se non si ha un account Azure, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi della sottoscrizione di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
>
>

1. In Storage Explorer (anteprima), selezionare **Azure Account settings**(Impostazioni account Azure).

    ![Azure Account settings][0]

2. Il riquadro sinistro visualizza tutti gli account Microsoft a cui si è connessi. Per connettersi a un altro account, selezionare **Aggiungi un account** e seguire le istruzioni per accedere con un account Microsoft associato ad almeno una sottoscrizione di Azure attiva.

    >[!NOTE]
    >La connessione ad Azure nazionale, ad esempio Azure Germania, Azure per enti pubblici e Azure Cina tramite accesso, non è attualmente supportata. Vedere la sezione "Collegare o scollegare un account di archiviazione esterno" per la modalità di connessione agli account di archiviazione di Azure nazionale.

3. Dopo aver effettuato l'accesso con un account Microsoft, il riquadro sinistro viene popolato con le sottoscrizioni di Azure associate a tale account. Selezionare le sottoscrizioni di Azure da usare e quindi selezionare **Applica**. Selezionando **Tutte le sottoscrizioni** , viene alternata la selezione di tutte o di nessuna delle sottoscrizioni di Azure elencate.

    ![Selezionare le sottoscrizioni di Azure][3]  
    Il riquadro sinistro mostra gli account di archiviazione associati alle sottoscrizioni di Azure selezionate.

    ![Sottoscrizioni di Azure selezionate][4]

## <a name="connect-to-an-azure-stack-subscription"></a>Connettersi a una sottoscrizione di Azure Stack

È necessaria una connessione VPN per consentire a Storage Explorer di accedere alla sottoscrizione di Azure Stack in remoto. Per informazioni su come configurare una connessione VPN ad Azure Stack, vedere [Connettersi ad Azure Stack con VPN](azure-stack/azure-stack-connect-azure-stack.md#connect-with-vpn).

Per il modello di verifica di Azure Stack è necessario esportare il certificato radice dell'autorità di Azure Stack. A tale scopo, procedere come segue:

1. Aprire `mmc.exe` in MAS-CON01, in un computer host Azure Stack o in un computer locale con connessione VPN ad Azure Stack. 

2. In **File** selezionare **Aggiungi/Rimuovi snap-in**, aggiungere **Certificati** per gestire **Account del computer** di **Computer locale**.

    ![Caricare il certificato radice di Azure Stack tramite mmc.exe][25]   

3. Trovare **AzureStackCertificationAuthority** in **Radice console\Certificati - Computer locale\Autorità di certificazione radice attendibili\Certificati**. 

4. Fare clic con il pulsante destro del mouse sull'elemento, scegliere **Tutte le attività** > **Esporta** e quindi seguire le istruzioni per esportare il certificato con **Codificato Base 64 X.509 (.CER)**.  

    Il certificato esportato verrà usato nel passaggio successivo.   

    ![Esportare il certificato radice dell'autorità di Azure Stack radice][26]   

5. In Storage Explorer (anteprima) scegliere **Certificati SSL** dal menu **Modifica**, quindi selezionare **Importa certificati**. Usare la finestra di dialogo selezione file per trovare e aprire il certificato esportato nel passaggio precedente.  

    Dopo l'importazione verrà chiesto di riavviare Storage Explorer.

    ![Importare il certificato in Storage Explorer (anteprima)][27]

6. Dopo il riavvio di Storage Explorer (anteprima), selezionare il menu **Modifica** e verificare che **Target Azure Stack** (Azure Stack di destinazione) sia selezionato. In caso contrario, selezionarlo e riavviare Storage Explorer per applicare la modifica. Questa configurazione è obbligatoria per la compatibilità con l'ambiente di Azure Stack.

    ![Verificare che Target Azure Stack (Azure Stack di destinazione) sia selezionato][28]

7. Nel riquadro sinistro selezionare **Manage Accounts** (Gestisci account).  
    Verranno visualizzati tutti gli account Microsoft a cui si è connessi.

8. Per connettersi all'account Azure Stack, selezionare **Aggiungi un account**.

    ![Aggiungere un account Azure Stack][29]

9. Nella finestra di dialogo **Add new account** (Aggiungi nuovo account), selezionare **Create Custom Environment** (Crea ambiente personalizzato) in **Azure environment** (Ambiente Azure) e quindi fare clic su **Next** (Avanti).

10. Immettere tutte le informazioni necessarie sull'ambiente personalizzato di Azure Stack, quindi fare clic su **Sign in** (Accedi). 

11. Per accedere con l'account Azure Stack associato ad almeno una sottoscrizione di Azure Stack attiva, compilare la finestra di dialogo **Sign in to a Custom Cloud environment** (Accedi a un ambiente cloud personalizzato).  

    I dati per ogni campo sono i seguenti:

    * **Environment name** (Nome ambiente): il campo può essere personalizzato dall'utente.
    * **Authority** (Autorità): il valore deve essere https://login.windows.net. Per Azure Cina usare https://login.chinacloudapi.cn.
    * **Sign in resource id** (ID risorsa di accesso): recuperare il valore eseguendo uno degli script di PowerShell seguenti:

        Se si è un amministratore cloud:

        ```powershell
        PowerShell (Invoke-RestMethod -Uri https://adminmanagement.local.azurestack.external/metadata/endpoints?api-version=1.0 -Method Get).authentication.audiences[0]
        ```

        Se si è un tenant:

        ```powershell
        PowerShell (Invoke-RestMethod -Uri https://management.local.azurestack.external/metadata/endpoints?api-version=1.0 -Method Get).authentication.audiences[0]
        ```

    * **Graph endpoint** (Endpoint di Graph): il valore deve essere https://graph.windows.net. Per Azure Cina usare https://graph.chinacloudapi.cn.
    * **ARM resource id** (ID risorsa di Azure Resource Manager): usare lo stesso valore di **Sign in resource id** (ID risorsa di accesso).
    * **ARM resource endpoint** (Endpoint risorse di Azure Resource Manager): esempi di endpoint di risorse di Azure Resource Manager:

        * Per gli amministratori cloud: https://adminmanagement.local.azurestack.external   
        * Per i tenant: https://management.local.azurestack.external
 
    * **Tenant Ids** (ID tenant): facoltativo. Il valore viene indicato solo quando deve essere specificata la directory.

12. Dopo avere effettuato l'acceso con un account Azure Stack, il riquadro sinistro verrà popolato con le sottoscrizioni di Azure Stack associate a quell'account. Selezionare le sottoscrizioni di Azure Stack da usare e quindi selezionare **Applica**. Selezionando o deselezionando la casella di controllo **Tutte le sottoscrizioni**, sarà possibile selezionare o deselezionare tutte le sottoscrizioni di Azure Stack elencate.

    ![Selezionare le sottoscrizioni di Azure Stack dopo avere compilato la finestra di dialogo Custom Cloud Environment (Ambiente cloud personalizzato)][30]  
    Il riquadro sinistro mostra gli account di archiviazione associati alle sottoscrizioni di Azure Stack selezionate.

    ![Elenco di account di archiviazione, inclusi gli account delle sottoscrizioni di Azure Stack][31]

## <a name="work-with-local-development-storage"></a>Utilizzare la risorsa di archiviazione locale
Storage Explorer (anteprima) consente di lavorare con la risorsa di archiviazione locale usando l'emulatore di archiviazione di Azure che consente di scrivere codice per la risorsa di archiviazione e di testarla senza necessariamente avere un account di archiviazione distribuito in Azure, perché l'account di archiviazione viene emulato dall'emulatore di archiviazione di Azure.

> [!NOTE]
> Emulatore di archiviazione di Azure è attualmente supportato solo per Windows.
>
>

1. Nel riquadro sinistro di Storage Explorer (anteprima) espandere il nodo **(Local and Attached) (Locale e collegato)** > **Storage Accounts (Account di archiviazione)** > **(Development) (Sviluppo)**.

    ![Nodo di sviluppo locale][21]

2. Se Emulatore di archiviazione di Azure non è ancora stato installato, verrà richiesto di farlo tramite una barra informazioni. Se la barra informazioni è visualizzata, selezionare **Scarica la versione più recente** e installare l'emulatore.

    ![Richiesta di download dell'Emulatore di archiviazione di Azure][22]

3. Dopo aver installato l'emulatore è possibile creare e usare BLOB, code e tabelle locali. Per informazioni su come usare i vari tipi di account di archiviazione, vedere uno degli argomenti seguenti:

    * [Gestire le risorse dell'archivio BLOB di Azure](vs-azure-tools-storage-explorer-blobs.md)
    * Manage Azure file share storage resources (Gestire risorse di condivisione file di Azure): *presto disponibile*
    * Manage Azure queue storage resources (Gestire risorse di archiviazione code di Azure): *presto disponibile*
    * Manage Azure table storage resources (Gestire risorse di archiviazione tabelle di Azure): *presto disponibile*

## <a name="attach-or-detach-an-external-storage-account"></a>Collegare o scollegare un account di archiviazione esterno
Storage Explorer (anteprima) consente di collegarsi agli account di archiviazione esterni per poter condividere facilmente gli account di archiviazione. Questa sezione illustra come collegarsi (e scollegarsi) agli account di archiviazione esterni.

### <a name="get-the-storage-account-credentials"></a>Ottenere le credenziali dell'account di archiviazione
Per condividere un account di archiviazione esterno, il proprietario di tale account deve prima ottenere le credenziali, ovvero il nome e la chiave dell'account, e quindi condividere tali informazioni con la persona che vuole collegarsi a tale account esterno. Per ottenere le credenziali dell'account di archiviazione nel portale di Azure, è possibile seguire questa procedura:

1. Accedere al [portale di Azure](https://portal.azure.com).

2. Selezionare **Esplora**.

3. Selezionare **Account di archiviazione**.

4. Nel pannello **Account di archiviazione** selezionare l'account di archiviazione desiderato.

5. Nel pannello **Impostazioni** per l'account di archiviazione selezionare **Chiavi di accesso**.

    ![Opzione Chiavi di accesso][5]

6. Nel pannello **Chiavi di accesso** copiare i valori di **Nome account di archiviazione** e **key1** da usare quando ci si collega all'account di archiviazione.

    ![Chiavi di accesso][6]

### <a name="attach-to-an-external-storage-account"></a>Collegarsi a un account di archiviazione esterno
Per il collegamento a un account di archiviazione esterno è necessario avere la chiave e il nome dell'account. La sezione "Ottenere le credenziali dell'account di archiviazione" spiega come ottenere questi valori dal portale di Azure. Nel portale, la chiave dell'account è tuttavia denominata **key1**. Quando Storage Explorer (anteprima) chiede la chiave dell'account, immettere quindi il valore di **key1**.

1. In Storage Explorer (anteprima), selezionare **Connect to Azure storage**(Connetti ad Archiviazione di Azure).

    ![Opzione Connect to Azure storage (Connetti ad Archiviazione di Azure)][23]

2. Nella finestra di dialogo **Connetti ad Archiviazione di Azure** specificare la chiave dell'account, ovvero il valore di **key1** ottenuto dal portale di Azure, e quindi selezionare **Avanti**.

    > [!NOTE]
    > È possibile immettere la stringa di connessione di archiviazione di un account di archiviazione in Azure nazionale. Per connettersi ad esempio ad account di archiviazione di Azure Germania, immettere stringhe di connessione simile alle seguenti: 
    >
    >* DefaultEndpointsProtocol=https
    >* AccountName=cawatest03
    >* AccountKey=<storage_account_key>
    >* EndpointSuffix=core.cloudapi.de
    
    >È possibile ottenere la stringa di connessione dal portale di Azure come descritto nella sezione "Ottenere le credenziali dell'account di archiviazione".

    ![Finestra di dialogo Connetti ad Archiviazione di Azure][24]

3. Nella finestra di dialogo **Associa archiviazione esterna** immettere il nome dell'account di archiviazione nella casella **Nome account**, specificare eventuali altre impostazioni e quindi selezionare **Avanti**.

    ![Finestra di dialogo Associa archiviazione esterna][8]

4. Nella finestra di dialogo **Riepilogo connessione** verificare le informazioni. Per apportare modifiche, selezionare **Indietro** e immettere nuovamente le impostazioni. 

5. Selezionare **Connessione**.

6. Dopo la connessione, l'account di archiviazione esterno viene visualizzato con il testo **(Esterno)** aggiunto al nome dell'account di archiviazione.

    ![Risultato della connessione a un account di archiviazione esterno][9]

### <a name="detach-from-an-external-storage-account"></a>Scollegarsi da un account di archiviazione esterno
1. Fare clic con il pulsante destro del mouse sull'account di archiviazione esterno che si vuole scollegare e quindi scegliere **Scollega**.

    ![Opzione per scollegarsi da un account di archiviazione][10]

2. Nella finestra di dialogo del messaggio di conferma, selezionare **Sì** per confermare che si vuole scollegare l'account di archiviazione esterno.

## <a name="attach-a-storage-account-by-using-an-sas"></a>Collegare un account di archiviazione usando la firma di accesso condiviso
Una [firma di accesso condiviso](storage/storage-dotnet-shared-access-signature-part-1.md) consente all'amministratore di una sottoscrizione di Azure di concedere temporaneamente l'accesso a un account di archiviazione senza dover fornire le credenziali della sottoscrizione di Azure.

Per illustrare questo scenario, si supponga che l'utente A sia l'amministratore di una sottoscrizione di Azure e che voglia consentire all'utente B di accedere a un account di archiviazione per un periodo limitato con determinate autorizzazioni:

1. L'utente A genera una firma di accesso condiviso, costituita dalla stringa di connessione per l'account di archiviazione, per un periodo di tempo specifico e con le autorizzazioni desiderate.

2. L'utente A condivide la firma di accesso condiviso con la persona che vuole accedere all'account di archiviazione, ovvero l'utente B.  

3. L'utente B usa Storage Explorer (anteprima) per collegarsi all'account appartenente all'utente A usando la firma di accesso condiviso fornita.

### <a name="get-an-sas-for-the-account-you-want-to-share"></a>Ottenere una firma di accesso condiviso per l'account che si vuole condividere
1. In Storage Explorer (anteprima) fare clic con il pulsante destro del mouse sull'account di archiviazione che si vuole condividere e quindi scegliere **Get Shared Access Signature** (Ottieni firma di accesso condiviso).

    ![Menu di scelta rapida Get SAS (Ottieni firma di accesso condiviso)][13]

2. Nella finestra di dialogo **Shared Access Signature** (Firma di accesso condiviso) specificare il periodo di tempo e le autorizzazioni per l'account e quindi selezionare **Create** (Crea).

    ![Finestra di dialogo Get SAS][14] (Ottieni firma di accesso condiviso)  
    La finestra di dialogo **Firma di accesso condiviso** visualizza la firma di accesso condiviso.

3. Selezionare **Copia** accanto a **Stringa di connessione** per copiare la stringa negli Appunti e quindi selezionare **Chiudi**.

### <a name="attach-to-the-shared-account-by-using-the-sas"></a>Collegarsi all'account condiviso usando la firma di accesso condiviso
1. In Storage Explorer (anteprima), selezionare **Connect to Azure storage**(Connetti ad Archiviazione di Azure).

    ![Opzione Connect to Azure storage (Connetti ad Archiviazione di Azure)][23]

2. Nella finestra di dialogo **Connetti ad Archiviazione di Azure** specificare la stringa di connessione e quindi selezionare **Avanti**.

    ![Finestra di dialogo Connetti ad Archiviazione di Azure][24]

3. Nella finestra di dialogo **Riepilogo connessione** verificare le informazioni. Per apportare modifiche, selezionare **Indietro** e immettere le impostazioni desiderate. 

4. Selezionare **Connessione**.

5. Una volta collegato, l'account di archiviazione verrà visualizzato con il testo **(SAS)** (Firma di accesso condiviso) aggiunto al nome dell'account specificato.

    ![Risultato del collegamento a un account con firma di accesso condiviso][17]

## <a name="attach-a-service-by-using-an-sas"></a>Collegare un servizio usando la firma di accesso condiviso
La sezione "Collegare un account di archiviazione usando la firma di accesso condiviso" illustra come l'amministratore di una sottoscrizione di Azure possa concedere l'accesso temporaneo a un account di archiviazione generando e condividendo una firma di accesso condiviso per l'account di archiviazione. È allo stesso modo possibile generare una firma di accesso condiviso per un servizio specifico, ovvero contenitore BLOB, coda o tabella, in un account di archiviazione.  

### <a name="generate-an-sas-for-the-service-that-you-want-to-share"></a>Generare una firma di accesso condiviso per il servizio che si vuole condividere
In questo contesto, un servizio può essere un contenitore BLOB, una coda o una tabella. Per generare la firma di accesso condiviso per un servizio elencato, vedere:

* [Ottenere la firma di accesso condiviso per un contenitore BLOB](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* Get the SAS for a file share (Ottenere la firma di accesso condiviso per una condivisione file): *presto disponibile*
* Get the SAS for a queue (Ottenere la firma di accesso condiviso per una coda): *presto disponibile*
* Get the SAS for a table (Ottenere la firma di accesso condiviso per una tabella): *presto disponibile*

### <a name="attach-to-the-shared-account-service-by-using-the-sas"></a>Collegarsi al servizio account condiviso usando la firma di accesso condiviso
1. In Storage Explorer (anteprima), selezionare **Connect to Azure storage**(Connetti ad Archiviazione di Azure).

    ![Opzione Connect to Azure storage (Connetti ad Archiviazione di Azure)][23]

2. Nella finestra di dialogo **Connetti ad Archiviazione di Azure** specificare l'URI della firma di accesso condiviso e quindi selezionare **Avanti**.

    ![Finestra di dialogo Connetti ad Archiviazione di Azure][24]

3. Nella finestra di dialogo **Riepilogo connessione** verificare le informazioni. Per apportare modifiche, selezionare **Indietro** e immettere le impostazioni desiderate. 

4. Selezionare **Connessione**.

5. Una volta collegato, il nuovo servizio collegato verrà visualizzato nel nodo **(Service SAS)** (Firma di accesso condiviso servizio).

    ![Risultato della connessione a un servizio condiviso usando una firma di accesso condiviso][20]

## <a name="search-for-storage-accounts"></a>Cercare gli account di archiviazione
Se l'elenco di account di archiviazione è lungo, è possibile trovare rapidamente un determinato account di archiviazione usando la casella di ricerca nella parte superiore del riquadro sinistro.

Mentre si digita nella casella di ricerca, il riquadro sinistro mostra gli account di archiviazione che corrispondono al valore di ricerca immesso fino a quel momento. La ricerca di tutti gli account di archiviazione il cui nome contiene **tarcher** è ad esempio illustrata nello screenshot seguente:

![Ricerca dell'account di archiviazione][11]

## <a name="next-steps"></a>Passaggi successivi
* [Gestire le risorse dell'archivio BLOB di Azure con Storage Explorer (anteprima)](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png

