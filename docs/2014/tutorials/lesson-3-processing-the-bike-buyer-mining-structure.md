---
title: "Lezione 3: L'elaborazione della struttura di Data Mining Bike Buyer | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e748c2cd-339d-4e82-82f1-be2d0fc41b61
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2e3f85016b32884b9a6b809e28d20d9985f97cd9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62655800"
---
# <a name="lesson-3-processing-the-bike-buyer-mining-structure"></a>Lezione 3: Elaborazione della struttura di data mining Bike Buyer
  In questa lezione si utilizzerà l'inserimento in istruzione e la vista vTargetMail il [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] per elaborare le strutture di data mining e modelli di data mining creato nel database di esempio [lezione 1: Creazione della struttura di Data Mining Bike Buyer](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md) e [lezione 2: Aggiunta di modelli di Data Mining alla struttura di Data Mining Bike Buyer](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md).  
  
 Quando si elabora una struttura di data mining, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] legge i dati di origine e compila le strutture che supportano i modelli di data mining. Quando si elabora un modello di data mining, i dati definiti dalla struttura di data mining vengono elaborati tramite l'algoritmo di data mining selezionato. L'algoritmo ricerca tendenze e schemi e quindi archivia queste informazioni nel modello di data mining. Il modello di data mining non contiene pertanto i dati di origine effettivi, bensì le informazioni individuate dall'algoritmo. Per altre informazioni sull'elaborazione dei modelli di data mining, vedere [considerazioni e requisiti di elaborazione &#40;Data Mining&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Una struttura di data mining deve essere rielaborata solo se si modifica una colonna della struttura o i dati di origine. Se si aggiunge un modello di data mining a una struttura di data mining già elaborata, è possibile utilizzare l'istruzione INSERT INTO MINING MODEL per eseguire il training del nuovo modello di data mining.  
  
## <a name="train-structure-template"></a>Training del modello di struttura  
 Per eseguire il training struttura di data mining e i relativi modelli di data mining associati, usare il [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) istruzione. Il codice nell'istruzione può essere suddiviso nelle parti seguenti:  
  
-   Identificazione della struttura di data mining  
  
-   Creazione di un elenco delle colonne nella struttura di data mining  
  
-   Definizione dei dati di training  
  
 Di seguito è riportato un esempio generico dell'istruzione INSERT INTO:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
)  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 La prima riga del codice identifica la struttura di data mining di cui si eseguirà il training:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 La riga successiva del codice specifica le colonne definite dalla struttura di data mining. È necessario che siano elencate tutte le colonne nella struttura di data mining e ogni colonna deve essere associata a una colonna nei dati della query di origine.  
  
```  
(  
   <mining structure columns>  
)  
```  
  
 L'ultima riga del codice definisce i dati che verranno utilizzati per il training della struttura di data mining.  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 In questa lezione si utilizzerà `OPENQUERY` per definire i dati di origine. Per informazioni sugli altri metodi di definizione di query di origine, vedere [ &#60;query sull'origine dati&#62;](/sql/dmx/source-data-query).  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione verrà eseguita l'attività seguente:  
  
-   Elaborazione della struttura di data mining Bike Buyer  
  
## <a name="processing-the-predictive-mining-structure"></a>Elaborazione della struttura di data mining predittiva  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>Per elaborare la struttura di data mining mediante INSERT INTO  
  
1.  Nella **Esplora oggetti**, fare doppio clic sull'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], scegliere **nuova Query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico dell'istruzione INSERT INTO nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    [<mining structure name>]   
    ```  
  
     con:  
  
    ```  
    Bike Buyer  
    ```  
  
4.  Sostituire quanto segue:  
  
    ```  
    <mining structure columns>  
    ```  
  
     con:  
  
    ```  
    [Customer Key],  
    [Age],  
    [Bike Buyer],  
    [Commute Distance],  
    [Education],  
    [Gender],  
    [House Owner Flag],  
    [Marital Status],  
    [Number Cars Owned],  
    [Number Children At Home],  
    [Occupation],  
    [Region],  
    [Total Children],  
    [Yearly Income]  
    ```  
  
5.  Sostituire quanto segue:  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     con:  
  
    ```  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
     L'istruzione OPENQUERY fa riferimento all'origine dati [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] per accedere alla vista vTargetMail in cui sono contenuti i dati di origine che verranno utilizzati per il training dei modelli di data mining.  
  
     L'istruzione completa dovrebbe risultare analoga alla seguente:  
  
    ```  
    INSERT INTO MINING STRUCTURE [Bike Buyer]  
    (  
       [Customer Key],  
       [Age],  
       [Bike Buyer],  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]     
    )  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
6.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
7.  Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `Process Bike Buyer Structure.dmx`.  
  
8.  Sulla barra degli strumenti, scegliere il **Execute** pulsante.  
  
 Nella lezione successiva verrà esplorato il contenuto dei modelli di data mining aggiunti alla struttura di data mining in questa lezione.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 4: Esplorazione di modelli di Data Mining Bike Buyer](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
  
  
