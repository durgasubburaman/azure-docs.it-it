---
title: Come registrare le origini dati | Documentazione Microsoft
description: Articolo sulle procedure che illustra come registrare origini dati in Azure Data Catalog, inclusi i campi di metadati estratti durante la registrazione.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 05/15/2017
ms.author: maroche
ms.translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: 25c2b279487f099a0e688621e63faaa4ed265e6e
ms.contentlocale: it-it
ms.lasthandoff: 11/17/2016


---
# <a name="how-to-register-data-sources"></a>Come registrare le origini dati
## <a name="introduction"></a>Introduzione
**Catalogo dati di Microsoft Azure** è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per origini dati aziendali. In altre parole, il **Catalogo dati di Azure** consente agli utenti di individuare, comprendere e usare origini dati e aiuta le organizzazioni a ottenere maggior valore dai dati esistenti. Il primo passaggio per rendere individuabile un'origine dati nel **Catalogo dati di Azure** consiste nel registrare l'origine dati.

## <a name="registering-data-sources"></a>Registrazione delle origini dati
La registrazione è il processo di estrazione dei metadati da un'origine dati e di copia dei dati nel servizio **Catalogo dati di Azure** . I dati rimangono nella posizione in cui risiedono attualmente e sotto il controllo degli amministratori e dei criteri del sistema corrente.

Per registrare un'origine dati, avviare semplicemente lo strumento di registrazione dell'origine dati di **Azure Data Catalog** dal portale **Azure Data Catalog**. Accedere con l'account aziendale o dell'istituto di istruzione (le stesse credenziali di Azure Active Directory usate per accedere al portale) e quindi selezionare l'origine dati che si vuole registrare.
Per altre informazioni dettagliate, vedere [Introduzione al Catalogo dati di Azure](data-catalog-get-started.md) .

Dopo la registrazione dell'origine dati, il catalogo tiene traccia del percorso e indicizza i metadati, in modo che gli utenti possano cercare, sfogliare e individuare l'origine dati e quindi usare il relativo percorso a cui connettersi con l'applicazione o lo strumento preferito.

## <a name="sources-supported"></a>Origini supportate
Per un elenco delle origini dati attualmente supportate, vedere [Origini dati supportate da Catalogo dati di Azure](data-catalog-dsr.md) .
<br/>

## <a name="structural-metadata"></a>Metadati strutturali
Quando si registra un'origine dati, lo strumento di registrazione estrae le informazioni sulla struttura degli oggetti selezionati, dette metadati strutturali.

Per tutti gli oggetti, questi metadati strutturali includeranno la posizione dell'oggetto, in modo che gli utenti che individuano i dati possano utilizzare tali informazioni per connettersi all'oggetto negli strumenti client di propria scelta. Altri metadati strutturali includono il tipo e il nome dell'oggetto e il nome di colonna/attributo e il tipo di dati.

## <a name="descriptive-metadata"></a>Metadati descrittivi
Oltre ai metadati strutturali di base estratti dall'origine dati, lo strumento di registrazione dell'origine dati estrae anche metadati descrittivi. Per SQL Server Analysis Services e SQL Server Reporting Services questi dati vengono estratti dalle proprietà Description esposte da questi servizi. Per SQL Server vengono estratti i valori specificati con la proprietà estesa ms_description. Per il database Oracle lo strumento di registrazione dell'origine dati estrae la colonna COMMENTS dalla vista ALL_TAB_COMMENTS.

Oltre ai metadati descrittivi estratti dall'origine dati, gli utenti possono anche immettere metadati descrittivi con lo strumento di registrazione dell'origine dati. Gli utenti possono aggiungere tag e identificare esperti per gli oggetti in fase di registrazione. Tutti questi metadati descrittivi vengono copiati nel servizio **Catalogo dati di Azure** insieme ai metadati strutturali.

## <a name="including-previews"></a>Inclusione delle anteprime
Per impostazione predefinita, solo i metadati vengono estratti dalle origini dati e copiati nel servizio **Catalogo dati di Azure** , ma un'origine dati spesso è più facile da comprendere osservando un esempio dei dati che contiene.

Lo strumento di registrazione dell'origine dati del **Catalogo dati di Azure** consente agli utenti di includere un'anteprima dei dati in ogni tabella sotto forma di snapshot e una vista registrata. Se l'utente sceglie di includere anteprime durante la registrazione, lo strumento di registrazione includerà un massimo di 20 record da ogni tabella e vista. Questo snapshot viene quindi copiato nel catalogo insieme ai metadati strutturali e descrittivi.

> [!NOTE]
> Nell'anteprima delle tabelle di grandi dimensioni con un numero elevato di colonne potrebbero essere inclusi meno di 20 record.
>
>

## <a name="including-data-profiles"></a>Includere profili dati
Esattamente come l’inclusione delle anteprime può offrire un contesto utile per la ricerca di origini dati nel **Catalogo dati di Azure**da parte degli utenti, anche l’inclusione di un profilo dati può semplificare la comprensione delle origini dati individuate.

Lo strumento di registrazione dell'origine dati del **Catalogo dati di Azure** consente agli utenti di includere un profilo dati in ogni tabella e vista registrate. Se l'utente sceglie di includere un profilo dati durante la registrazione, lo strumento di registrazione includerà statistiche aggregate sui dati in ogni tabella o vista, tra cui:

* Il numero di righe e le dimensioni dei dati nell'oggetto
* La data dell'aggiornamento più recente dei dati e lo schema dell'oggetto
* Il numero di record null e i valori distinti per colonne
* I valori minimo, massimo, medio e deviazione standard per le colonne

Queste statistiche vengono quindi copiate nel catalogo insieme ai metadati strutturali e descrittivi.

> [!NOTE]
> Le colonne del testo e della data non includeranno le statistiche della media o della deviazione standard nel profilo dati.
>
>

## <a name="updating-registrations"></a>Aggiornamento delle registrazioni
La registrazione di un'origine dati la renderà individuabile nel **Catalogo dati di Azure** usando i metadati e l'anteprima facoltativa estratti durante la registrazione. Se l'origine dati deve essere aggiornata nel Catalogo (ad esempio, se lo schema di un oggetto è stato modificato o le tabelle escluse in origine devono essere incluse oppure un utente vuole aggiornare i dati inclusi nelle anteprime), è possibile eseguire di nuovo lo strumento di registrazione dell'origine dati.

La nuova registrazione di un'origine dati già registrata esegue un'operazione di unione "upsert": gli oggetti esistenti vengono aggiornati, mentre i nuovi oggetti vengono creati. Tutti i metadati forniti dagli utenti tramite il portale del **Catalogo dati di Azure** verranno mantenuti.

## <a name="summary"></a>Riepilogo
La registrazione di un'origine dati con il **Catalogo dati di Azure** rende più semplice individuare e comprendere l'origine dati, copiando i metadati strutturali e descrittivi dall'origine dati nel servizio Catalogo. Dopo la registrazione di un'origine dati, questa potrà essere annotata, gestita e individuata tramite il portale del **Catalogo dati di Azure** .

## <a name="see-also"></a>Vedere anche
* [Introduzione al Catalogo dati di Azure](data-catalog-get-started.md) .

