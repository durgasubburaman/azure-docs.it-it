---
title: Esempio di script di Azure PowerShell - Creare un&quot;app Web con distribuzione continua da GitHub | Microsoft Docs
description: Esempio di script di Azure PowerShell - Creare un&quot;app Web con distribuzione continua da GitHub
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.translationtype: Human Translation
ms.sourcegitcommit: aaf97d26c982c1592230096588e0b0c3ee516a73
ms.openlocfilehash: c371833219426fbc4a0fd8aaa798a8b44e67672b
ms.contentlocale: it-it
ms.lasthandoff: 04/27/2017

---

# <a name="create-a-web-app-with-continuous-deployment-from-github"></a>Creare un'App Web con distribuzione continua da GitHub

Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi configura la distribuzione continua da un archivio GitHub. Per la distribuzione GitHub senza distribuzione continua, vedere [Creare un'App Web e distribuire il codice da GitHub](app-service-powershell-deploy-github.md).

Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview). Verificare inoltre se:

- È stata creata una connessione con Azure usando il comando `az login`.
- Il codice dell'applicazione è in un archivio GitHub pubblico o privato di cui si è proprietari.
- È stato [creato un token di accesso nell'account GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Creare un'App Web con distribuzione continua da GitHub")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script usa i comandi seguenti. Ogni comando della tabella include collegamenti alla documentazione specifica del comando.

| Comando | Note |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Consente di creare un piano di servizio app. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Crea un'App Web. |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/set-azurermresource) | Modificare una risorsa in un gruppo di risorse. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).

Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).

