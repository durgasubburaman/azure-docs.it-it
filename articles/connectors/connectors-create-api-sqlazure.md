---
title: Aggiungere il connettore del database SQL di Azure alle app per la logica | Microsoft Docs
description: Panoramica del connettore del database SQL di Azure con i parametri dell&quot;API REST
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia
translationtype: Human Translation
ms.sourcegitcommit: 66fc8f7e1da55dbe6bb1dd8b8d6a535c498c1cf7
ms.openlocfilehash: ce3a622db8667df8b3f1d1391c2aa0d7e1e012a5
ms.lasthandoff: 02/16/2017


---
# <a name="get-started-with-the-azure-sql-database-connector"></a>Introduzione al connettore del database SQL di Azure
Usando il connettore del database SQL di Azure, creare flussi di lavoro per l'organizzazione che gestiscano i dati nelle tabelle. 

Con il database SQL è possibile:

* Creare il flusso di lavoro aggiungendo un nuovo cliente in un database di clienti o aggiornando un ordine in un database di ordini.
* Usare le azioni per ottenere una riga di dati, inserire una nuova riga e persino eliminare una riga. Ad esempio, quando viene creato un record in Dynamics CRM Online (trigger), inserire una riga in un database SQL di Azure (azione). 

Questo argomento illustra come usare il connettore database SQL in un'app per la logica ed elenca le azioni.

> [!NOTE]
> Questa versione dell'articolo si applica alla la disponibilità generale delle app per la logica. 
> 
> 

Per altre informazioni sulle app per la logica, vedere [Cosa sono le app per la logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-to-azure-sql-database"></a>Connettersi al database SQL di Azure
Prima che l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una *connessione* al servizio. Una connessione fornisce la connettività tra un'app per la logica e un altro servizio. Ad esempio, per connettersi al database SQL, si crea una *connessione* al database SQL. Per creare una connessione, immettere le credenziali che si usano normalmente per accedere al servizio a cui connettersi. Pertanto, per creare la connessione al database SQL, immettere le credenziali del database SQL. 

#### <a name="create-the-connection"></a>Creare la connessione
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>Usare un trigger
Questo connettore non include trigger. Usare altri trigger per avviare l'app per la logica, come un trigger di ricorrenza, un trigger Webhook HTTP, i trigger disponibili con altri connettori e altri ancora. [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) illustra un esempio.

## <a name="use-an-action"></a>Usare un'azione
Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica. [Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Selezionare il segno più. Sono disponibili varie opzioni: **Aggiungi un'azione**, **Aggiungi una condizione** e le opzioni in **Altro**.
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. Selezionare **Aggiungi un'azione**.
3. Nella casella di testo digitare "sql" per ottenere l'elenco di tutte le azioni disponibili.
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. Nell'esempio scegliere **SQL Server - Ottieni riga**. Se esiste già una connessione, selezionare il **nome della tabella** dall'elenco a discesa e immettere l'**ID riga** che si vuole restituire.
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    Se viene richiesto di inserire le informazioni di connessione, immettere i dettagli per creare la connessione. La sezione [Creare la connessione](connectors-create-api-sqlazure.md#create-the-connection) di questo argomento descrive queste proprietà. 
   
   > [!NOTE]
   > In questo esempio si restituisce una riga da una tabella. Per visualizzare i dati in questa riga aggiungere un'altra azione che crea un file usando i campi della tabella. Ad esempio, aggiungere un'azione OneDrive che usa i campi Nome e Cognome per creare un nuovo file nell'account di archiviazione cloud. 
   > 
   > 
5. Scegliere **Salva** nell'angolo in alto a sinistra della barra degli strumenti per salvare le modifiche. L'app per la logica viene salvata e può essere attivata automaticamente.

## <a name="technical-details"></a>Dettagli tecnici
## <a name="sql-database-actions"></a>Azioni del database SQL
Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica. Il connettore del database SQL include le azioni seguenti. 

| Azione | Description |
| --- | --- |
| [ExecuteProcedure](connectors-create-api-sqlazure.md#execute-stored-procedure) |Esegue una stored procedure in SQL |
| [GetRow](connectors-create-api-sqlazure.md#get-row) |Recupera una riga singola da una tabella SQL |
| [GetRows](connectors-create-api-sqlazure.md#get-rows) |Recupera righe da una tabella SQL |
| [InsertRow](connectors-create-api-sqlazure.md#insert-row) |Inserisce una nuova riga in una tabella SQL |
| [DeleteRow](connectors-create-api-sqlazure.md#delete-row) |Elimina una riga da una tabella SQL |
| [GetTables](connectors-create-api-sqlazure.md#get-tables) |Recupera le tabelle da un database SQL |
| [UpdateRow](connectors-create-api-sqlazure.md#update-row) |Aggiorna una riga esistente in una tabella SQL |

### <a name="action-details"></a>Informazioni dettagliate sulle azioni
In questa sezione si vedranno i dettagli relativi a ogni azione, incluse le proprietà di input obbligatorie o facoltative e gli output corrispondenti associati al connettore.

#### <a name="execute-stored-procedure"></a>Esegui stored procedure
Esegue una stored procedure in SQL.  

| Nome proprietà | Nome visualizzato | Descrizione |
| --- | --- | --- |
| procedure* |Nome della stored procedure |Il nome della stored procedure da eseguire |
| parameters* |Parametri di input |I parametri sono dinamici e basati sulla stored procedure selezionata. <br/><br/> Ad esempio, se si usa il database di esempio Adventure Works, scegliere la stored procedure *ufnGetCustomerInformation*. Viene visualizzato il parametro di input **ID cliente**. Immettere "6" o uno degli altri ID cliente. |

L'asterisco (*) indica che la proprietà è obbligatoria.

##### <a name="output-details"></a>Dettagli dell'output
ProcedureResult: riporta il risultato dell'esecuzione della stored procedure

| Nome proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| OutputParameters |oggetto |Valori di output dei parametri |
| ReturnCode |integer |Codice restituito di una routine |
| ResultSets |oggetto |Set di risultati |

#### <a name="get-row"></a>Ottenere la riga
Recupera una riga singola da una tabella SQL.  

| Nome proprietà | Nome visualizzato | Descrizione |
| --- | --- | --- |
| table* |Nome tabella |Nome della tabella SQL |
| id* |ID di riga |Identificatore univoco della riga da recuperare |

L'asterisco (*) indica che la proprietà è obbligatoria.

##### <a name="output-details"></a>Dettagli dell'output
Item

| Nome proprietà | Tipo di dati |
| --- | --- |
| ItemInternalId |string |

#### <a name="get-rows"></a>Ottieni righe
Recupera righe da una tabella SQL.  

| Nome proprietà | Nome visualizzato | Descrizione |
| --- | --- | --- |
| table* |Nome tabella |Nome della tabella SQL |
| $skip |Ignora conteggio |Numero di elementi da ignorare (impostazione predefinita = 0) |
| $top |Numero massimo di Get |Numero massimo di elementi da recuperare (impostazione predefinita = 256) |
| $filter |Query di filtro |Query di filtro ODATA per limitare il numero di elementi |
| $orderby |Ordina per |Query orderBy ODATA per specificare l'ordine degli elementi |

L'asterisco (*) indica che la proprietà è obbligatoria.

##### <a name="output-details"></a>Dettagli dell'output
ItemsList

| Nome proprietà | Tipo di dati |
| --- | --- |
| value |array |

#### <a name="insert-row"></a>Inserisci riga
Inserisce una nuova riga in una tabella SQL.  

| Nome proprietà | Nome visualizzato | Descrizione |
| --- | --- | --- |
| table* |Nome tabella |Nome della tabella SQL |
| item* |Riga |Riga da inserire nella tabella specificata in SQL |

L'asterisco (*) indica che la proprietà è obbligatoria.

##### <a name="output-details"></a>Dettagli dell'output
Item

| Nome proprietà | Tipo di dati |
| --- | --- |
| ItemInternalId |string |

#### <a name="delete-row"></a>Elimina riga
Elimina una riga da una tabella SQL.  

| Nome proprietà | Nome visualizzato | Descrizione |
| --- | --- | --- |
| table* |Nome tabella |Nome della tabella SQL |
| id* |ID di riga |Identificatore univoco della riga da eliminare |

L'asterisco (*) indica che la proprietà è obbligatoria.

##### <a name="output-details"></a>Dettagli dell'output
Nessuna.

#### <a name="get-tables"></a>Ottieni tabelle
Recupera le tabelle da un database SQL.  

Non sono disponibili parametri per questa chiamata. 

##### <a name="output-details"></a>Dettagli dell'output
TablesList

| Nome proprietà | Tipo di dati |
| --- | --- |
| value |array |

#### <a name="update-row"></a>Aggiorna riga
Aggiorna una riga esistente in una tabella SQL.  

| Nome proprietà | Nome visualizzato | Descrizione |
| --- | --- | --- |
| table* |Nome tabella |Nome della tabella SQL |
| id* |ID di riga |Identificatore univoco della riga da aggiornare |
| item* |Riga |Riga con i valori aggiornati |

L'asterisco (*) indica che la proprietà è obbligatoria.

##### <a name="output-details"></a>Dettagli dell'output
Item

| Nome proprietà | Tipo di dati |
| --- | --- |
| ItemInternalId |string |

### <a name="http-responses"></a>Risposte HTTP
Quando si effettuano chiamate alle diverse azioni, è possibile ottenere determinate risposte. La tabella seguente indica le risposte e le relative descrizioni:  

| Nome | Descrizione |
| --- | --- |
| 200 |OK |
| 202 |Accepted |
| 400 |Bad Request |
| 401 |Non autorizzata |
| 403 |Accesso negato |
| 404 |Non trovato |
| 500 |Errore interno del server. Si è verificato un errore sconosciuto |
| default |Operazione non riuscita. |

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md). Esplorare gli altri connettori disponibili nelle app per la logica nell' [elenco delle API](apis-list.md).


