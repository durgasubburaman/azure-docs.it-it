---
title: Eseguire il debug di Analisi di flusso di Azure con i ricevitori dell&quot;hub eventi | Documentazione Microsoft
description: Procedure consigliate di query per considerare i gruppi di consumer dell&quot;hub eventi nei processi di Analisi di flusso.
keywords: limite dell&quot;hub eventi, gruppo di consumer
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.translationtype: Human Translation
ms.sourcegitcommit: 7f8b63c22a3f5a6916264acd22a80649ac7cd12f
ms.openlocfilehash: 3724b9077b04c767d0b1679caffed2bc5d077113
ms.contentlocale: it-it
ms.lasthandoff: 05/01/2017


---

# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>Eseguire il debug di Analisi di flusso di Azure con i ricevitori dell'hub eventi

È possibile usare gli hub eventi di Analisi di flusso di Azure per inserire o estrarre dati da un processo. Una procedura consigliata per l'utilizzo dell'hub eventi è usare più gruppi di consumer in modo da garantire la scalabilità del processo. Uno dei motivi è che il numero di lettori del processo di Analisi di flusso per uno specifico input influisce sul numero dei lettori di un singolo gruppo di consumer. Il numero preciso di ricevitori si basa sui dettagli di implementazione interna per la logica della topologia con scalabilità orizzontale. Il numero di ricevitori non viene esposto esternamente. Il numero di lettori può cambiare al momento di inizio del processo o durante gli aggiornamenti del processo.

> [!NOTE]
> Quando il numero di lettori cambia durante un aggiornamento del processo, vengono scritti avvisi temporanei nei log di controllo. I processi di Analisi di flusso vengono ripristinati automaticamente da questi problemi temporanei.

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>Il numero di lettori per partizione supera il limite di cinque hub eventi

Gli scenari in cui il numero di lettori per ogni partizione supera il limite di cinque hub eventi comprendono i seguenti:

* Più istruzioni SELECT: se si usano più istruzioni SELECT che fanno riferimento allo **stesso** input dell'hub eventi, ogni istruzione SELECT fa sì che venga creato un nuovo ricevitore.
* UNION: quando si usa UNION, è possibile avere più input che si riferiscono allo **stesso** hub eventi e gruppo di consumer.
* SELF JOIN: quando si usa un'operazione SELF JOIN è possibile fare riferimento allo **stesso** hub eventi più volte.

## <a name="solution"></a>Soluzione

Le procedure consigliate seguenti possono aiutare a mitigare gli scenari in cui il numero di lettori per ogni partizione supera il limite di cinque hub eventi.

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>Suddividere la query in più passaggi usando una clausola WITH

La clausola WITH specifica un set di risultati con nome temporaneo a cui è possibile fare riferimento mediante una clausola FROM nella query. La clausola WITH viene definita nell'ambito di esecuzione di una singola istruzione SELECT.

Ad esempio, invece di questa query:

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

Usare questa query:

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-to-different-consumer-groups"></a>Assicurarsi che gli input siano associati a gruppi di consumer diversi

Per le query in cui tre o più input sono connessi allo stesso gruppo di consumer di hub eventi, creare gruppi di consumer separati. Ciò richiede la creazione di input di Analisi di flusso aggiuntivi.


## <a name="get-help"></a>Ottenere aiuto
Per ottenere assistenza, provare ad accedere al [forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
* [Presentazione di Analisi di flusso](stream-analytics-introduction.md)
* [Introduzione ad Analisi di flusso](stream-analytics-get-started.md)
* [Scalabilità dei processi di Analisi di flusso](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sull'API REST di gestione di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn835031.aspx)

