---
title: Installare o aggiornare Mono in HDInsight | Microsoft Docs
description: Informazioni su come usare una versione specifica di Mono con cluster HDInsight. Mono viene usato per eseguire applicazioni .NET in cluster HDInsight basati su Linux.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 64bd7f356673b385581c8060b17cba721d0cf8e3
ms.openlocfilehash: dc303b5386d48cd7daad1630a35c8b8366a9c19f
ms.contentlocale: it-it
ms.lasthandoff: 05/02/2017


---

# <a name="install-or-update-mono-on-hdinsight"></a>Installare o aggiornare Mono in HDInsight

Informazioni su come installare una versione specifica di [Mono](https://www.mono-project.com) in HDInsight 3.4 o versione successiva.

Mono viene installato in HDInsight 3.4 e versioni successive per eseguire applicazioni .NET. Per informazioni sulla versione di Mono inclusa in ogni versione di HDInsight, vedere [Componenti e versioni di Hadoop disponibili in HDInsight](hdinsight-component-versioning.md). Per installare una versione diversa nel cluster, usare l'azione di script presente in questo documento. 

## <a name="how-it-works"></a>Funzionamento

Questo script accetta il parametro seguente:

* __Numero di versione di Mono__: versione di Mono da installare. La versione deve essere disponibile sul sito Web all'indirizzo [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).

Lo script installa i pacchetti Mono seguenti:

* __mono-complete__

* __ca-certificates-mono__

## <a name="the-script"></a>Lo script

__Percorso dello script__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)

__Requisiti__:

* Lo script deve essere applicato a di __nodi head__ e ai __nodi del ruolo di lavoro__.

## <a name="to-use-the-script"></a>Per usare lo script

Per informazioni su come usare questo script con HDInsight, vedere il documento [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster). È possibile usare lo script tramite il portale di Azure, Azure PowerShell o l'interfaccia della riga di comando di Azure.

Quando si segue il documento di azione di script, usare l'URI seguente:

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> Durante la configurazione di HDInsight con lo script, contrassegnare quest'ultimo con l'opzione __Con salvataggio permanente__. Questa impostazione consente a HDInsight di applicare lo script ai nodi del ruolo di lavoro aggiunti tramite operazioni di ridimensionamento.


## <a name="next-steps"></a>Passaggi successivi

Si è appreso come aggiornare o installare una versione specifica di Mono in HDInsight. Per altre informazioni sull'uso di applicazioni .NET con Mono in HDInsight, vedere i documenti seguenti:

* [Usare C# con lo streaming di MapReduce su Hadoop in HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [Sviluppare topologie C# per Apache Storm in HDInsight tramite gli strumenti Hadoop per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Eseguire la migrazione di soluzioni .NET per HDInsight basato su Windows a HDInsight basato su Linux](hdinsight-hadoop-migrate-dotnet-to-linux.md)

Per altre informazioni sulle azioni di script, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md)
