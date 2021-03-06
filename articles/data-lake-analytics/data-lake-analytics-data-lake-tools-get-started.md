---
title: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio | Microsoft Docs
description: 'Informazioni su come installare Strumenti di Data Lake per Visual Studio e come sviluppare e testare script U-SQL. '
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/06/2017
ms.author: edmaca, yanacai
ms.translationtype: Human Translation
ms.sourcegitcommit: 5edc47e03ca9319ba2e3285600703d759963e1f3
ms.openlocfilehash: 9be337c3e04959a1ad2152c989c8532383362521
ms.contentlocale: it-it
ms.lasthandoff: 05/31/2017


---
# <a name="tutorial-develop-u-sql-scripts-using-data-lake-tools-for-visual-studio"></a>Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Scrivere e testare script U-SQL con Data Lake Tools per Visual Studio.

U-SQL è un linguaggio estremamente scalabile e facilmente estendibile per la preparazione, la trasformazione e l'analisi di tutti i dati presenti nel data lake e non solo. Per altre informazioni, vedere la pagina di [riferimento su U-SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).

## <a name="prerequisites"></a>Prerequisiti
* **Visual Studio 2017, in carico di elaborazione e archiviazione dati, aggiornamento 3 di Visual Studio 2015, aggiornamento 4 di Visual Studio 2013 o Visual Studio 2012. Sono supportate le edizioni Enterprise (Ultimate/Premium), Professional e Community. L'edizione Express non è supportata.**
* **Microsoft Azure SDK per .NET versione 2.7.1 o successiva**.  Installarlo usando il [programma di installazione della piattaforma Web](http://www.microsoft.com/web/downloads/platform.aspx).
* **[Data Lake Tools per Visual Studio](http://aka.ms/adltoolsvs)**.

    Una volta installato Strumenti di Data Lake per Visual Studio, verrà visualizzato un nodo "Data Lake Analytics" in Esplora server sotto il nodo "Azure". Per aprire Esplora server, premere CTRL+ALT+S.

* **Dati di esempio e account di Data Lake Analytics** Gli strumenti di Data Lake non supportano la creazione degli account Data Lake Analytics. Creare un account tramite il portale di Azure, Azure PowerShell, .NET SDK o l'interfaccia della riga di comando di Azure.
Per comodità, uno script di PowerShell per la creazione di un servizio Data Lake Analytics e per il caricamento di file dei dati di origine è disponibile in [Appendice: Esempio di PowerShell per la preparazione dell'esercitazione](data-lake-analytics-data-lake-tools-get-started.md#appx-a-powershell-sample-for-preparing-the-tutorial).

    Facoltativamente è possibile eseguire le procedure descritte nelle due sezioni seguenti, disponibili nell'articolo [Introduzione ad Azure Data Lake Analytics con il portale di Azure](data-lake-analytics-get-started-portal.md) per creare l'account e caricare i dati manualmente:

    1. [Creare un account di Analisi Data Lake di Azure](data-lake-analytics-get-started-portal.md#create-data-lake-analytics-account).
    2. [Caricare SearchLog.tsv nell'account di archiviazione predefinito di Data Lake](data-lake-analytics-get-started-portal.md).

## <a name="connect-to-azure"></a>Connettersi ad Azure
**Connettersi a Data Lake Analytics**

1. Aprire Visual Studio.
2. Scegliere **Esplora server** dal menu **Visualizza** per aprire Esplora server. In alternativa, premere **[CTRL] + [ALT] + S**.
3. Fare clic con il pulsante destro del mouse su **Azure**, scegliere "Connessione alla sottoscrizione di Microsoft Azure" e quindi seguire le istruzioni.
4. Da **Esplora server** espandere **Azure** e quindi **Data Lake Analytics**. Verrà visualizzato l'elenco degli account di Analisi Data Lake personali, se disponibili. Non è possibile creare account di Analisi Data Lake da Visual Studio. Per creare un account, vedere [Introduzione ad Azure Data Lake Analytics con il portale di Azure](data-lake-analytics-get-started-portal.md) o [Introduzione ad Azure Data Lake Analytics con Azure PowerShell](data-lake-analytics-get-started-powershell.md).

## <a name="upload-source-data-files"></a>Caricare i file dei dati di origine
Alcuni dati sono già stati caricati nell'ambito della sezione **Prerequisiti** di questa esercitazione.  

Per usare i propri dati, seguire questi passaggi per il caricamento di dati Strumenti di Data Lake.

**Caricare i file nell'account di Azure Data Lake dipendente**

1. Da **Esplora server** espandere **Azure**, quindi **Data Lake Analytics**, l'account Data Lake Analytics e **Account di archiviazione**. Verrà visualizzato l'account di archiviazione predefinito di Data Lake, con gli account di archiviazione di Data Lake e gli account di Archiviazione di Azure collegati. L'account di archiviazione predefinito di Data Lake è contraddistinto dall'etichetta "Account di archiviazione predefinito".
2. Fare doppio clic sull'account di archiviazione predefinito di Data Lake e quindi fare clic su **Esplora**.  Viene visualizzato il pannello di esplorazione relativo a Strumenti di Data Lake per Visual Studio.  Nella parte sinistra è presente una visualizzazione albero, mentre la visualizzazione contenuto è disponibile sulla destra.
3. Selezionare la cartella in cui si desidera caricare i file.
4. Fare clic con il pulsante destro del mouse su uno spazio vuoto e fare clic su **Carica**.

    ![Progetto Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-upload-files.png)

**Caricare file in un account di archiviazione BLOB di Azure collegato**

1. Da **Esplora server** espandere **Azure**, quindi **Data Lake Analytics**, l'account Data Lake Analytics e **Account di archiviazione**. Verrà visualizzato l'account di archiviazione predefinito di Data Lake, con gli account di archiviazione di Data Lake e gli account di Archiviazione di Azure collegati.
2. Espandere l'account di Archiviazione di Azure.
3. Fare clic con il pulsante destro del mouse sul contenitore in cui si vuole caricare i file e quindi fare clic su **Esplora**. Se non è disponibile, creare prima di tutto un contenitore usando il portale di Azure, Azure PowerShell o altri strumenti.
4. Selezionare la cartella in cui si desidera caricare i file.
5. Fare clic con il pulsante destro del mouse su uno spazio vuoto e fare clic su **Carica**.

## <a name="develop-u-sql-scripts"></a>Sviluppare script U-SQL
I processi di Data Lake Analtyics vengono scritti nel linguaggio U-SQL. Per altre informazioni su U-SQL, vedere [Introduzione al linguaggio U-SQL](data-lake-analytics-u-sql-get-started.md) e [U-SQL Language Reference](http://go.microsoft.com/fwlink/?LinkId=691348) (Riferimenti al linguaggio U-SQL).

**Creare e inviare un processo di Data Lake Analytics**

1. Scegliere **Nuovo** dal menu **File** e quindi fare clic su **Progetto**.
2. Selezionare il tipo **Progetto U-SQL** .

    ![Nuovo progetto Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. Fare clic su **OK**. Visual Studio crea una soluzione con un file **Script.usql** .
4. Immettere lo script seguente in **Script.usql**:

        @searchlog =
            EXTRACT UserId          int,
                    Start           DateTime,
                    Region          string,
                    Query           string,
                    Duration        int?,
                    Urls            string,
                    ClickedUrls     string
            FROM "/Samples/Data/SearchLog.tsv"
            USING Extractors.Tsv();

        @res =
            SELECT *
            FROM @searchlog;        

        OUTPUT @res   
            TO "/Output/SearchLog-from-Data-Lake.csv"
        USING Outputters.Csv();

    Questo script U-SQL legge il file di dati di origine tramite **Extractors.Tsv()** e quindi crea un file CSV tramite **Outputters.Csv()**.

    Non modificare i due percorsi, a meno che il file di origine non sia stato copiato in una posizione diversa.  Analisi Data Lake creerà la cartella di output, se non esiste già.

    Risulta più semplice usare i percorsi relativi dei file archiviati negli account predefiniti di Data Lake, è possibile usare anche percorsi assoluti.  Ad esempio

        adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv

    È necessario usare percorsi assoluti per accedere ai file presenti negli account di archiviazione collegati.  La sintassi dei file presenti in un account di Archiviazione di Azure collegato è:

        wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv

   > [!NOTE]
   > Non sono attualmente supportate autorizzazioni di accesso a contenitori pubblici o a contenitori BLOB di Azure con BLOB pubblici.  
   >
   >

    Prestare attenzione alle funzionalità seguenti:

   * **IntelliSense**

       Per le entità seguenti vengono visualizzati il nome completato in modo automatico e i membri: Rowset, Classes, Databases, Schemas e User Defined Objects (UDO).

       IntelliSense per le entità di catalogo (Databases, Schemas, Tables, UDO, e così via) è correlato all'account di calcolo personale. È possibile controllare l'account di calcolo, il database e lo schema attualmente attivi nella barra degli strumenti superiore e sostituirli tramite gli elenchi a discesa.
   * **Espandere * le colonne con il simbolo**

       Facendo clic a destra del simbolo *, verrà visualizzata una sottolineatura blu sotto *. Passare il puntatore del mouse sulla sottolineatura blu e quindi fare clic sulla freccia verso il basso.
       ![Espansione di * in Data Lake Tools per Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-expand-asterisk.png)

       Fare clic su **Espandi colonne**e lo strumento sostituirà l'asterisco con i nomi di colonna.
   * **Formattazione automatica**

       Gli utenti possono modificare il rientro dello script U-SQL in base alla struttura di codice definita in Modifica->Avanzate:

     * Formatta documento (Ctrl + E, D): formatta l'intero documento   
     * Formatta selezione (Ctrl+K, Ctrl+F): formatta la selezione. Se non è stata effettuata alcuna selezione, questo collegamento formatta la riga in cui si trova il cursore.  

       Tutte le regole di formattazione possono essere configurate in Strumenti->Opzioni->Editor di testo->SIP->Formattazione.  
   * **Rientro automatico**

       Strumenti di Data Lake per Visual Studio è in grado di impostare automaticamente il rientro delle espressioni durante la scrittura degli script. Per attivare questa funzionalità, disabilitata per impostazione predefinita, è necessario selezionare U-SQL->Opzioni e impostazioni->Opzione->Abilita rientro automatico.
   * **Vai a definizione e Trova tutti i riferimenti**

       Fare clic con il pulsante destro del mouse sul nome di un set di righe/parametro/colonna/UDO e fare clic su Vai a definizione (F12) per accedere alla relativa definizione. Facendo clic su Trova tutti i riferimenti (Shift+F12) verranno invece visualizzati tutti i riferimenti.
   * **Inserimento di percorsi di Azure**

       Con Data Lake Tools per Visual Studio non sarà più necessario ricordare il percorso del file di Azure e digitarlo manualmente, ma sarà sufficiente fare clic con il pulsante destro del mouse nell'editor e scegliere Insert Azure Path (Inserisci percorso di Azure). Selezionare il file nella finestra di dialogo del browser relativo al BLOB di Azure. Fare clic su **OK**. Il percorso del file verrà inserito nel codice personale.
5. Specificare l'account di Analisi Data Lake, il database e lo schema. È possibile selezionare **(local)** per eseguire lo script in locale per finalità di testing. Per altre informazioni, vedere [Eseguire U-SQL in locale](#run-u-sql-locally).

    ![Invio progetto Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

    Per altre informazioni, vedere la pagina di [Usare il catalogo di U-SQL](data-lake-analytics-use-u-sql-catalog.md).
6. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Build Script** (Compila script). Verificare il risultato nel riquadro di output.
7. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Submit Script** (Invia script). In alternativa, è possibile fare clic su **Invia** nel pannello Script.usql.  Vedere l'immagine sopra riportata.  Fare clic sulla freccia rivolta verso il basso accanto al pulsante di invio per accedere alle opzioni avanzate.
8. Specificare un valore in **Nome processo**, verificare il nome presente in **Analytics Account** (Account Analytics) e quindi fare clic su **Invia**. Al termine della procedura di invio, nella finestra dei risultati di Strumenti di Data Lake per Visual Studio saranno disponibili i risultati dell'operazione di invio e il collegamento al processo.

    ![Invio progetto Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
9. Per visualizzare lo stato attuale del processo, è necessario fare clic sul pulsante Aggiorna per aggiornare la schermata. Al termine del processo verranno visualizzate le schede **Job Graph** (Grafico processo), **Meta Data Operations** (Operazioni metadati), **State History** (Cronologia stato), **Diagnostics** (Diagnostica):

    ![Grafico delle prestazioni del processo di Analisi Data Lake per Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * Riepilogo del processo. Mostra le informazioni di riepilogo del processo corrente, tra cui lo stato, lo stato di avanzamento, il tempo di esecuzione, il nome di runtime, l'autore dell'invio e così via.   
   * Dettagli del processo. Visualizza informazioni dettagliate sul processo corrente, tra cui lo script, le risorse e la vista relativa all'esecuzione del vertice.
   * Grafico del processo. Contiene quattro grafici in cui vengono visualizzate graficamente numerose informazioni sul processo, tra cui lo stato di avanzamento, i dati letti, i dati scritti, il tempo di esecuzione, il tempo di esecuzione medio per ogni nodo, la velocità effettiva di input e la velocità effettiva di output.
   * Operazioni sui metadati. Mostra tutte le operazioni eseguite sui metadati.
   * Cronologia dello stato.
   * Diagnostica. Strumenti di Data Lake per Visual Studio diagnosticherà l'esecuzione dei processi in modo automatico e invierà avvisi in caso di errori o problemi di prestazioni nei processi. Per altre informazioni, vedere la sezione relativa alle funzioni di diagnostica del processo (collegamento da definire).

**Per controllare lo stato del processo**

1. Da Esplora server espandere **Azure**, quindi **Data Lake Analytics** e il nome dell'account Data Lake Analytics
2. Fare doppio clic su **Processi** per ottenere un elenco dei processi.
3. Fare clic su un processo per visualizzarne lo stato.

**Per visualizzare l'output del processo**

1. Da **Esplora server** espandere **Azure**, quindi **Data Lake Analytics**, l'account Data Lake Analytics e infine **Account di archiviazione**. Fare clic con il pulsante destro del mouse sull'account Data Lake Analytics predefinito e quindi scegliere **Esplora**.
2. Fare doppio clic su **output** per aprire la cartella.
3. Fare doppio clic su **SearchLog-From-adltools.csv**.

### <a name="job-playback"></a>Riproduzione del processo
Con la riproduzione del processo è possibile controllare lo stato di avanzamento del processo e rilevare visivamente eventuali colli di bottiglia o anomalie delle prestazioni. Questa funzionalità può essere usata sia prima del completamento del processo (ad esempio mentre il processo è ancora in esecuzione), sia dopo il termine dell'esecuzione. Se si esegue la riproduzione durante l'esecuzione del processo, sarà possibile riprodurre lo stato di avanzamento fino all'ora corrente.

**Per visualizzare lo stato di esecuzione del processo**  

1. Fare clic su **Carica profilo** nell'angolo superiore destro. Vedere l'immagine sopra riportata.
2. Fare clic sul pulsante di riproduzione nell'angolo inferiore sinistro per rivedere lo stato di esecuzione del processo.
3. Durante la riproduzione, è possibile fare clic su **Pausa** per arrestarla oppure trascinare direttamente la barra di avanzamento in posizioni specifiche.

### <a name="heat-map"></a>Mappa termica
Strumenti di Data Lake per Visual Studio applica alla visualizzazione del processo sovrapposizioni di colore selezionabili dall'utente per indicare, per ogni fase, lo stato di avanzamento, l'input/output di dati, il tempo di esecuzione e la velocità effettiva di input/output. In questo modo, gli utenti possono individuare in modo diretto e intuitivo eventuali problemi potenziali e la distribuzione delle proprietà del processo. Dall'elenco a discesa è possibile scegliere un'origine dati da visualizzare.  

## <a name="run-u-sql-locally"></a>Eseguire U-SQL in locale

È possibile usare Strumenti di Azure Data Lake per Visual Studio e l'SDK U-SQL di Azure Data Lake per eseguire i processi di U-SQL nella workstation, esattamente come nel servizio Azure Data Lake. Queste due funzionalità eseguite localmente permettono di risparmiare tempo per le operazioni di test e debug dei processi di U-SQL.

* [Eseguire test e debug di processi U-SQL tramite l'esecuzione locale e l'SDK U-SQL di Azure Data Lake](data-lake-analytics-data-lake-tools-local-run.md)


## <a name="see-also"></a>Vedere anche
Per iniziare a usare Analisi Data Lake usando vari tipi di strumenti, vedere:

* [Esercitazione: Introduzione ad Azure Data Lake Analytics con il portale di Azure](data-lake-analytics-get-started-portal.md)
* [Introduzione ad Azure Data Lake Analytics con Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Introduzione ad Analisi Data Lake mediante .NET SDK](data-lake-analytics-get-started-net-sdk.md)
* [Debug dei processi U-SQL](data-lake-analytics-debug-u-sql-jobs.md)

Per conoscere il codice di Data Lake Tools per Visual Studio code, vedere [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md) (Usare il codice di Azure Data Lake Tools per Visual Studio).

Per vedere altri argomenti relativi allo sviluppo:

* [Analizzare blog mediante Analisi Data Lake](data-lake-analytics-analyze-weblogs.md)
* [Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Introduzione al linguaggio U-SQL di Analisi Azure Data Lake](data-lake-analytics-u-sql-get-started.md)
* [Sviluppare operatori U-SQL definiti dall'utente per i processi di Analisi Data Lake](data-lake-analytics-u-sql-develop-user-defined-operators.md)

## <a name="appx-a-powershell-sample-for-preparing-the-tutorial"></a>Appendice: Esempio di PowerShell per la preparazione dell'esercitazione
Lo script di PowerShell seguente prepara automaticamente i dati di origine e un account di Azure Data Lake Analytics, per poter passare alla sezione [Sviluppare script U-SQL](data-lake-analytics-data-lake-tools-get-started.md#develop-u-sql-scripts).

    #region - used for creating Azure service names
    $nameToken = "<Enter an alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - service names
    $resourceGroupName = $namePrefix + "rg"
    $dataLakeStoreName = $namePrefix + "adas"
    $dataLakeAnalyticsName = $namePrefix + "adla"
    $location = "East US 2"
    #endregion


    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an Azure Data Lake Analytics service account
    Write-Host "Create a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Create a Data Lake account ..."  -ForegroundColor Green
    New-AzureRmDataLakeStoreAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $dataLakeStoreName `
        -Location $location

    Write-Host "Create a Data Lake Analytics account ..."  -ForegroundColor Green
    New-AzureRmDataLakeAnalyticsAccount `
        -Name $dataLakeAnalyticsName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultDataLake $dataLakeStoreName

    Write-Host "The newly created Data Lake Analytics account ..."  -ForegroundColor Green
    Get-AzureRmDataLakeAnalyticsAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $dataLakeAnalyticsName  
    #endregion

    #region - prepare the source data
    Write-Host "Import the source data ..."  -ForegroundColor Green
    $localFolder = "C:\Tutorials\Downloads\" # A temp location for the file.
    $storageAccount = "adltutorials"  # Don't modify this value.
    $container = "adls-sample-data"  #Don't modify this value.

    # Create the temp location  
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download the sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName $storageAccount -Anonymous
    $blobs = Azure\Get-AzureStorageBlob -Container $container -Context $context
    $blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload the file to the default Data Lake Store account    
    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $localFolder"SearchLog.tsv" -Destination "/Samples/Data/SearchLog.tsv"

    Write-Host "List the source data ..."  -ForegroundColor Green
    Get-AzureRmDataLakeStoreChildItem -Account $dataLakeStoreName -Path  "/Samples/Data/"
    #endregion

