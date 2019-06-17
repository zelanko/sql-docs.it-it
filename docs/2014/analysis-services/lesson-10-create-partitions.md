---
title: 'Lezione 11: Creare partizioni | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06ffe60802e52bd0ae141435628fc3812dc2c7c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079197"
---
# <a name="lesson-11-create-partitions"></a>Lezione 11: Creare partizioni
  In questa lezione verranno create partizioni per dividere la tabella Internet Sales in parti logiche più piccole, che possono essere elaborate (aggiornate) indipendentemente dalle altre partizioni. Per impostazione predefinita, ogni tabella a che inclusa nel modello dispone di una partizione che include tutte le colonne e le righe della tabella. Per la tabella Internet Sales, si desidera dividere i dati per anno. una partizione per ognuno dei cinque anni della tabella.  Ogni partizione può quindi essere elaborata in modo indipendente. Per altre informazioni, vedere [Partizioni &#40;SSAS tabulare&#41;](tabular-models/partitions-ssas-tabular.md).  
  
 Tempo stimato per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 10: Creare gerarchie](lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Creare partizioni  
  
#### <a name="to-create-partitions-in-the-internet-sales-table"></a>Per creare partizioni nella tabella Internet Sales  
  
1.  In Progettazione modelli fare clic sulla tabella **Internet Sales** , quindi scegliere **Partizioni** dal menu **Tabella**.  
  
     Verrà visualizzata la finestra di dialogo **Gestione partizioni** .  
  
2.  Nel **gestione partizioni** nella finestra di dialogo **partizioni**, fare clic sui **Internet Sales** partizione.  
  
3.  Nelle **nome partizione**, denominarlo `Internet Sales 2005`.  
  
    > [!TIP]  
    >  Prima di continuare con il passaggio successivo, osservare che per i nomi di colonna nella finestra Anteprima tabella vengono visualizzate le colonne incluse nella tabella del modello (selezionate) con i nomi di colonna dell'origine. Questo si verifica in quanto nella finestra Anteprima tabella vengono visualizzate le colonne della tabella di origine, non quelle della tabella del modello.  
  
4.  Fare clic sul pulsante **Editor di query** nella parte superiore destra della finestra di anteprima.  
  
     Poiché si desidera che la partizione includa solo le righe comprese in un determinato periodo, è necessario includere una clausola WHERE. È possibile creare una clausola WHERE solo tramite un'istruzione SQL.  
  
5.  Nel campo **Istruzione SQL** sostituire l'istruzione esistente incollando l'istruzione seguente:  
  
    ```  
    SELECT   
    [dbo].[FactInternetSales].[ProductKey],  
    [dbo].[FactInternetSales].[CustomerKey],  
    [dbo].[FactInternetSales].[PromotionKey],  
    [dbo].[FactInternetSales].[CurrencyKey],  
    [dbo].[FactInternetSales].[SalesTerritoryKey],  
    [dbo].[FactInternetSales].[SalesOrderNumber],  
    [dbo].[FactInternetSales].[SalesOrderLineNumber],  
    [dbo].[FactInternetSales].[RevisionNumber],  
    [dbo].[FactInternetSales].[OrderQuantity],  
    [dbo].[FactInternetSales].[UnitPrice],  
    [dbo].[FactInternetSales].[ExtendedAmount],  
    [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
    [dbo].[FactInternetSales].[DiscountAmount],  
    [dbo].[FactInternetSales].[ProductStandardCost],  
    [dbo].[FactInternetSales].[TotalProductCost],  
    [dbo].[FactInternetSales].[SalesAmount],  
    [dbo].[FactInternetSales].[TaxAmt],  
    [dbo].[FactInternetSales].[Freight],  
    [dbo].[FactInternetSales].[CarrierTrackingNumber],  
    [dbo].[FactInternetSales].[CustomerPONumber],  
    [dbo].[FactInternetSales].[OrderDate],  
    [dbo].[FactInternetSales].[DueDate],  
    [dbo].[FactInternetSales].[ShipDate]   
    FROM [dbo].[FactInternetSales]  
    WHERE (([OrderDate] >= N'2005-01-01 00:00:00') AND ([OrderDate] < N'2006-01-01 00:00:00'))  
    ```  
  
     Questa istruzione specifica che la partizione deve includere tutti i dati delle righe in cui OrderDate si riferisce all'anno di calendario 2005, come specificato nella clausola WHERE.  
  
6.  Fare clic su **Convalida**.  
  
     Si noti che viene visualizzato un avviso che indica che alcune colonne non sono presenti nell'origine. Infatti, in [lezione 3: Rinominare le colonne](rename-columns.md), si rinominate le colonne nella tabella Internet Sales nel modello può essere diverso alle stesse colonne nell'origine.  
  
#### <a name="to-create-a-partition-for-the-2006-year-in-the-internet-sales-table"></a>Per creare una partizione per l'anno 2006 nella tabella Internet Sales  
  
1.  Nel **gestione partizioni** nella finestra di dialogo **partizioni**, fare clic sui `Internet Sales 2005` partizione appena creata, e quindi **copia**.  
  
2.  Nelle **nome partizione**, tipo `Internet Sales 2006`.  
  
3.  Nell'istruzione SQL, affinché nella partizione siano incluse solo le righe per l'anno 2006, sostituire la clausola WHERE con gli elementi seguenti:  
  
    ```  
    WHERE (([OrderDate] >= N'2006-01-01 00:00:00') AND ([OrderDate] < N'2007-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2007-year-in-the-internet-sales-table"></a>Per creare una partizione per l'anno 2007 nella tabella Internet Sales  
  
1.  Nella finestra di dialogo **Gestione partizioni** fare clic su **Copia**.  
  
2.  Nelle **nome partizione**, tipo `Internet Sales 2007`.  
  
3.  Nelle **passa a**, selezionare **Editor di Query**.  
  
4.  Nell'istruzione SQL, affinché nella partizione siano incluse solo le righe per l'anno 2007, sostituire la clausola WHERE con gli elementi seguenti:  
  
    ```  
    WHERE (([OrderDate] >= N'2007-01-01 00:00:00') AND ([OrderDate] < N'2008-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2008-year-in-the-internet-sales-table"></a>Per creare una partizione per l'anno 2008 nella tabella Internet Sales  
  
1.  Nella finestra di dialogo **Gestione partizioni** fare clic su **Nuova**.  
  
2.  Nelle **nome partizione**, tipo `Internet Sales 2008`.  
  
3.  Nelle **passa a**, selezionare **Editor di Query**.  
  
4.  Nell'istruzione SQL, affinché nella partizione siano incluse solo le righe per l'anno di 2008, sostituire la clausola WHERE con gli elementi seguenti:  
  
    ```  
    WHERE (([OrderDate] >= N'2008-01-01 00:00:00') AND ([OrderDate] < N'2009-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2009-year-in-the-internet-sales-table"></a>Per creare una partizione per l'anno 2009 nella tabella Internet Sales  
  
1.  Nella finestra di dialogo **Gestione partizioni** fare clic su **Nuova**.  
  
2.  Nelle **nome partizione**, tipo `Internet Sales 2009`.  
  
3.  Nelle **passa a**, selezionare **Editor di Query**.  
  
4.  Nell'istruzione SQL, affinché nella partizione siano incluse solo le righe per l'anno 2009, sostituire la clausola WHERE con la seguente:  
  
    ```  
    WHERE (([OrderDate] >= N'2009-01-01 00:00:00') AND ([OrderDate] < N'2010-01-01 00:00:00'))  
    ```  
  
## <a name="process-partitions"></a>Elaborare le partizioni  
 Nella finestra di dialogo **Gestione partizioni** , notare l'asterisco ( **\*** ) accanto ai nomi di partizione per ognuna delle nuove partizioni appena create. L'asterisco indica che la partizione non è stata elaborata (aggiornata). Quando si creano nuove partizioni, è necessario eseguire un'operazione di elaborazione delle partizioni o della tabella per aggiornare i dati nelle partizioni.  
  
#### <a name="to-process-internet-sales-partitions"></a>Per elaborare le partizioni di Internet Sales  
  
1.  Fare clic su **OK** per chiudere la finestra di dialogo **Gestione partizioni** .  
  
2.  In Progettazione modelli fare clic sulla tabella **Internet Sales** , scegliere **Elabora** (Aggiorna) nel menu **Modello** , quindi fare clic su **Elabora partizioni**.  
  
3.  Nella finestra di dialogo **Elabora partizioni** verificare che l'opzione **Modalità** sia impostata su **Elaborazione predefinita**.  
  
4.  Selezionare la casella di controllo **Elabora** per ognuna delle cinque partizioni create, quindi fare clic su **OK**.  
  
     Se vengono richieste le credenziali di rappresentazione, immettere il nome utente e la password di Windows specificati al passaggio 6 della lezione 2.  
  
     Il **processo di Data** quindi nella finestra di dialogo viene visualizzata e consente di visualizzare i dettagli dei processi per ogni partizione. Si noti che per ogni partizione viene trasferito un numero diverso di righe. Questo avviene in quanto ogni partizione include solo le righe per l'anno specificato nella clausola WHERE dell'istruzione SQL. Non vi sono dati per l'anno 2010.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per continuare questa esercitazione, passare alla lezione successiva: Lezione: [Lezione 12: Creare ruoli](lesson-11-create-roles.md).  
  
  
