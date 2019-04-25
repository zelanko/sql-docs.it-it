---
title: 'Analysis Services tutorial-lezione 10: Creare partizioni | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 91b0fb17ae785098e54358132daa91c04c7f3e5d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62466245"
---
# <a name="create-partitions"></a>Creare partizioni

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione è creare partizioni per dividere la tabella FactInternetSales in parti logiche più piccole che possono essere elaborate (aggiornate) indipendentemente dalle altre. Per impostazione predefinita, ogni tabella a che inclusa nel modello dispone di una partizione, che include le colonne e righe della tabella. Per la tabella FactInternetSales, si desidera dividere i dati per anno. una partizione per ognuno dei cinque anni della tabella. Ogni partizione può quindi essere elaborata in modo indipendente. Per altre informazioni, vedere [Tabella](../tabular-models/partitions-ssas-tabular.md). 
  
Tempo stimato per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  

Questo articolo fa parte di un'esercitazione di modellazione tabulare, che deve essere completata nell'ordine. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 9: Creare gerarchie](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Creare partizioni  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>Per creare partizioni nella tabella FactInternetSales  
  
1.  In Esplora modelli tabulari, espandere **tabelle**e quindi fare doppio clic su **FactInternetSales** > **partizioni**.  
  
2.  Fare clic in Gestione partizioni **copia**e quindi denominarlo **FactInternetSales2010**.
  
    Poiché si vuole che la partizione includa solo le righe all'interno di un determinato periodo, per l'anno 2010, è necessario modificare l'espressione di query.
  
4.  Fare clic su **Design** per aprire l'Editor di Query e quindi fare clic sui **FactInternetSales2010** query.

5.  In fase di anteprima, fare clic sulla freccia verso il basso nel **OrderDate** sull'intestazione di colonna e quindi fare clic su **filtri data/ora** > **tra**.

    ![as-lesson10-query-editor](../tutorial-tabular-1400/media/as-lesson10-query-editor.png)

6.  Nella finestra di dialogo Filtra righe in **Mostra righe in cui: OrderDate**, lasciare **è dopo o uguale a**, quindi nel campo della data, immettere **1/1/2010**. Lasciare il **e** operatore selezionato, quindi selezionare **prima**, immettere nel campo della data **1/1/2011**, quindi fare clic su **OK**.

    ![as-lesson10-filter-rows](../tutorial-tabular-1400/media/as-lesson10-filter-rows.png)
    
    Si noti che nell'Editor di Query, in passaggi applicati, viene visualizzato un altro passaggio denominato filtrate righe. Questo filtro consiste nel selezionare solo le date degli ordini dal 2010.

8.  Fare clic su **Importa**.

    In Gestione partizioni si noti che l'espressione di query a questo punto ha una clausola filtrate righe aggiuntiva.

    ![as-lesson10-query](../tutorial-tabular-1400/media/as-lesson10-query.png)
  
    Questa istruzione specifica che la partizione deve includere solo i dati delle righe in cui OrderDate rientra nell'anno di calendario 2010 come specificato nella clausola filtrate righe.  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>Per creare una partizione per l'anno 2011  
  
1.  Nell'elenco delle partizioni, scegliere il **FactInternetSales2010** partizionare creato e quindi fare clic su **copia**.  Modificare il nome della partizione per **FactInternetSales2011**. 

    Non devi usare l'Editor di Query per creare una nuova clausola righe filtrate. Poiché una copia della query è stato creato per 2010, è sufficiente eseguire è apportare una piccola modifica nella query per 2011.
  
2.  Nelle **espressione di Query**in modo che per questa partizione includa solo le righe per l'anno 2011, sostituire gli anni nella clausola filtrate righe con **2011** e **2012**, rispettivamente come:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a>Per creare partizioni per 2012, 2013 e 2014.  
  
- Seguire i passaggi precedenti, la creazione di partizioni per 2012, 2013 e 2014, modificando gli anni nella clausola filtrate righe siano incluse solo le righe per tale anno. 
  

## <a name="delete-the-factinternetsales-partition"></a>Eliminare la partizione FactInternetSales

Dopo aver creato le partizioni per ogni anno, è possibile eliminare la partizione FactInternetSales; evitare sovrapposizioni quando si sceglie elabora tutti gli quando si elaborano partizioni.

#### <a name="to-delete-the-factinternetsales-partition"></a>Per eliminare la partizione FactInternetSales

-  Scegliere il **FactInternetSales** partizionare e quindi fare clic su **eliminare**.



## <a name="process-partitions"></a>Elaborare le partizioni  

Si noti che in Gestione partizioni, il **ultima elaborazione** colonna per ogni nuova partizione creata mostra queste partizioni non sono mai state elaborate. Quando si creano partizioni, è consigliabile eseguire un'operazione elabora partizioni o elabora tabella per aggiornare i dati in tali partizioni.  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>Per elaborare le partizioni FactInternetSales  
  
1.  Fare clic su **OK** per chiudere Gestione partizioni.  
  
2.  Fare clic sul **FactInternetSales** , quindi scegliere il **modello** menu > **processo** > **elabora partizioni**.  
  
3.  Nella finestra di dialogo Elabora partizioni verificare **modalità** è impostata su **elaborazione predefinita**.  
  
4.  Selezionare la casella di controllo **Elabora** per ognuna delle cinque partizioni create, quindi fare clic su **OK**.  

    ![as-lesson10-process-partitions](../tutorial-tabular-1400/media/as-lesson10-process-partitions.png)
  
    Se viene chiesto di immettere le credenziali di rappresentazione, immettere il nome utente di Windows e la password specificati nella lezione 2.  
  
    Viene visualizzata la finestra di dialogo **Processo dati** , con informazioni dettagliate sul processo per ogni partizione. Si noti che per ogni partizione viene trasferito un numero diverso di righe. Ogni partizione include solo le righe per l'anno specificato nella clausola WHERE nell'istruzione SQL. Al termine dell'elaborazione, proseguire e chiudere la finestra di dialogo Processo dati.  
  
    ![as-lesson10-process-complete](../tutorial-tabular-1400/media/as-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>Quali sono le operazioni successive?

Passare alla lezione successiva: [Lezione 11: Creare ruoli](../tutorial-tabular-1400/as-lesson-11-create-roles.md). 
