---
title: Scenari di ripristino di emergenza per macchine virtuali di Azure | Documentazione Microsoft
description: Informazioni su cosa fare in caso di un&quot;interruzione di servizio di Azure che influisce sulle macchine virtuali di Azure.
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
translationtype: Human Translation
ms.sourcegitcommit: 0d8472cb3b0d891d2b184621d62830d1ccd5e2e7
ms.openlocfilehash: b1fb88277f6da86c023cd63af0d7c2c5681f8be0
ms.lasthandoff: 03/21/2017


---
# <a name="what-to-do-in-the-event-that-an-azure-service-disruption-impacts-azure-vms"></a>Cosa fare in caso di un'interruzione di servizio di Azure che influisce sulle macchine virtuali di Azure
Microsoft si impegna costantemente per garantire agli utenti la disponibilità dei servizi in base alle esigenze. Eventi imprevisti possono, tuttavia, causare interruzioni non pianificate dei servizi.

La connettività e la disponibilità dei servizi Microsoft sono garantite da un contratto di servizio. I contratti di servizio relativi ai singoli servizi di Azure sono disponibili alla pagina [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).

Azure offre già diverse funzionalità della piattaforma predefinite che supportano applicazioni a disponibilità elevata. Per altre informazioni su questi servizi, vedere [Ripristino di emergenza e disponibilità elevata per le applicazioni basate su Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Questo articolo illustra uno scenario reale di ripristino di emergenza, quando in un'intera area si verifica un'interruzione a causa di un grave disastro naturale o di un'interruzione diffusa del servizio. Si tratta di episodi rari, ma è necessario prepararsi alla possibilità che si verifichi un evento del genere. In caso di un'interruzione del servizio che interessa un'intera area, le copie ridondanti locali dei dati non saranno temporaneamente disponibili. Se è stata abilitata la replica geografica, esistono altre tre copie dei BLOB e delle tabelle di Archiviazione di Azure memorizzate in un'area diversa. Nel caso di un'interruzione a livello dell'intera area o di un'emergenza in cui l'area primaria non sia recuperabile, Azure esegue un nuovo mapping di tutte le voci DNS all'area con replica geografica.

> [!NOTE]
> Tenere presente che non è possibile controllare questo processo e che verrà eseguito solo in caso di interruzioni del servizio a livello di area. Per questo motivo, è necessario affidarsi anche ad altre strategie di backup specifiche dell'applicazione per ottenere il massimo livello di disponibilità. Per altre informazioni, vedere la sezione [Strategie dei dati per il ripristino di emergenza](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).
>
>

Per semplificare la gestione di questi rari avvenimenti, di seguito vengono fornite indicazioni per le macchine virtuali di Azure in caso di interruzione del servizio nell'intera area in cui è distribuita la macchina virtuale di Azure.

## <a name="option-1-wait-for-recovery"></a>Opzione 1: Attendere il ripristino
In tal caso, non è necessaria alcuna azione da parte dell'utente. Si sta lavorando per ripristinare la disponibilità dei servizi. È possibile vedere lo stato corrente del servizio nel [dashboard per l'integrità dei servizi di Azure](https://azure.microsoft.com/status/).

> [!NOTE]
> Questa è l'opzione migliore se prima dell'interruzione non è stato impostato Azure Site Recovery, il backup delle macchine virtuali, l'archiviazione con ridondanza geografica o con ridondanza geografica e accesso in lettura. Se è stata impostata l'archiviazione con ridondanza geografica o con ridondanza geografica e accesso in lettura per l'account di archiviazione in cui sono archiviati i dischi rigidi virtuali della VM, è possibile cercare di ripristinare il VHD immagine di base e usarlo per provare a effettuare il provisioning di una nuova VM. Questa non è un'opzione consigliata perché non offre alcuna garanzia di sincronizzazione dei dati, a meno di usare Azure Site Recovery o il backup delle VM di Azure. Di conseguenza, non è certo che questa opzione possa funzionare.
>
>

Per i clienti che vogliono avere accesso immediato alle macchine virtuali, sono disponibili le due opzioni seguenti.  

> [!NOTE]
> Tenere presente che con entrambe le opzioni potrebbe verificarsi una perdita parziale dei dati.     
>
>

## <a name="option-2-restore-a-vm-from-a-backup"></a>Opzione 2: Ripristinare una macchina virtuale da un backup
I clienti che hanno configurato un backup delle VM possono ripristinare la macchina virtuale dal punto di backup e ripristino.

Per ripristinare una nuova macchina virtuale da Backup di Azure, vedere [Ripristinare le macchine virtuali in Azure](../backup/backup-azure-restore-vms.md).

Per pianificare l'infrastruttura di backup delle macchine virtuali di Azure, vedere [Pianificare l'infrastruttura di backup delle macchine virtuali in Azure](../backup/backup-azure-vms-introduction.md).

## <a name="option-3-initiate-a-failover-by-using-azure-site-recovery"></a>Opzione 3: Avviare un failover con Azure Site Recovery
Se è stato configurato Azure Site Recovery per l'uso con le macchine virtuali di Azure colpite dall'interruzione, è possibile ripristinare le VM dalle relative repliche. Le repliche possono risiedere in Azure o in locale. In tal caso, è possibile creare una nuova VM dalla replica esistente. Per ripristinare le VM da una replica di Azure Site Recovery, vedere [Eseguire la migrazione delle macchine virtuali IaaS di Azure tra aree di Azure con Azure Site Recovery](../site-recovery/site-recovery-migrate-azure-to-azure.md).

> [!NOTE]
> Anche se i dischi dati e il sistema operativo della macchina virtuale di Azure vengono replicati in un disco rigido virtuale secondario, se si trovano in un account di archiviazione con ridondanza geografica o con ridondanza geografica e accesso in lettura ogni disco rigido virtuale verrà replicato in modo indipendente. Questo livello di replica non garantisce la coerenza tra i dischi rigidi virtuali replicati. Se l'applicazione e/o i database che usano questi dischi dati presentano dipendenze reciproche, non è garantito che tutti i dischi rigidi virtuali vengano replicati come un unico snapshot. Non c'è alcuna garanzia neanche che la replica di dischi rigidi virtuali dall'archiviazione con ridondanza geografica o con ridondanza geografica e accesso in lettura generi uno snapshot coerente con l'applicazione per l'avvio della macchina virtuale.
>
>

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni su come implementare una strategia di disponibilità elevata e ripristino di emergenza, vedere [Ripristino di emergenza e disponibilità elevata per le applicazioni basate su Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Per sviluppare una conoscenza tecnica approfondita delle funzionalità della piattaforma cloud, vedere [Indicazioni tecniche sulla resilienza di Azure](../resiliency/resiliency-technical-guidance.md).

Per informazioni su come eseguire il backup di macchine virtuali, vedere [Eseguire il backup di macchine virtuali di Azure](../backup/backup-azure-vms.md).

Per informazioni su come usare Azure Site Recovery per orchestrare e automatizzare la protezione di computer e macchine virtuali Windows e Linux in esecuzione in macchine virtuali Hyper-V e VMWare, vedere [Site Recovery](https://azure.microsoft.com/documentation/learning-paths/site-recovery/).

Per chiarimenti sulle istruzioni o per chiedere a Microsoft di eseguire le operazioni per proprio conto, contattare il [supporto tecnico](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

