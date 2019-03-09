---
title: 'Analysis Services tutorial-lezione 2: Ottenere i dati | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 01bf31c3d4f89b77ebdceae2e69d4054a578b03f
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685318"
---
# <a name="get-data"></a>Recuperare i dati

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione, Usa **recupera dati** per connettersi al database di esempio AdventureWorksDW, selezionare i dati, anteprima e filtro e quindi importarli nell'area di lavoro modello.  
  
Dietro le quinte, recupera dati è Power Query, che fornisce una vasta gamma di strumenti per la connessione a e modificare la forma dei dati per la modellazione e l'analisi. Per altre informazioni, vedere [documentazione di Power Query](https://docs.microsoft.com/power-query/). 

> [!NOTE]
> Attività e le immagini in questa esercitazione mostrano la connessione a un database AdventureWorksDW2014 in un server locale. In alcuni casi, un database AdventureWorksDW in Azure SQL Data Warehouse potrebbe mostrare oggetti diversi. Tuttavia, sono sostanzialmente uguali.
  
Tempo stimato per il completamento della lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  

Questo articolo fa parte di un'esercitazione di modellazione tabulare, che deve essere completata nell'ordine. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 1: Creare un nuovo progetto di modello tabulare](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Creare una connessione  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw-database"></a>Per creare una connessione al database AdventureWorksDW  
  
1.  Nelle **Esplora modelli tabulari**, fare doppio clic su **Zdroje dat** > **Importa da origine dati**.  
  
    Verrà avviata **recupera dati**, che illustra la connessione a un'origine dati. Se non viene visualizzato Esplora modelli tabulari, in **Esplora soluzioni**, fare doppio clic su **Model. bim** per aprire il modello nella finestra di progettazione. 
    
    ![as-lesson2-getdata](../tutorial-tabular-1400/media/as-lesson2-getdata.png)
  
2.  In recupera dati, fare clic su **Database** > **Database SQL Server** > **Connect**.  
  
3.  Nel **Database di SQL Server** finestra di dialogo, nel **Server**, digitare il nome del server in cui è installato il database AdventureWorksDW e quindi fare clic su **Connect**.  

4.  Quando viene richiesto di immettere le credenziali, è necessario specificare le credenziali di che Analysis Services utilizza per connettersi all'origine dati durante l'importazione e l'elaborazione dei dati. Nelle **modalità di rappresentazione**, selezionare **rappresentare l'Account**, quindi immettere le credenziali e quindi fare clic su **Connect**. È consigliabile che utilizzare un account in cui le password senza scadenza.

    ![as-lesson2-account](../tutorial-tabular-1400/media/as-lesson2-account.png)
  
    > [!NOTE]  
    > L'utilizzo di un account utente e una password di Windows rappresenta il metodo più sicuro per la connessione a un'origine dati.
  
5.  Nel Pannello di navigazione selezionare la **AdventureWorksDW** del database e quindi fare clic su **OK**. In questo modo viene creata la connessione al database. 
  
6.  Nello strumento di navigazione selezionare la casella di controllo per le tabelle seguenti: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, e **FactInternetSales**.  

    ![as-lesson2-select-tables](../tutorial-tabular-1400/media/as-lesson2-select-tables.png)
  
Dopo aver selezionato OK, viene aperto l'Editor di Query. Nella sezione successiva, si seleziona solo i dati da importare.

  
## <a name="filter-the-table-data"></a>Filtrare i dati della tabella  

Le tabelle nel database di esempio AdventureWorksDW hanno dati che non sono necessari includere nel modello. Quando possibile, si desidera filtrare i dati non necessari per risparmiare spazio nella memoria utilizzato dal modello. È escludere alcune colonne dalle tabelle in modo che non vengano importate nel database dell'area di lavoro o il database del modello dopo che è stato distribuito. 
  
#### <a name="to-filter-the-table-data-before-importing"></a>Per filtrare i dati della tabella prima dell'importazione  
  
1.  Nell'Editor di Query, selezionare la **DimCustomer** tabella. Verrà visualizzata una vista della tabella DimCustomer nell'origine dati (database di esempio AdventureWorksDW). 
  
2.  Selezione multipla (Ctrl + clic) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, quindi pulsante destro del mouse e quindi fare clic su **Rimuovi colonne**. 

    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-columns.png)
  
    Poiché i valori per queste colonne non sono attinenti all'analisi delle vendite Internet, non è necessario importare queste colonne. Eliminazione di colonne non necessarie rende il modello più piccoli e più efficiente.  

    > [!TIP]
    > Se si commette un errore, è possibile eseguire il backup, eliminando un passaggio **passaggi applicati**.   
    
    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-step.png)

  
4.  Filtrare le tabelle restanti rimuovendo le colonne seguenti in ogni tabella:  
    
    **DimDate**
    
      |colonna|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |colonna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |colonna|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |colonna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |colonna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      Nessuna colonna rimossa.
  
## <a name="Import"></a>Import the selected tables and column data  

Dopo aver visualizzato in anteprima e filtrati i dati non necessari, è possibile importare il resto dei dati che si desidera. La procedura guidata consente di importare i dati delle tabelle e qualsiasi relazione presente tra le tabelle. Vengono create nuove tabelle e colonne nel modello e non è possibile importare i dati esclusi tramite filtro.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Per importare i dati delle tabelle e delle colonne selezionati  
  
1.  Verificare le selezioni. Se tutto sembra corretto, fare clic su **importazione**. La finestra di dialogo di elaborazione dei dati mostra lo stato dei dati da importare dall'origine dati nel database dell'area di lavoro.
  
    ![as-lesson2-success](../tutorial-tabular-1400/media/as-lesson2-success.png) 
  
2.  Scegliere **Chiudi**.  

  
## <a name="save-your-model-project"></a>Salvare il progetto di modello  

È importante salvare frequentemente il progetto di modello.  
  
#### <a name="to-save-the-model-project"></a>Per salvare il progetto di modello  
  
-   Click **Salva tutto** > **File**.  
  
## <a name="whats-next"></a>Quali sono le operazioni successive?

[Lezione 3: Contrassegna come tabella data](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md).

  
  
