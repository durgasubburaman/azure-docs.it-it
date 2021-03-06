---
title: Replicare le VM Hyper-V nei cloud VMM in Azure | Microsoft Docs
description: Orchestrare la replica, il failover e il ripristino di macchine virtuali Hyper-V gestite nei cloud di System Center VMM in Azure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: raynew
ms.translationtype: Human Translation
ms.sourcegitcommit: c308183ffe6a01f4d4bf6f5817945629cbcedc92
ms.openlocfilehash: 7de37f106e33d425b3b497cec640bac3fa4afa74
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-site-recovery-in-the-azure-portal"></a>Eseguire la replica di macchine virtuali Hyper-V nei cloud VMM in Azure tramite Site Recovery nel Portale di Azure
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-vmm-to-azure.md)
> * [Azure classico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell - Classica](site-recovery-deploy-with-powershell.md)


Questo articolo illustra come eseguire la replica di macchine virtuali Hyper-V locali gestite nei cloud di System Center VMM in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel Portale di Azure.

È possibile inviare commenti nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Se si desidera eseguire la migrazione di macchine in Azure (senza failback), sono disponibili altre informazioni in [questo articolo](site-recovery-migrate-to-azure.md).


## <a name="deployment-steps"></a>Passaggi di distribuzione

Seguire l'articolo per completare i passaggi di distribuzione seguenti:


1. Ottenere [altre informazioni ](site-recovery-components.md#hyper-v-to-azure) sull'architettura di questa distribuzione. Ottenere inoltre [altre informazioni](site-recovery-hyper-v-azure-architecture.md) sul funzionamento della replica Hyper-V in Site Recovery.
2. Verificare i prerequisiti e le limitazioni.
3. Configurare la rete e gli account di archiviazione di Azure.
4. Preparare il server VMM e gli host Hyper-V locali.
5. Creare un insieme di credenziali dei servizi di ripristino. L'insieme di credenziali contiene le impostazioni di configurazione e orchestra la replica.
6. Specificare le impostazioni di origine. Registrare il server VMM nell'insieme di credenziali. Installare il provider di Azure Site Recovery nel server VMM. Installare l'agente di Servizi di ripristino di Microsoft negli host Hyper-V.
7. Specificare le impostazioni di replica e di destinazione.
8. Abilitare la replica per le VM.
9. Eseguire un failover di test per verificare che tutti gli elementi funzionino come previsto.



## <a name="prerequisites"></a>Prerequisiti


**Requisiti di supporto** | **Dettagli**
--- | ---
**Azure** | Vedere i [requisiti di Azure](site-recovery-prereq.md#azure-requirements).
**Server locali** | [Altre informazioni](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-in-virtual-machine-manager-clouds-to-azure) sui requisiti per il server VMM e gli host Hyper-V locali.
**VM Hyper-V locali** | Le VM da replicare devono eseguire un [sistema operativo supportato](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) ed essere conformi ai [prerequisiti di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL di Azure** | Il server VMM deve poter accedere agli URL seguenti:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se sono presenti regole del firewall basate sull'indirizzo IP, verificare che consentano la comunicazione con Azure.<br/></br> Consentire gli [intervalli IP del data center di Azure ](https://www.microsoft.com/download/confirmation.aspx?id=41653) e la porta HTTPS (443).<br/></br> Consentire gli intervalli di indirizzi IP per l'area di Azure della sottoscrizione e per gli Stati Uniti occidentali (usati per il controllo di accesso e la gestione delle identità).


## <a name="prepare-for-deployment"></a>Preparare la distribuzione
Per preparare la distribuzione è necessario:

1. [Configurare una rete di Azure](#set-up-an-azure-network) in cui verranno collocate le VM di Azure dopo il failover.
2. [Configurare un account di archiviazione di Azure](#set-up-an-azure-storage-account) per i dati replicati.
3. [Preparare il server VMM](#prepare-the-vmm-server) per la distribuzione di Site Recovery.
4. Preparare il mapping di rete. Configurare le reti in modo che sia possibile configurare il mapping di rete durante la distribuzione di Site Recovery.

### <a name="set-up-an-azure-network"></a>Configurare una rete di Azure
È necessario configurare una rete di Azure a cui connettere le VM di Azure create dopo il failover.

* La rete deve trovarsi nella stessa area dell'insieme di credenziali di Servizi di ripristino.
* A seconda del modello di risorsa da usare per le VM di Azure di cui si esegue il failover, la rete di Azure viene configurata in [modalità Resource Manager](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) o in [modalità classica](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* È consigliabile configurare una rete prima di iniziare. In caso contrario sarà necessario eseguire l'operazione durante la distribuzione di Site Recovery.
Le reti di Azure usate da Site Recovery non possono essere [spostate](../azure-resource-manager/resource-group-move-resources.md) all'interno della stessa sottoscrizione o tra sottoscrizioni diverse.

### <a name="set-up-an-azure-storage-account"></a>Configurare un account di archiviazione di Azure
* Per contenere i dati replicati in Azure è necessario un account di archiviazione di Azure Standard/Premium. [Archiviazione Premium](../storage/storage-premium-storage.md) viene usata per le macchine virtuali che necessitano costantemente di prestazioni I/O elevate e bassa latenza per ospitare carichi di lavoro di I/O intensivi. Se si vuole usare un account Premium per archiviare i dati replicati, sarà necessario anche un account di archiviazione standard per l'archiviazione dei log di replica in cui vengono acquisite le modifiche in corso ai dati locali. L'account deve trovarsi nella stessa area dell'insieme di credenziali di Servizi di ripristino.
* A seconda del modello di risorsa da usare per le macchine virtuali di Azure di cui si esegue il failover, l'account deve essere configurato in [modalità Resource Manager](../storage/storage-create-storage-account.md) o in [modalità classica](../storage/storage-create-storage-account-classic-portal.md).
* È consigliabile configurare un account prima di iniziare. In caso contrario sarà necessario eseguire l'operazione durante la distribuzione di Site Recovery.
- Si noti che gli account di archiviazione usati per Site Recovery non possono essere [spostati](../azure-resource-manager/resource-group-move-resources.md) all'interno della stessa sottoscrizione o tra sottoscrizioni diverse.

### <a name="prepare-the-vmm-server"></a>Preparare il server VMM
* Assicurarsi che il server VMM sia conforme ai [prerequisiti](#prerequisites).
* Durante la distribuzione di Site Recovery è possibile specificare la disponibilità di tutti i cloud in un server VMM nel portale di Azure. Per fare in modo che nel portale siano visibili soltanto cloud specifici è possibile abilitare tale impostazione nel cloud dalla console di amministrazione VMM.

### <a name="prepare-for-network-mapping"></a>Preparare il mapping di rete
Durante la distribuzione di Site Recovery è necessario configurare il mapping di rete. Questa operazione esegue il mapping tra le reti VM di VMM di origine e le reti di Azure di destinazione per consentire quanto segue:

* I computer di cui viene eseguito il failover nella stessa rete possono connettersi tra loro, anche se il failover non avviene nello stesso modo o nello stesso piano di ripristino.
* Se nella rete di Azure di destinazione è configurato un gateway di rete, le macchine virtuali di Azure possono connettersi alle macchine virtuali locali.
* Per configurare un mapping di rete è necessario quanto segue:

  * Accertarsi che le macchine virtuali nel server host Hyper-V di origine siano connesse a una rete VM di VMM. È necessario che tale rete sia collegata a una rete logica associata al cloud.
  * Una rete di Azure come descritto [in precedenza](#set-up-an-azure-network)

## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino
1. Accedere al [portale di Azure](https://portal.azure.com).
2. Fare clic su **Nuovo** > **Monitoraggio e gestione** > **Backup e Site Recovery (OMS)**.

    ![Nuovo insieme di credenziali](./media/site-recovery-vmm-to-azure/new-vault3.png)
3. In **Nome**specificare un nome descrittivo per identificare l'insieme di credenziali. Se è disponibile più di una sottoscrizione, selezionarne una.
4. [Creare un gruppo di risorse](../azure-resource-manager/resource-group-template-deploy-portal.md)o selezionarne uno esistente. Specificare un'area di Azure. I computer verranno replicati in quest'area. Per informazioni sulla disponibilità a livello geografico e sulle aree supportate, vedere la pagina relativa ai [dettagli sui prezzi per Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Per accedere rapidamente all'insieme di credenziali dal dashboard, fare clic su **Aggiungi al dashboard** > **Crea insieme di credenziali**.

    ![Nuovo insieme di credenziali](./media/site-recovery-vmm-to-azure/new-vault.png)

Il nuovo insieme di credenziali verrà visualizzato in **Dashboard** > **Tutte le risorse** e nel pannello **Insiemi di credenziali dei servizi di ripristino** principale.


## <a name="select-the-protection-goal"></a>Selezionare l'obiettivo di protezione

Selezionare gli elementi da replicare e la posizione in cui eseguire la replica.

1. In **Insiemi di credenziali dei servizi di ripristino** selezionare l'insieme di credenziali.
2. In **Introduzione** fare clic su **Site Recovery** > **Preparare l'infrastruttura** > **Obiettivo di protezione**.

    ![Scegliere gli obiettivi](./media/site-recovery-vmm-to-azure/choose-goals.png)
3. In **Obiettivo di protezione** selezionare **In Azure** e scegliere **Sì, con Hyper-V**. Selezionare **Sì** per confermare l'uso di VMM per la gestione degli host Hyper-V e del sito di ripristino. Fare quindi clic su **OK**.

## <a name="set-up-the-source-environment"></a>Configurare l'ambiente di origine

Installare il provider di Azure Site Recovery nel server VMM e registrare il server nell'insieme di credenziali. Installare l'agente di Servizi di ripristino di Azure negli host Hyper-V.

1. Fare clic su **Preparare l'infrastruttura** > **Origine**.

    ![Impostare l'origine](./media/site-recovery-vmm-to-azure/set-source1.png)

2. In **Prepara origine** fare clic su **+ VMM** per aggiungere un server VMM.

    ![Impostare l'origine](./media/site-recovery-vmm-to-azure/set-source2.png)

3. In **Aggiungi server** verificare che in **Tipo di server** sia visualizzato **System Center VMM server** (Server System Center VMM) e che il server VMM sia conforme a [prerequisiti e requisiti URL](#prerequisites).
4. Scaricare il file di installazione del provider di Azure Site Recovery.
5. Scaricare la chiave di registrazione, che sarà necessaria durante l'installazione. La chiave è valida per cinque giorni dal momento in cui viene generata.

    ![Impostare l'origine](./media/site-recovery-vmm-to-azure/set-source3.png)


## <a name="install-the-provider-on-the-vmm-server"></a>Installare il provider nel server VMM

1. Eseguire il file di installazione del provider in ogni server VMM.
2. In **Microsoft Update** è possibile acconsentire esplicitamente agli aggiornamenti in modo che gli aggiornamenti del provider vengano installati in base ai criteri di Microsoft Update.
3. In **Installazione** accettare o modificare il percorso predefinito di installazione del provider e quindi fare clic su **Installa**.

    ![Percorso di installazione](./media/site-recovery-vmm-to-azure/provider2.png)
4. Al termine dell'installazione fare clic su **Registra** per registrare il server VMM nell'insieme di credenziali.
5. Nella pagina **Impostazioni dell'insieme di credenziali** fare clic su **Sfoglia** per selezionare il file di chiave dell'insieme di credenziali. Specificare la sottoscrizione di Azure Site Recovery e il nome dell'insieme di credenziali.

    ![Server registration](./media/site-recovery-vmm-to-azure/provider10.PNG)
6. In **Connessione Internet**specificare la modalità di connessione a Site Recovery tramite Internet del provider in esecuzione nel server VMM.

   * Per fare in modo che il provider si connetta direttamente, selezionare **Connetti direttamente ad Azure Site Recovery senza server proxy**.
   * Se per il proxy esistente è necessaria l'autenticazione o si vuole usare un proxy personalizzato, selezionare **Connetti ad Azure Site Recovery usando un server proxy**.
   * Se si usa un proxy personalizzato è necessario specificare l'indirizzo, la porta e le credenziali.
   * Se si usa un proxy, è necessario che gli URL descritti nei [prerequisiti](#on-premises-prerequisites) siano già consentiti.
   * Se si usa un proxy personalizzato, un account RunAs di VMM (DRAProxyAccount) verrà creato automaticamente con le credenziali del proxy specificate. Configurare il server proxy in modo che l'account possa eseguire correttamente l'autenticazione. Le impostazioni dell'account RunAs di VMM possono essere modificate nella console VMM. In **Impostazioni** espandere **Sicurezza** > **Account RunAs** e quindi modificare la password di DRAProxyAccount. È necessario riavviare il servizio VMM per rendere effettiva l'impostazione.

     ![Internet](./media/site-recovery-vmm-to-azure/provider13.PNG)
7. Accettare o modificare il percorso del certificato SSL generato automaticamente per la crittografia dei dati. Questo certificato viene usato se si abilita la crittografia dei dati per un cloud protetto da Azure nel portale di Azure Site Recovery. Conservare il certificato in una posizione sicura, Se la crittografia dei dati è abilitata, quando si esegue un failover in Azure è necessario eseguire la decrittografia.
8. In **Nome server**specificare un nome descrittivo per identificare il server VMM nell'insieme di credenziali. In una configurazione cluster specificare il nome del ruolo relativo al cluster VMM.
9. Abilitare **Sincronizza i metadati cloud** per sincronizzare i metadati relativi a tutti i cloud presenti nel server VMM con l'insieme di credenziali. È necessario eseguire questa azione solo una volta in ogni server. Se non si vogliono sincronizzare tutti i cloud, è possibile lasciare deselezionata questa opzione e sincronizzare ogni cloud singolarmente nelle proprietà del cloud nella console VMM. Fare clic su **Register** per completare il processo.

    ![Server registration](./media/site-recovery-vmm-to-azure/provider16.PNG)
10. Verrà avviata la registrazione. Al termine della registrazione, il server verrà visualizzato in **Infrastruttura di Site Recovery** > **Server VMM**.


## <a name="install-the-azure-recovery-services-agent-on-hyper-v-hosts"></a>Installare l'agente di Servizi di ripristino di Azure negli host Hyper-V

1. Dopo aver configurato il provider è necessario scaricare il file di installazione per l'agente di Servizi di ripristino di Azure. Eseguire l'installazione in ogni server Hyper-V nel cloud VMM.

    ![Siti Hyper-V](./media/site-recovery-vmm-to-azure/hyperv-agent1.png)
2. In **Controllo dei prerequisiti** fare clic su **Avanti**. Gli eventuali prerequisiti mancanti verranno installati automaticamente.

    ![Prerequisiti per l'agente di Servizi di ripristino di Azure](./media/site-recovery-vmm-to-azure/hyperv-agent2.png)
3. In **Impostazioni di installazione** accettare o modificare il percorso di installazione e il percorso della cache. È possibile configurare la cache in un'unità con almeno 5 GB di spazio di archiviazione disponibile ma è consigliabile usare un disco della cache con almeno 600 GB di spazio disponibile. Fare clic su **Installa**.
4. Al termine dell'installazione fare clic su **Chiudi** per completare l'operazione.

    ![Registrare l'Agente di Servizi di ripristino di Microsoft Azure](./media/site-recovery-vmm-to-azure/hyperv-agent3.png)

### <a name="command-line-installation"></a>Installazione dalla riga di comando
È possibile installare l'agente di Servizi di ripristino di Microsoft Azure dalla riga di comando con questo comando:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-to-site-recovery-from-hyper-v-hosts"></a>Impostare l'accesso tramite proxy Internet a Site Recovery da host Hyper-V

L'agente di servizi di ripristino in esecuzione negli host Hyper-V richiede l'accesso ad Azure tramite Internet per la replica delle macchine virtuali. Se si accede a Internet tramite un proxy, configurarlo come indicato di seguito:

1. Aprire lo snap-in di MMC di Backup di Microsoft Azure nell'host Hyper-V. Per impostazione predefinita, un collegamento a Backup di Microsoft Azure è disponibile sul desktop oppure in: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Nello snap-in fare clic su **Modifica proprietà**.
3. Nella scheda **Configurazione proxy** specificare le informazioni del server proxy.

    ![Registrare l'Agente di Servizi di ripristino di Microsoft Azure](./media/site-recovery-vmm-to-azure/mars-proxy.png)
4. Assicurarsi che l'agente possa raggiungere gli URL indicati nei [prerequisiti](#on-premises-prerequisites).

## <a name="set-up-the-target-environment"></a>Configurare l'ambiente di destinazione
Specificare l'account di archiviazione di Azure da usare per la replica e la rete di Azure a cui le macchine virtuali di Azure dovranno connettersi dopo il failover.

1. Fare clic su **Preparare l'infrastruttura** > **Destinazione**, selezionare la sottoscrizione e il gruppo di risorse in cui si vuole creare il failover delle macchine virtuali. Scegliere il modello di distribuzione che si vuole usare in Azure (classica o con Resource Manager) per il failover delle macchine virtuali.

    ![Archiviazione](./media/site-recovery-vmm-to-azure/enablerep3.png)

2. Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.

    ![Archiviazione](./media/site-recovery-vmm-to-azure/compatible-storage.png)

3. Per creare un account di archiviazione con Resource Manager, se non è già stato fatto, fare clic su **+ Account di archiviazione** per eseguire l'operazione inline.  Nel pannello **Crea account di archiviazione** specificare il nome, il tipo, la sottoscrizione e la località dell'account. L'account deve trovarsi nella stessa località dell'insieme di credenziali di Servizi di ripristino.

   ![Archiviazione](./media/site-recovery-vmm-to-azure/gs-createstorage.png)


   * Per creare un account di archiviazione con il modello di distribuzione classica, usare il portale di Azure. [Altre informazioni](../storage/storage-create-storage-account-classic-portal.md)
   * Se si usa un account di archiviazione Premium per i dati replicati, configurare un account di archiviazione Standard aggiuntivo per l'archiviazione dei log di replica in cui vengono acquisite le modifiche in corso ai dati locali.
5. Per creare una rete di Azure con Resource Manager, se non è già stato fatto, fare clic su **+ Rete** per eseguire l'operazione inline. Nel pannello **Crea rete virtuale** specificare il nome, l'intervallo di indirizzi, i dettagli della subnet, la sottoscrizione e la località della rete. La rete deve trovarsi nella stessa località dell'insieme di credenziali di Servizi di ripristino.

   ![Rete](./media/site-recovery-vmm-to-azure/gs-createnetwork.png)

   Per creare una rete con il modello di distribuzione classica, usare il portale di Azure. [Altre informazioni](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

### <a name="configure-network-mapping"></a>Configurare il mapping di rete

* [Fare clic qui](#prepare-for-network-mapping) per una panoramica rapida del funzionamento del mapping di rete.
* Verificare che le macchine virtuali nel server VMM siano connesse a una rete VM e di aver creato almeno una rete virtuale di Azure. È possibile mappare più reti VM a una singola rete di Azure.

Per configurare il mapping, procedere come segue:

1. In **Infrastruttura di Site Recovery** > **Mapping di rete** > **Mapping di rete** fare clic sull'icona **+Mapping di rete**.

    ![Mapping di rete](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. In **Aggiungi mapping di rete** selezionare il server VMM di origine e **Azure** come destinazione.
3. Verificare la sottoscrizione e il modello di distribuzione dopo il failover.
4. In **Rete di origine**selezionare la rete VM locale di origine di cui si vuole eseguire il mapping dall'elenco associato al server VMM.
5. In **Rete di destinazione**selezionare la rete di Azure in cui inserire le macchine virtuali di Azure di replica dopo la creazione. Fare quindi clic su **OK**.

    ![Mapping di rete](./media/site-recovery-vmm-to-azure/network-mapping2.png)

Quando ha inizio il mapping di rete vengono eseguite le operazioni seguenti:

* Le macchine virtuali esistenti nella rete VM di origine vengono connesse alla rete di destinazione quando ha inizio il mapping. Le nuove macchine virtuali connesse alla rete VM di origine vengono connesse alla rete di Azure di cui è stato eseguito il mapping quando viene eseguita la replica.
* Se si modifica un mapping di rete esistente, le macchine virtuali di replica si connettono usando le nuove impostazioni.
* Se la rete di destinazione dispone di più subnet e una di esse ha lo stesso nome di una subnet in cui si trova la macchina virtuale di origine, la macchina virtuale di replica si connette a questa subnet di destinazione dopo il failover.
* Se non è presente una subnet di destinazione con un nome corrispondente, la macchina virtuale si connette alla prima subnet della rete.

## <a name="configure-replication-settings"></a>Configurare le impostazioni di replica
1. Per creare nuovi criteri di replica, fare clic su **Preparare l'infrastruttura** > **Impostazioni della replica** > **+Crea e associa**.

    ![Rete](./media/site-recovery-vmm-to-azure/gs-replication.png)
2. In **Criteri di creazione e associazione**specificare il nome dei criteri.
3. In **Frequenza di copia**specificare la frequenza con cui replicare i dati differenziali dopo la replica iniziale, ogni 30 secondi oppure ogni 5 o 15 minuti.

    > [!NOTE]
    >  Quando si esegue la replica in archiviazione Premium la frequenza di 30 secondi non è supportata. Il limite è determinato dal numero di snapshot per BLOB (100) supportato dal servizio di archiviazione Premium. [Altre informazioni](../storage/storage-premium-storage.md#snapshots-and-copy-blob)

4. In **Conservazione del punto di ripristino**specificare la durata in ore dell'intervallo di conservazione per ogni punto di ripristino. I computer protetti possono essere ripristinati in qualsiasi punto all'interno di un intervallo.
5. In **Frequenza snapshot coerenti con l'app**specificare la frequenza, da 1 a 12 ore, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione. Hyper-V utilizza due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale e uno snapshot coerente con l'applicazione che accetta uno snapshot temporizzato dei dati dell'applicazione all'interno della macchina virtuale. Negli snapshot coerenti dell'applicazione viene usato il servizio Copia Shadow del volume (VSS) per garantire che le applicazioni siano coerenti durante la creazione dello snapshot. Si noti che un'eventuale abilitazione di snapshot coerenti dell'applicazione influirà sulle prestazioni delle applicazioni in esecuzione nelle macchine virtuali di origine. Assicurarsi che il valore impostato sia inferiore al numero di punti di ripristino aggiuntivi configurati.
6. In **Ora di inizio della replica iniziale** specificare quando deve essere avviata la replica iniziale. La replica avviene sulla larghezza di banda Internet. È quindi consigliabile pianificarla al di fuori dell'orario di lavoro.
7. In **Crittografare i dati archiviati in Azure**specificare se crittografare i dati inattivi in Archiviazione di Azure. Fare quindi clic su **OK**.

    ![Criteri di replica](./media/site-recovery-vmm-to-azure/gs-replication2.png)
8. Quando si creano nuovi criteri, questi vengono associati automaticamente al cloud VMM. Fare clic su **OK**. È possibile associare altri cloud VMM (e le VM in essi contenute) a questi criteri di replica in **Replica** > nome del criterio > **Associate VMM Cloud (Associa cloud VMM)**.

    ![Criteri di replica](./media/site-recovery-vmm-to-azure/policy-associate.png)

## <a name="capacity-planning"></a>Pianificazione della capacità

Dopo avere configurato l'infrastruttura di base, passare alla pianificazione della capacità e valutare se sono necessarie altre risorse.

In Site Recovery è disponibile lo strumento Capacity Planner, che permettere di allocare le risorse appropriate all'ambiente di origine, i componenti di Site Recovery, la rete e l'archiviazione. È possibile eseguire lo strumento di pianificazione in modalità rapida, per ottenere stime basate su un numero medio di macchine virtuali, dischi e risorse di archiviazione, oppure in modalità dettagliata, dove si inseriscono le cifre a livello di carico di lavoro. Prima di iniziare:

* Raccogliere informazioni sull'ambiente di replica, incluse le macchine virtuali, i dischi per ogni macchina virtuale e le risorse di archiviazione per ogni disco.
* Stimare la frequenza di modifica giornaliera (varianza) prevista per i dati replicati. A questo scopo è possibile usare lo strumento [Capacity Planner for Hyper-V Replica](https://www.microsoft.com/download/details.aspx?id=39057) .

1. Fare clic su **Download** per scaricare lo strumento e quindi eseguirlo. [Vedere l'articolo](site-recovery-capacity-planner.md) fornito con lo strumento.
2. Al termine scegliere **Sì** in **Have you run the Capacity Planner**(È stato eseguito lo strumento Capacity Planner?).

   ![Pianificazione della capacità](./media/site-recovery-vmm-to-azure/gs-capacity-planning.png)

   Ulteriori informazioni sul [controllo della larghezza di banda di rete](#network-bandwidth-considerations)




## <a name="enable-replication"></a>Abilitare la replica

Prima di iniziare, verificare che l'account utente di Azure disponga delle [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) necessarie per abilitare la replica di una nuova macchina virtuale in Azure.

Per abilitare la replica, procedere come descritto di seguito.

1. Fare clic su **Passaggio 2: Eseguire la replica dell'applicazione** > **Origine**. Dopo avere abilitato la replica per la prima volta, è necessario fare clic su **+Replica** nell'insieme di credenziali per abilitare la replica per altre macchine.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication1.png)
2. Nel pannello **Origine** selezionare il cloud e il server VMM in cui si trovano gli host Hyper-V. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication-source.png)
3. In **Destinazione** selezionare la sottoscrizione, il modello di distribuzione da usare dopo il failover e l'account di archiviazione usato per i dati replicati.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication-target.png)
4. Selezionare l'account di archiviazione da usare. Per usare un account di archiviazione diverso da quelli disponibili, è possibile [crearne uno](#set-up-an-azure-storage-account). Se si usa un account di archiviazione Premium per i dati replicati, è necessario selezionare un account di archiviazione Standard aggiuntivo per l'archiviazione dei log di replica in cui vengono acquisite le modifiche in corso ai dati locali. Per creare un account di archiviazione usando il modello di Resource Manager, fare clic su **Crea nuovo**. Per creare un account di archiviazione con il modello di distribuzione classica, usare il [portale di Azure](../storage/storage-create-storage-account-classic-portal.md). Fare quindi clic su **OK**.
5. Selezionare la rete di Azure e la subnet a cui dovranno connettersi le VM di Azure create dopo il failover. Scegliere **Configurare ora per le macchine virtuali selezionate** per applicare le impostazioni di rete a tutti i computer selezionati per la protezione. Scegliere **Configurare in seguito** per selezionare la rete di Azure per ogni computer. Se si vuole usare una rete diversa da quelle disponibili, è possibile [crearne una](#set-up-an-azure-network). Per creare una rete con il modello di distribuzione di Resource Manager, fare clic su **Crea nuovo**. Per creare una rete con il modello di distribuzione classica, usare il [portale di Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Selezionare una subnet, se applicabile. Fare quindi clic su **OK**.
6. In **Macchine virtuali** > **Seleziona macchine virtuali** fare clic per selezionare tutte le macchine virtuali da replicare. È possibile selezionare solo i computer per cui è possibile abilitare la replica. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication5.png)

7. In **Proprietà** > **Configura proprietà**selezionare il sistema operativo per le VM selezionate e il disco del sistema operativo.

    - Verificare che il nome della VM di Azure (nome di destinazione) sia conforme ai [requisiti per le macchine virtuali di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Per impostazione predefinita, tutti i dischi della VM sono selezionati per la replica. È tuttavia possibile cancellarli per escluderli,

        - ad esempio per ridurre la larghezza di banda di replica. È possibile evitare, ad esempio, di replicare i dischi con dati temporanei o dati che vengono aggiornati ad ogni riavvio di un computer o di un'applicazione, come pagefile.sys o tempdb di Microsoft SQL Server. Per escludere un disco dalla replica, è sufficiente selezionarlo.
        - Solo i dischi di base possono essere esclusi dalla replica. Non è possibile escludere dischi del sistema operativo
        - e non è consigliabile escludere dischi dinamici. Site Recovery non può determinare se un disco rigido virtuale all'interno della macchina virtuale guest è di base o dinamico. Se non sono esclusi tutti i volumi dinamici dipendenti, in caso di failover della VM il disco dinamico protetto risulterà guasto e non sarà possibile accedere ai dati presenti su tale disco.
        - Dopo aver abilitato la replica, non è più possibile aggiungere o rimuovere dischi da replicare. Se si desidera aggiungere o escludere un disco, è necessario disabilitare la protezione della macchina virtuale e riabilitarla al termine dell'operazione.
        - Per i dischi creati manualmente in Azure non viene eseguito il failback. Ad esempio, se si esegue il failover di tre dischi e se ne creano due direttamente in Azure, verrà eseguito il failback da Azure a Hyper-V soltanto dei tre dischi. Non è possibile includere nel failback o nella replica inversa da Hyper-V ad Azure i dischi creati manualmente.
        - Se si esclude un disco necessario per il funzionamento di un'applicazione, dopo il failover in Azure è necessario crearlo manualmente in Azure per consentire l'esecuzione dell'applicazione replicata. È possibile in alternativa integrare Automazione di Azure in un piano di ripristino per creare il disco durante il failover del computer.

    Fare clic su **OK** per salvare le modifiche. È possibile impostare proprietà aggiuntive in un secondo momento.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

8. In **Impostazioni della replica** > **Configurare le impostazioni di replica** selezionare i criteri di replica da applicare per le VM protette. Fare quindi clic su **OK**. È possibile modificare i criteri di replica in **Criteri di replica** > nome del criterio > **Modifica impostazioni**. Le modifiche applicate vengono usate per i computer di cui è già in corso la replica e per i nuovi computer.

   ![Abilitare la replica](./media/site-recovery-vmm-to-azure/enable-replication7.png)

È possibile tenere traccia dello stato del processo **Abilita protezione** in **Processi** > **Site Recovery jobs** (Processi di Site Recovery). Dopo l'esecuzione del processo **Finalizza protezione** la macchina virtuale è pronta per il failover.

### <a name="view-and-manage-vm-properties"></a>Visualizzare e gestire le proprietà della macchina virtuale

È consigliabile verificare le proprietà del computer di origine. Tenere presente che il nome della VM di Azure deve essere conforme ai [requisiti delle macchine virtuali di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. In **Elementi protetti** fare clic su **Elementi replicati** e selezionare il computer per visualizzarne i dettagli.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/vm-essentials.png)
2. In **Proprietà** sono disponibili le informazioni su replica e failover per la VM.

    ![Abilitare la replica](./media/site-recovery-vmm-to-azure/test-failover2.png)
3. In **Calcolo e rete** > **Proprietà di calcolo** è possibile specificare le dimensioni di destinazione e il nome della VM di Azure. Se necessario, modificare il nome in modo che sia conforme ai [requisiti di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) . È anche possibile visualizzare e modificare le informazioni sulla rete di destinazione, la subnet e l'indirizzo IP assegnati alla VM di Azure.
Si noti che:

   * È possibile impostare l'indirizzo IP di destinazione. Se non si specifica un indirizzo, il computer di cui è stato eseguito il failover usa DHCP. Se si imposta un indirizzo che non è disponibile al momento del failover, il failover ha esito negativo. Se l'indirizzo è disponibile nella rete di failover di test, è possibile usare lo stesso indirizzo IP di destinazione per il failover di test.
   * Il numero di schede di rete dipende dalle dimensioni specificate per la macchina virtuale di destinazione, come illustrato di seguito:

     * Se il numero di schede di rete nella macchina di origine è minore o uguale al numero di schede consentite per la macchina di destinazione, la destinazione avrà lo stesso numero di schede dell’origine.
     * Se il numero di schede per la macchina virtuale di origine supera il numero consentito per le dimensioni di destinazione, verrà usata la dimensione di destinazione massima.
     * Ad esempio, se una macchina di origine dispone di due schede di rete e le dimensioni della macchina di destinazione ne supportano quattro, la macchina di destinazione avrà due schede. Se la macchina di origine dispone di due schede ma le dimensioni di destinazione supportate ne consentono solo una, la macchina di destinazione avrà una sola scheda.     
     * Se la VM ha più schede di rete, si connetteranno tutte alla stessa rete.

     ![Abilitare la replica](./media/site-recovery-vmm-to-azure/test-failover4.png)

4. In **Dischi** è possibile visualizzare il sistema operativo e i dischi dati della VM che verranno replicati.

#### <a name="managed-disks"></a>Dischi gestiti

In **Calcolo e rete** > **Proprietà di calcolo** è possibile impostare l'opzione "Usa dischi gestiti" della macchina virtuale su "Sì" per collegare i dischi gestiti al computer in uso al momento della migrazione in Azure. Managed Disks semplifica la gestione dei dischi per le macchine virtuali IaaS di Azure grazie alla gestione degli account di archiviazione associati ai dischi delle macchine virtuali. [Altre informazioni su Managed Disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - I dischi gestiti vengono creati e collegati alla macchina virtuale solo in caso di failover in Azure. Abilitando la protezione, i dati verranno comunque replicati dai computer locali agli account di archiviazione.
   È possibile creare dischi gestiti solo per le macchine virtuali distribuite tramite il modello di distribuzione di Resource Manager.  

  > [!NOTE]
  > Il failback da Azure all'ambiente Hyper-V locale non è al momento supportato per i computer con dischi gestiti. Impostare l'opzione "Usa dischi gestiti" su "Sì" solo se si prevede di eseguire la migrazione della macchina in Azure.

   - Quando l'opzione "Usa dischi gestiti" viene impostata su "Sì", nel gruppo di risorse è possibile selezionare solo i set di disponibilità con l'opzione "Usa dischi gestiti" impostata su "Sì". Infatti, le macchine virtuali con dischi gestiti possono solo far parte di set di disponibilità la cui proprietà "Usa dischi gestiti" è impostata su "Sì". Verificare di creare set di disponibilità con la proprietà "Usa dischi gestiti" impostata in funzione dell'intenzione di usare i dischi gestiti in caso di failover.  Allo stesso modo, quando l'opzione "Usa dischi gestiti" è impostata su "No", nel gruppo di risorse è possibile selezionare solo i set di disponibilità con la proprietà "Usa dischi gestiti" impostata su "No". [Altre informazioni sui dischi gestiti e i set di disponibilità](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Se l'account di archiviazione usato per la replica è stato crittografato con Crittografia del servizio di archiviazione in un qualsiasi momento, la creazione dei dischi gestiti durante il failover non avrà esito positivo. È possibile impostare "Usa dischi gestiti" su "No" e ripetere il failover oppure disabilitare la protezione per la macchina virtuale e proteggerla in un account di archiviazione per il quale non sia attivata la Crittografia del servizio di archiviazione in qualsiasi momento.
  > [Altre informazioni su Crittografia del servizio di archiviazione e dischi gestiti](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-the-deployment"></a>Test della distribuzione

Per testare la distribuzione è possibile eseguire un failover di test per una singola macchina virtuale o un piano di ripristino che contenga una o più macchine virtuali.

### <a name="before-you-start"></a>Prima di iniziare

 - Per connettersi alle macchine virtuali di Azure con RDP dopo il failover, seguire le istruzioni per la [preparazione alla connessione](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - Per un test completo è necessario copiare Active Directory e DNS nell'ambiente di test. [Altre informazioni](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Eseguire un failover di test

1. Per eseguire il failover di una VM, in **Elementi replicati** fare clic sulla VM e quindi su **+Failover di test**.
2. Per eseguire il failover di un piano di ripristino, in **Piani di ripristino** fare clic con il pulsante destro del mouse sul piano e quindi su **Failover di test**. Per creare un piano di ripristino, [seguire queste istruzioni](site-recovery-create-recovery-plans.md).
3. In **Failover di test** selezionare la rete di Azure a cui dovranno connettersi le VM di Azure dopo il failover.
4. Fare clic su **OK** per iniziare il failover. Per tenere traccia dello stato del processo, fare clic sulla VM per visualizzarne le proprietà oppure sul processo **Failover di test** in **Processi di Site Recovery**.
5. Al termine del failover sarà possibile visualizzare la macchina virtuale di Azure di replica in **Macchine virtuali** nel portale di Azure. Assicurarsi che la VM sia delle dimensioni appropriate, che sia connessa alla rete giusta e che sia in esecuzione.
6. Se sono state preparate le connessioni dopo il failover, sarà possibile connettersi alla VM di Azure.
7. Al termine, fare clic su **Cleanup test failover** (Pulizia failover di test) nel piano di ripristino. Fare clic su **Note** per registrare e salvare eventuali osservazioni associate al failover di test. Verranno eliminate le macchine virtuali create durante il failover di test.

Per altre informazioni, vedere l'articolo [Failover di test in Azure](site-recovery-test-failover-to-azure.md).

## <a name="monitor-the-deployment"></a>Monitorare la distribuzione

Per monitorare le impostazioni di configurazione, lo stato e l'integrità della distribuzione di Site Recovery, seguire questa procedura:

1. Fare clic sul nome dell'insieme di credenziali per accedere al dashboard **Informazioni di base** . In questo dashboard è possibile visualizzare i processi di Site Recovery, lo stato della replica, i piani di ripristino, l'integrità del server e gli eventi.  Il dashboard **Informazioni di base** può essere personalizzato con i riquadri e i layout più utili all'utente, incluso lo stato degli insiemi di credenziali di Backup e di Site Recovery.

    ![Informazioni di base](./media/site-recovery-vmm-to-azure/essentials.png)
2. In **Integrità** è possibile monitorare i problemi sui server locali (VMM o server di configurazione) e gli eventi generati da Site Recovery nelle ultime 24 ore.
3. È possibile gestire e monitorare la replica nei riquadri **Elementi replicati**, **Piani di ripristino** e **Processi di Site Recovery**. Per eseguire il drill-down dei processi, accedere a **Processi** > **Processi di Site Recovery**.

## <a name="command-line-installation-for-the-azure-site-recovery-provider"></a>Installazione dalla riga di comando per il provider di Azure Site Recovery

Il provider di Azure Site Recovery può essere installato dalla riga di comando. Questo metodo può essere usato per installare il provider in un Server Core per Windows Server 2012 R2.

1. Scaricare il file di installazione del provider e il codice di registrazione in una cartella, ad esempio C:\ASR.
2. Da un prompt dei comandi con privilegi elevati eseguire questi comandi per estrarre il programma di installazione del provider:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Eseguire questo comando per installare i componenti:

            C:\ASR> setupdr.exe /i
4. Quindi eseguire questi comandi per registrare il server nell'insieme di credenziali:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of the server> /Credentials <path of the credentials file> /EncryptionEnabled <full file name to save the encryption certificate>       

Dove:

* **/Credentials**: parametro obbligatorio che specifica la posizione in cui si trova il file della chiave di registrazione.  
* **/FriendlyName**: parametro obbligatorio per il nome del server host Hyper-V che viene visualizzato nel portale di Azure Site Recovery.
* * **/EncryptionEnabled**: parametro facoltativo usato quando si esegue la replica di macchine virtuali Hyper-V nei cloud VMM in Azure. Specificare se le macchine virtuali devono essere crittografate in Azure (crittografia dei dati inattivi). Assicurarsi che il nome del file abbia l'estensione **pfx** . La crittografia è disabilitata per impostazione predefinita.
* **/proxyAddress**: parametro facoltativo che specifica l'indirizzo del server proxy.
* **/proxyport**: parametro facoltativo che specifica la porta del server proxy.
* **/proxyUsername**: parametro facoltativo che specifica il nome utente proxy, se il proxy richiede l'autenticazione.
* **/proxyPassword**: parametro facoltativo che specifica la password per l'autenticazione con il server proxy, se il proxy richiede l'autenticazione.


### <a name="network-bandwidth-considerations"></a>Considerazioni sulla larghezza di banda di rete
Lo strumento Capacity Planner può essere usato per calcolare la larghezza di banda necessaria per la replica iniziale e poi quella differenziale. Per controllare la quantità di larghezza di banda usata per la replica è possibile scegliere una delle opzioni seguenti:

* **Limitare la larghezza di banda**: il traffico Hyper-V che viene replicato in un sito secondario passa attraverso un host Hyper-V specifico. È possibile limitare la larghezza di banda nel server host.
* **Perfezionare la larghezza di banda**: è possibile influire sulla larghezza di banda usata per la replica tramite una coppia di chiavi del Registro di sistema.

#### <a name="throttle-bandwidth"></a>Limitare la larghezza di banda
1. Aprire lo snap-in di MMC di Backup di Microsoft Azure nel server host Hyper-V. Per impostazione predefinita, un collegamento a Backup di Microsoft Azure è disponibile sul desktop oppure in: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Nello snap-in fare clic su **Modifica proprietà**.
3. Nella scheda **Limitazione larghezza di banda rete** selezionare **Abilita la limitazione all'uso della larghezza di banda Internet per le operazioni di backup** e impostare i limiti per le ore lavorative e non lavorative. Gli intervalli validi sono compresi tra 512 Kbps e 102 Mbps al secondo.

    ![Limitare la larghezza di banda](./media/site-recovery-vmm-to-azure/throttle2.png)

È anche possibile usare il cmdlet [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) per impostare la limitazione. Di seguito è riportato un esempio:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica che non è necessaria alcuna limitazione.

#### <a name="influence-network-bandwidth"></a>Influire sulla larghezza di banda di rete
Il valore **UploadThreadsPerVM** del Registro di sistema controlla il numero di thread usati per il trasferimento dei dati di un disco, durante la replica iniziale o differenziale. Un valore più elevato aumenta la larghezza di banda di rete usata per la replica. Il valore **DownloadThreadsPerVM** del Registro di sistema specifica il numero di thread usati per il trasferimento dei dati durante il failback.

1. Nel Registro di sistema passare a **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.

   * Per controllare i thread usati per la replica dei dischi, modificare il valore **UploadThreadsPerVM** o creare la chiave, se non esiste.
   * Per controllare i thread usati per il traffico di failback da Azure, modificare il valore **DownloadThreadsPerVM** o creare la chiave, se non esiste.
2. Il valore predefinito è 4. In una rete con provisioning eccessivo è necessario modificare i valori predefiniti di queste chiavi del Registro di sistema. Il valore massimo è 32. Monitorare il traffico per ottimizzare il valore.

## <a name="next-steps"></a>Passaggi successivi

Al termine della replica iniziale e dei test della distribuzione, è possibile chiamare i failover in caso di necessità. Altre informazioni sui diversi tipi di failover e su come eseguirli sono disponibili [qui](site-recovery-failover.md).

