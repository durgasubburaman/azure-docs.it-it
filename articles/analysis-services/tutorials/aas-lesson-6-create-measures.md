---
title: 'Esercitazione su Azure Analysis Services - Lezione 6: Creare misure | Microsoft Docs'
description: Descrive come creare misure nel progetto per l&quot;esercitazione su Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/02/2017
ms.author: owend
ms.translationtype: Human Translation
ms.sourcegitcommit: e72275ffc91559a30720a2b125fbd3d7703484f0
ms.openlocfilehash: c4977758997c91f0191e0367fb57923f43080b56
ms.contentlocale: it-it
ms.lasthandoff: 05/05/2017

---
# <a name="lesson-6-create-measures"></a>Lezione 6: Creare misure
In questa lezione verranno create le misure da includere nel modello. In modo simile alle colonne calcolate create, una misura è un calcolo creato usando una formula DAX. Tuttavia, a differenza delle colonne calcolate, le misure vengono valutate in base a un *filtro* selezionato dall'utente, ad esempio, una particolare colonna o filtro dei dati aggiunto al campo Etichette di riga in una tabella pivot. Con la misura applicata viene quindi calcolato un valore per ogni cella nel filtro. Le misure sono calcoli potenti e flessibili che sarà utile includere in quasi tutti i modelli tabulari per eseguire calcoli dinamici su dati numerici. Per altre informazioni, vedere [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular) (Misure).
  
Per creare le misure si usa la *griglia delle misure*. Per impostazione predefinita, ogni tabella ha una griglia delle misure vuota, ma di solito non si creano misure per ogni tabella. La griglia delle misure viene visualizzata sotto una tabella nella finestra di progettazione dei modelli in vista dati. Per mostrare o nascondere la griglia delle misure per una tabella, fare clic sul menu **Tabella** e quindi fare clic su **Mostra griglia delle misure**.  
  
È possibile creare una misura facendo clic su una cella vuota nella griglia delle misure e quindi digitando una formula DAX nella barra della formula. Quando si preme INVIO per completare la formula, la misura verrà quindi visualizzata nella cella. È anche possibile creare misure con una funzione di aggregazione standard facendo clic su una colonna e quindi sul pulsante Somma automatica (**∑**) sulla barra degli strumenti. Le misure create con la funzionalità Somma automatica verranno visualizzate nella cella della griglia delle misure direttamente sotto la colonna, ma possono essere spostate.  
  
In questa lezione le misure vengono create sia immettendo una formula DAX nella barra della formula che usando la funzionalità Somma automatica.  
  
Tempo previsto per il completamento della lezione: **30 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 5: Creare colonne calcolate](../tutorials/aas-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Creare misure  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>Per creare una misura DaysCurrentQuarterToDate nella tabella DimDate  
  
1.  Nella finestra di progettazione dei modelli fare clic sula tabella **DimDate**.  
  
2.  Nella griglia delle misure fare clic sulla cella vuota in alto a sinistra.  
  
3.  Nella barra della formula digitare la formula seguente:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Si noti che la cella in alto a sinistra contiene ora un nome di misura, **DaysCurrentQuarterToDate**, seguito dal risultato, **92**.
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    Diversamente dalle colonne calcolate, con le formule per le misure è possibile digitare il nome della misura, seguito da una virgola, seguita dall'espressione della formula.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>Per creare una misura DaysInCurrentQuarter nella tabella DimDate  
  
1.  Con la tabella **DimDate** ancora attiva nella finestra di progettazione dei modelli, nella griglia delle misure fare clic sulla cella vuota sotto la misura appena creata.  
  
2.  Nella barra della formula digitare la formula seguente:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Quando si crea un rapporto di confronto tra un periodo incompleto e il periodo precedente, la formula deve tenere conto della proporzione del periodo trascorso e confrontarla con la stessa proporzione del periodo precedente. In questo caso, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] restituisce la proporzione per il periodo corrente.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>Per creare una misura InternetDistinctCountSalesOrder nella tabella FactInternetSales  
  
1.  Fare clic sulla tabella **FactInternetSales**.   
  
2.  Fare clic sull'intestazione di colonna **SalesOrderNumber**.  
  
3.  Sulla barra degli strumenti fare clic sulla freccia in giù accanto a Somma automatica (**∑**) e quindi selezionare **DistinctCount**.  
  
    La funzionalità Somma automatica crea automaticamente una misura per la colonna selezionata usando la formula di aggregazione standard DistinctCount.  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  Nella griglia delle misure fare clic sulla nuova misura e quindi nella finestra **Proprietà**, in **Nome misura**, rinominare la misura in **InternetDistinctCountSalesOrder**. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>Per creare altre misure nella tabella FactInternetSales  
  
1.  Usare la funzionalità Somma automatica e creare le misure seguenti con i nomi indicati:  

    |Colonna|Nome misura|Somma automatica (∑)|Formula|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Numero|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|Somma|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|Somma|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|Somma|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|Somma|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|Somma|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|Somma|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|Somma|=SUM([Freight])|  
  
2.  Facendo clic su una cella vuota nella griglia delle misure e quindi usando la barra della formula creare le misure seguenti con il nome indicato in ordine:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Le misure create per la tabella FactInternetSales possono essere usate per analizzare dati finanziari importanti, ad esempio vendite, costi e margine di profitto per gli elementi definiti dal filtro selezionato dall'utente.  
  
## <a name="whats-next"></a>Passaggi successivi
[Lezione 7: Creare indicatori di prestazioni chiave](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  

  

