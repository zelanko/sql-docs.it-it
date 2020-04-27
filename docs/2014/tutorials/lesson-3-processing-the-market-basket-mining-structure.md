---
title: 'Lezione 3: elaborazione della struttura di data mining Market basket | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 095a043f-cf6f-45bb-a021-ae4e1b535c65
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ce2c2e6944d524a38edc331d2cd128ca7cf7d419
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62653863"
---
# <a name="lesson-3-processing-the-market-basket-mining-structure"></a>Lezione 3: Elaborazione della struttura di data mining Market Basket
  In questa lezione verrà utilizzata l'istruzione [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx) e VAssocSeqLineItems e vAssocSeqOrders dal database di [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] esempio per elaborare le strutture e i modelli di data mining creati nella [lezione 1: creazione della struttura di data mining Market basket](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md) e [lezione 2: aggiunta di modelli di data mining alla struttura di data mining Market basket](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md).  
  
 Quando si elabora una struttura di data mining, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] legge i dati di origine e compila le strutture che supportano i modelli di data mining. Quando si elabora un modello di data mining, i dati definiti dalla struttura di data mining vengono elaborati tramite l'algoritmo di data mining selezionato. L'algoritmo ricerca tendenze e schemi e quindi archivia queste informazioni nel modello di data mining. Il modello di data mining non contiene pertanto i dati di origine effettivi, bensì le informazioni individuate dall'algoritmo. Per ulteriori informazioni sull'elaborazione dei modelli di data mining, vedere [requisiti e considerazioni sull'elaborazione &#40;&#41;di data mining ](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Una struttura di data mining deve essere rielaborata solo se si modifica una colonna della struttura o i dati di origine. Se si aggiunge un modello di data mining a una struttura di data mining già elaborata, è possibile utilizzare l'istruzione `INSERT INTO MINING MODEL` per eseguire il training del nuovo modello di data mining sui dati esistenti.  
  
 Dato che la struttura di data mining per l'analisi degli acquisti contiene una tabella nidificata, sarà necessario definire le colonne di data mining di cui eseguire il training utilizzando la struttura di tabelle nidificate e utilizzare il comando `SHAPE` per definire le query che eseguono il pull dei dati di training dalle tabelle di origine.  
  
## <a name="insert-into-statement"></a>Istruzione INSERT INTO  
 Per eseguire il training della struttura di data mining Market basket e dei modelli di data mining associati, utilizzare l'istruzione [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx) . Il codice nell'istruzione può essere suddiviso nelle parti seguenti.  
  
-   Identificazione della struttura di data mining  
  
-   Creazione di un elenco delle colonne nella struttura di data mining  
  
-   Definizione dei dati di training mediante il comando `SHAPE`  
  
 Di seguito è riportato un esempio generico di istruzione `INSERT INTO`:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],'<nested SELECT statement>')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 La prima riga del codice identifica la struttura di data mining di cui si eseguirà il training:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 Le successive righe del codice specificano le colonne definite dalla struttura di data mining. È necessario che siano elencate tutte le colonne nella struttura di data mining e ogni colonna deve essere associata a una colonna nei dati della query di origine. È possibile utilizzare `SKIP` per ignorare le colonne presenti nei dati di origine, ma non nella struttura di data mining. Per ulteriori informazioni sull'utilizzo `SKIP`di, vedere [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx).  
  
```  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
```  
  
 Le ultime righe del codice definiscono i dati che verranno utilizzati per il training della struttura di data mining. Dal momento che i dati di origine sono presenti in due tabelle, si utilizzerà `SHAPE` per correlare le tabelle.  
  
```  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],''<nested SELECT statement>'')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 In questa lezione si utilizzerà `OPENQUERY` per definire i dati di origine. Per informazioni su altri metodi di definizione di una query sui dati di origine, vedere [&#60;query sui dati di origine&#62;](/sql/dmx/source-data-query).  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione verrà eseguita l'attività seguente:  
  
-   Elaborazione della struttura di data mining Market Basket  
  
## <a name="processing-the-market-basket-mining-structure"></a>Elaborazione della struttura di data mining Market Basket  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>Per elaborare la struttura di data mining mediante INSERT INTO  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]mouse sull'istanza di, scegliere **nuova query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico dell'istruzione INSERT INTO nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    [<mining structure>]  
    ```  
  
     con:  
  
    ```  
    Market Basket  
    ```  
  
4.  Sostituire quanto segue:  
  
    ```  
    <mining structure columns>  
    [<nested table>]  
    ( SKIP, <skipped column> )  
    ```  
  
     con:  
  
    ```  
    [OrderNumber],  
    [Products]   
    (SKIP, [Model])  
    ```  
  
     Nell'istruzione, `Products` si riferisce alla tabella Products definita dall'istruzione SHAPE. `SKIP` viene utilizzato per ignorare la colonna Model che esiste nei dati di origine come chiave ma non viene utilizzata dalla struttura di data mining.  
  
5.  Sostituire quanto segue:  
  
    ```  
    SHAPE {  
      OPENQUERY([<datasource>],'<SELECT statement>') }  
    APPEND  
    (   
      {OPENQUERY([<datasource>],'<nested SELECT statement>')  
    }  
    RELATE [<case key>] TO [<foreign key>]  
    ) AS [<nested table>]  
    ```  
  
     con:  
  
    ```  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
     La query di origine fa [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] riferimento all'origine dati definita [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] nel progetto di esempio. Utilizza questa origine dei dati per accedere alle viste vAssocSeqLineItems e vAssocSeqOrders contenenti i dati origine che verranno utilizzati per il training del modello di data mining. Se il progetto non è stato creato o queste visualizzazioni, vedere [esercitazione di base sul data mining](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
     All'interno del comando `SHAPE` si utilizzerà `OPENQUERY` per definire due query. Nella prima query viene definita la tabella padre, mentre nella seconda viene definita la tabella nidificata. Le due tabelle vengono correlate mediante la colonna OrderNumber presente in entrambe.  
  
     L'istruzione completa dovrebbe risultare analoga alla seguente:  
  
    ```  
    INSERT INTO MINING STRUCTURE [Market Basket]  
    (  
       [OrderNumber],[Products] (SKIP, [Model])  
    )  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
6.  Scegliere **Salva DMXQuery1. DMX con nome**dal menu **file** .  
  
7.  Nella finestra di dialogo **Salva con** nome individuare la cartella appropriata e assegnare al file `Process Market Basket.dmx`il nome.  
  
8.  Sulla barra degli strumenti fare clic sul pulsante **Esegui** .  
  
 Una volta terminata l'esecuzione della query, è possibile visualizzare i modelli e i set di elementi trovati, visualizzare le associazioni o filtrare per set di elementi, probabilità o importanza. Per visualizzare queste informazioni, in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse sul nome del modello di dati, quindi scegliere **Sfoglia**.  
  
 Nella lezione successiva verranno create diverse stime basate sui modelli di data mining aggiunti alla struttura Market Basket.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 4: Esecuzione delle stime relative a Market Basket](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
  
  
