---
title: "Esempio di script dell&quot;interfaccia della riga di comando di Azure - Ridimensionare un&quot;App Web a livello globale con un&quot;architettura a disponibilità elevata | Microsoft Docs"
description: "Esempio di script dell&quot;interfaccia della riga di comando di Azure - Ridimensionare un&quot;App Web a livello globale con un&quot;architettura a disponibilità elevata"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.translationtype: Human Translation
ms.sourcegitcommit: 9568210d4df6cfcf5b89ba8154a11ad9322fa9cc
ms.openlocfilehash: 5c467f35351a9e0c6261967b6ed6e6b58cfab682
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---

# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a>Ridimensionare un'App Web a livello globale con un'architettura a disponibilità elevata

In questo scenario verranno creati un gruppo di risorse, due piani di servizio app, due App Web, una profilo di Gestione traffico e due endpoint di endpoint di Gestione traffico. Dopo aver completato l'esercizio si avrà un'architettura a disponibilità elevata che fornisce la disponibilità globale dell'App Web in base alla minima latenza di rete.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Scalabilità geografica")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Spiegazione dello script

Questo script usa i comandi seguenti per creare un gruppo di risorse, un'App Web, un profilo di Gestione traffico e tutte le risorse correlate. Ogni comando della tabella include collegamenti alla documentazione specifica del comando.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Consente di creare un piano di servizio app. Equivale a una server farm per l'App Web di Azure. |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#create) | Consente di creare un'App Web di Azure all'interno del piano di servizio app. |
| [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Crea un profilo di Gestione traffico di Azure. |
| [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | Aggiunge un endpoint a un profilo di Gestione traffico di Azure. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).

Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).

