---
title: Elemento MultiStorageAccountCombo dell&quot;interfaccia utente di Applicazione gestita di Azure | Microsoft Docs
description: Illustra l&quot;elemento Microsoft.Storage.MultiStorageAccountCombo dell&quot;interfaccia utente per le applicazioni gestite di Azure
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.translationtype: Human Translation
ms.sourcegitcommit: afa23b1395b8275e72048bd47fffcf38f9dcd334
ms.openlocfilehash: 27843b116d949899e4eae65f342324f77ebca70b
ms.contentlocale: it-it
ms.lasthandoff: 05/12/2017


---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a>Elemento Microsoft.Storage.MultiStorageAccountCombo dell'interfaccia utente
Gruppo di controlli per la creazione di più account di archiviazione, con nomi che iniziano con un prefisso comune. Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).

## <a name="ui-sample"></a>Esempio di interfaccia utente
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a>Schema
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Osservazioni
- Il valore per `defaultValue.prefix` viene concatenato a uno o più numeri interi per generare la sequenza di nomi di account di archiviazione. Se ad esempio `defaultValue.prefix` è **foobar** e `count` è **2**, vengono generati i nomi degli account di archiviazione **foobar1** e **foobar2**. L'unicità dei nomi degli account di archiviazione generati viene convalidata automaticamente.
- I nomi degli account di archiviazione vengono generati in modo lessicografico in base a `count`. Se ad esempio `count` è 10, i nomi degli account di archiviazione terminano con numeri interi a 2 cifre (01, 02, 03 e così via).
- Il valore predefinito per `defaultValue.prefix` è **null** e quello per `defaultValue.type` è **Premium_LRS**.
- I tipi non specificati in `constraints.allowedTypes` vengono nascosti e i tipi non specificati in `constraints.excludedTypes` vengono visualizzati.
`constraints.allowedTypes` e `constraints.excludedTypes` sono entrambi facoltativi, ma non possono essere usati contemporaneamente.
- Oltre a generare nomi di account di archiviazione, `count` viene usato per impostare il moltiplicatore appropriato per l'elemento. Supporta un valore statico, ad esempio **2**, o un valore dinamico da un altro elemento, ad esempio `[steps('step1').storageAccountCount]`. Il valore predefinito è **1**.

## <a name="sample-output"></a>Output di esempio
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a>Passaggi successivi
* Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).
* Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).

