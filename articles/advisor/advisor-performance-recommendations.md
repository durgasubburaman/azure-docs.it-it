---
title: Consigli di Azure Advisor sulle prestazioni | Microsoft Docs
description: Usare Advisor per ottimizzare le prestazioni delle distribuzioni di Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
translationtype: Human Translation
ms.sourcegitcommit: 197ebd6e37066cb4463d540284ec3f3b074d95e1
ms.openlocfilehash: 5fb86c60b2d1f258dde5636ff8854b6f30f7f1c8
ms.lasthandoff: 03/31/2017

---

# <a name="advisor-performance-recommendations"></a>Consigli di Advisor sulle prestazioni

Grazie ai consigli di Azure Advisor sulle prestazioni, è possibile migliorare e aumentare la velocità e la reattività delle applicazioni aziendali critiche. È possibile ottenere da Advisor consigli sulle prestazioni nella scheda **Prestazioni** scheda del dashboard di Advisor.

![Scheda Prestazioni di Advisor](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a>Migliorare le prestazioni del database con Advisor per database SQL

Advisor fornisce una visualizzazione coerente e consolidata dei consigli per tutte le risorse di Azure. Si integra con Advisor per database SQL per offrire consigli su come migliorare le prestazioni del database SQL di Azure. Advisor per database SQL consente di valutare le prestazioni dei database SQL di Azure analizzando la cronologia relativa all'uso. Offre quindi consigli ideali per l'esecuzione del carico di lavoro tipico del database. 

> [!NOTE]
> Per ottenere consigli, è necessario che un database sia stato in uso per circa una settimana, nel corso della quale deve essersi verificata attività coerente. Advisor per database SQL può essere più facilmente ottimizzato per modelli di query coerenti anziché picchi irregolari casuali di attività.

Per altre informazioni su Advisor per database SQL, vedere [Advisor per database SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).

![Consigli sul database SQL](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a>Migliorare affidabilità e prestazioni di Cache Redis

Advisor identifica le istanze di Cache Redis in cui le prestazioni potrebbero aver subito effetti negativi a causa di uso di memoria, carico del server, larghezza di banda di rete e numero di connessioni client elevati. Advisor fornisce inoltre consigli sulle procedure consigliate che consentono di evitare potenziali problemi. Per altre informazioni relative ai consigli su Cache Redis, vedere [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).


## <a name="improve-app-service-performance-and-reliability"></a>Migliorare affidabilità e prestazioni di Servizi app

Azure Advisor integra consigli sulle procedure consigliate per migliorare l'esperienza di Servizi app e scoprire le funzionalità della piattaforma pertinente. Esempi di consigli per Servizi app sono:
* Rilevamento delle istanze in cui le risorse di CPU o memoria vengono esaurite dai runtime delle app con opzioni di migrazione.
* Rilevamento delle istanze in cui la collocazione delle risorse come App Web e database può aumentare le prestazioni e ridurre il costo. 

Per altre informazioni sui consigli per Servizi app, vedere [Procedure consigliate per Servizio app di Azure](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).
![Consigli per Servizi app](./media/advisor-performance-recommendations/advisor-performance-app-service.png)

## <a name="how-to-access-performance-recommendations-in-advisor"></a>Come accedere ai consigli sulle prestazioni in Advisor

1. Accedere al [portale di Azure](https://portal.azure.com).

2. Nel riquadro sinistro selezionare **Altri servizi**.

3. Nel riquadro del menu del servizio in **Monitoraggio e gestione** fare clic su **Azure Advisor**.  
 Verrà visualizzato il dashboard di Advisor.

4. Nel dashboard di Advisor fare clic sulla scheda **Prestazioni**.

5. Selezionare la sottoscrizione per cui si desidera ricevere consigli e quindi fare clic su **Ottieni raccomandazioni**.

> [!NOTE]
> Per accedere ai consigli di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor. Una sottoscrizione viene registrata quando il *proprietario della sottoscrizione* avvia il dashboard di Advisor e fa clic sul pulsante **Ottieni raccomandazioni**. Si tratta di un'*operazione una tantum*. Dopo aver registrato una sottoscrizione, è possibile accedere ai consigli di Advisor come *Proprietario*, *Collaboratore* o *Lettore* di una sottoscrizione, di un gruppo di risorse o di una risorsa specifica.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui consigli di Advisor, vedere:

* [Introduction to Advisor](advisor-overview.md) (Presentazione di Azure Advisor)
* [Get started with Advisor](advisor-get-started.md) (Introduzione ad Advisor)
* [Advisor Cost recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sui costi)
* [Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)
* [Advisor Security recommendations](advisor-security-recommendations.md) (Consigli di Advisor sulla sicurezza)


