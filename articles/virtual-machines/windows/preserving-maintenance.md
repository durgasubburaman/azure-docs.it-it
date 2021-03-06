---
title: Manutenzione con mantenimento per macchine virtuali Windows in Azure | Microsoft Docs
description: Migrazione di macchine virtuali sul posto per aggiornamenti con mantenimento della memoria.
services: virtual-machines-windows
documentationcenter: 
author: 
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: 
translationtype: Human Translation
ms.sourcegitcommit: 5cce99eff6ed75636399153a846654f56fb64a68
ms.openlocfilehash: bc903f7523295da704ea8f0128dd553e3fdd96a9
ms.lasthandoff: 03/31/2017


---



# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a>Manutenzione con mantenimento delle macchine virtuali tramite la migrazione delle macchine virtuali sul posto

Sebbene la maggior parte degli aggiornamenti non abbia alcun impatto sulle macchine virtuali ospitate, vi sono casi in cui gli aggiornamenti ai componenti o ai servizi hanno un'interferenza minima sulle macchine virtuali in esecuzione (senza un riavvio completo della macchina virtuale).

Questi aggiornamenti vengono eseguiti con la tecnologia che consente la migrazione sul posto in tempo reale, anche detta aggiornamento con mantenimento della memoria. Durante l'aggiornamento dell'host, la macchina virtuale viene messa in pausa, mantenendo la memoria nella RAM, mentre l'ambiente host, ad esempio il sistema operativo sottostante, applica gli aggiornamenti e le patch necessari.
La macchina virtuale riprende poi l'esecuzione dopo un periodo di pausa di 30 secondi.
Dopo la ripresa, l’orologio della macchina virtuale viene sincronizzato automaticamente.

Non tutti gli aggiornamenti possono essere distribuiti utilizzando questo meccanismo, ma dato il breve periodo di pausa, la distribuzione degli aggiornamenti in questo modo riduce notevolmente l’impatto sulle macchine virtuali.

Gli aggiornamenti a istanza multipla (le macchine virtuali sono in un set di disponibilità) vengono applicati su un dominio di aggiornamento alla volta.

Le applicazioni in esecuzione in una macchina virtuale ricevono le informazioni sugli aggiornamenti futuri chiamando gli eventi pianificati del servizio metadati. Per altre informazioni sugli eventi pianificati, fare riferimento a [Servizio metadati Azure - eventi pianificati](../virtual-machines-scheduled-events.md).
