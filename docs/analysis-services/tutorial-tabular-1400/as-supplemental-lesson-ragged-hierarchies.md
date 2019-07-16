---
title: "Analysis Services lezione supplementare dell'esercitazione: Gerarchie incomplete | Microsoft Docs"
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
ms.openlocfilehash: 420b1ca4e6cdd72d86c715301957be1f14074fee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207125"
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Lezione supplementare - Gerarchie incomplete

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione supplementare, risolvere un problema comune quando la trasformazione tramite pivot sulle gerarchie che contengono valori (membri) vuoti a livelli diversi. Ad esempio, un'organizzazione in cui un responsabile di alto livello ha sia responsabili di reparto sia non responsabili come subalterni. In alternativa, le gerarchie geografiche composte da paese-regione-città, in cui alcune città non dispongono di uno stato o provincia, ad esempio Washington D.C., città del Vaticano. Quando una gerarchia include membri vuoti, spesso finisce per includere livelli diversi o incompleti.

![as-lesson-detail-ragged-hierarchies-table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

I modelli tabulari a livello di compatibilità 1400 offrono un'altra **Nascondi membri** proprietà per le gerarchie. Il **predefinito** impostazione dà per scontato vi siamo membri vuoti a qualsiasi livello. Il **Nascondi membri vuoti** impostazione esclude i membri vuoti dalla gerarchia quando aggiunto a una tabella pivot o un report.  
  
Tempo stimato per il completamento della lezione: **20 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo articolo lezione supplementare fa parte di un'esercitazione di modellazione tabulare. Prima di eseguire le attività in questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti o avere un progetto di modello di esempio Adventure Works Internet Sales completato. 

Se è stato creato il progetto AW Internet Sales come parte dell'esercitazione, il modello non contiene ancora dati o gerarchie incomplete. Per completare questa lezione supplementare, è necessario innanzitutto creare il problema aggiungendo alcune tabelle, creare relazioni, colonne calcolate, una misura e una nuova gerarchia organizzativa. Questa operazione richiede circa 15 minuti. Quindi, è possibile risolvere l'errore in pochi minuti.  

## <a name="add-tables-and-objects"></a>Aggiungere tabelle e oggetti
  
### <a name="to-add-new-tables-to-your-model"></a>Per aggiungere nuove tabelle al modello
  
1.  In Esplora modelli tabulari, espandere **Zdroje dat**, quindi fare clic sulla connessione > **Importa nuove tabelle**.
  
2.  Nello strumento di navigazione, selezionare **DimEmployee** e **FactResellerSales**, quindi fare clic su **OK**.

3.  Nell'Editor di Query, fare clic su **importazione**

4.  Creare la seguente [relazioni](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | Tabella 1           | Colonna       | Direzione del filtro   | tabella 2     | Colonna      | Attivo |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Impostazione predefinita            | DimDate     | Date        | Yes    |
    | FactResellerSales | DueDate      | Impostazione predefinita            | DimDate     | Date        | No     |
    | FactResellerSales | ShipDateKey  | Impostazione predefinita            | DimDate     | Date        | No     |
    | FactResellerSales | ProductKey   | Impostazione predefinita            | DimProduct  | ProductKey  | Yes    |
    | FactResellerSales | EmployeeKey  | Per entrambe le tabelle | DimEmployee | EmployeeKey | Yes    |

5. Nel **DimEmployee** tabella, creare la seguente [le colonne calcolate](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md): 

    **Percorso** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **nome completo** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],2,1)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],3,1)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],4,1)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],5,1)) 
    ```

6.  Nel **DimEmployee** tabella, creare un [gerarchia](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md) denominato **organizzazione**. Aggiungere le colonne seguenti nell'ordine: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  Nel **FactResellerSales** tabella, creare la seguente [misura](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Uso [analizza in Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md) per aprire Excel e creare automaticamente una tabella pivot.

9.  Nella **PivotTable Fields**, aggiungere il **organizzazione** gerarchia dal **DimEmployee** alla tabella **righe**e il  **ResellerTotalSales** misurate la distanza tra il **FactResellerSales** alla tabella **valori**.

    ![as-lesson-detail-ragged-hierarchies-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    Come può notare nella tabella pivot, la gerarchia Mostra righe incomplete. Sono presenti molte righe in cui vengono visualizzati i membri vuoti.

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>Per correggere la gerarchia incompleta impostando proprietà Nascondi membri

1.  Nelle **Esplora modelli tabulari**, espandere **tabelle** > **DimEmployee** > **gerarchie**  >  **Organizzazione**.

2.  Nelle **delle proprietà** > **Nascondi membri**, selezionare **Nascondi membri vuoti**. 

    ![as-lesson-detail-ragged-hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  Aggiorna la tabella pivot in Excel. 

    ![as-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Ora che ha un aspetto decisamente migliore.

## <a name="see-also"></a>Vedere anche   
[Lezione 9: Creare gerarchie](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[Lezione supplementare: sicurezza dinamica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Lezione supplementare: righe di dettaglio](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
