---
title: Definizione dei set denominati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 47254fd3-525f-4c35-b93d-316607652517
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c13de7878753524986cd4574aa2e892b3367eb6e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078411"
---
# <a name="defining-named-sets"></a>Definizione dei set denominati
  Un set denominato è un'espressione MDX (Multidimensional Expressions) che restituisce un set di membri della dimensione. È possibile definire set denominati e salvarli come parte della definizione del cubo, nonché creare set denominati in applicazioni client. I set denominati possono essere creati combinando dati del cubo, operatori aritmetici, numeri e funzioni. I set denominati possono essere utilizzati dagli utenti nelle query MDX in applicazioni client, nonché per definire set nei sottocubi. Un sottocubo è una raccolta di set di crossjoin che limita lo spazio del cubo nel sottospazio definito per istruzioni successive. La definizione di uno spazio del cubo limitato costituisce un concetto fondamentale dello scripting MDX.  
  
 I set denominati semplificano le query MDX e generano alias utili per espressioni set complesse utilizzate spesso. È possibile ad esempio definire un set denominato chiamato Large Resellers contenente il set di membri nella dimensione Reseller con il numero più elevato di dipendenti. Gli utenti finali potrebbero quindi utilizzare il set denominato Large Resellers nelle query, oppure utilizzarlo per definire un set in un sottocubo. Le definizioni dei set denominati vengono archiviate nei cubi, ma i loro valori si trovano solo nella memoria. Per creare un set denominato usare il comando **Nuovo set denominato** nella scheda **Calcoli** di Progettazione cubi. Per altre informazioni, vedere [Calcoli](multidimensional-models-olap-logical-cube-objects/calculations.md)e [Creare set denominati](multidimensional-models/create-named-sets.md).  
  
 Nelle procedure descritte in questo argomento si definiranno due set denominati: Core Products e Large Resellers.  
  
## <a name="defining-a-core-products-named-set"></a>Definizione di un set denominato Core Products  
  
1.  Passare alla scheda **Calcoli** di Progettazione cubi per il cubo di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial e fare clic su **Visualizzazione Form** nella barra degli strumenti.  
  
2.  Fare clic su **[Total Sales Ratio to All Products]** nel riquadro **Libreria script** e quindi fare clic su **Nuovo set denominato** nella barra degli strumenti della scheda **Calcoli** .  
  
     Quando si definisce un nuovo calcolo nella scheda **Calcoli** ricordare che i calcoli vengono risolti seguendo l'ordine di visualizzazione del riquadro **Libreria script** . Il calcolo selezionato all'interno di tale riquadro al momento della creazione di un nuovo calcolo ne determina l'ordine di esecuzione. Un nuovo calcolo viene definito immediatamente dopo il calcolo selezionato.  
  
3.  Nel **Name** modificare il nome del nuovo set denominato in `[Core Products]`.  
  
     Si noti nel riquadro **Libreria script** l'icona speciale che distingue un set denominato da un comando script o da un membro calcolato.  
  
4.  Nel **metadati** scheda le **strumenti di calcolo** riquadro, espandere **prodotto**, espandere **categoria**, espandere `Members`e quindi Espandere **All Products**.  
  
    > [!NOTE]  
    >  Se non è possibile visualizzare i metadati nel riquadro **Strumenti di calcolo** , fare clic su **Riconnetti** sulla barra degli strumenti. Se questo sistema non funziona, può essere necessario elaborare il cubo o avviare l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
5.  Trascinare **Bikes** nella casella **Espressione** .  
  
     È stata ora creata un'espressione set che restituirà il set di membri contenuti nella categoria Bike della dimensione Product.  
  
## <a name="defining-a-large-resellers-named-set"></a>Definizione di un set denominato Large Resellers  
  
1.  Fare doppio clic su `[Core Products]` nella **libreria Script** riquadro e quindi fare clic su **nuovo Set denominato**.  
  
2.  Nel **Name** modificare il nome di questo set denominato in `[Large Resellers]`.  
  
3.  Nel **espressione** , digitare `Exists()`.  
  
     La funzione Exists verrà usata per restituire il set di membri della gerarchia dell'attributo Reseller Name che si interseca con il set di membri della gerarchia dell'attributo Number of Employees contenente il maggior numero di dipendenti.  
  
4.  Nella scheda **Metadati** del riquadro **Strumenti di calcolo** , espandere la dimensione **Reseller** e quindi espandere la gerarchia dell'attributo **Reseller Name** .  
  
5.  Trascinare il livello **Nome rivenditore** all'interno delle parentesi per l'espressione set Exists.  
  
     Per restituire tutti i membri di questo set si userà la funzione Members. Per altre informazioni, vedere [Members &#40;Set&#41; &#40;MDX&#41;](/sql/mdx/members-set-mdx).  
  
6.  Digitare un punto dopo l'espressione set parziale e quindi aggiungere la funzione Members. L'espressione dovrebbe avere l'aspetto sotto illustrato:  
  
    ```  
    Exists([Reseller].[Reseller Name].[Reseller Name].Members)  
    ```  
  
     Ora che è stato definito il primo set per il metodo Exists espressione set, è possibile aggiungere il secondo set, il set di membri della dimensione Reseller contenente il maggior numero di dipendenti.  
  
7.  Nel **metadati** scheda le **strumenti di calcolo** riquadro, espandere **Number of Employees** nella dimensione Reseller, espandere `Members`e quindi espandere **Tutti i rivenditori**.  
  
     Si noti che i membri di questa gerarchia dell'attributo non sono raggruppati.  
  
8.  Aprire Progettazione dimensioni per la dimensione **Reseller** e quindi fare clic su **Number of Employees** nel riquadro **Attributi** .  
  
9. Nella finestra Proprietà modificare il `DiscretizationMethod` proprietà **automatici**e quindi modificare la `DiscretizationBucketCount` proprietà `5`. Per altre informazioni, vedere [Raggruppare membri di attributo &#40;discretizzazione&#41;](multidimensional-models/attribute-properties-group-attribute-members.md).  
  
10. Scegliere **Distribuisci Analysis Services Tutorial** dal menu [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]Compila **di**.  
  
11. Dopo aver completato la distribuzione, passare a Progettazione cubi per il cubo di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial e fare clic su **Riconnetti** nella barra degli strumenti della scheda **Calcoli** .  
  
12. Nel **metadati** scheda il **strumenti di calcolo** riquadro, espandere **Number of Employees** nel **rivenditore** della dimensione, espandere `Members`, quindi espandere **tutti i rivenditori**.  
  
     Si noti che i membri di questa gerarchia di attributi sono ora contenuti in cinque gruppi, numerati da 0 a 4. Per visualizzare il numero di un gruppo, posizionare il puntatore sul gruppo per visualizzare una finestra popup. Per l'intervallo `2 -17`InfoTip deve contenere `[Reseller].[Number of Employees].&[0]`.  
  
     I membri di questa gerarchia dell'attributo sono raggruppati perché la proprietà DiscretizationBucketCount è impostata su `5` e la proprietà DiscretizationMethod è impostata su **automatica**.  
  
13. Nell'espressione set Exists contenuta nella casella **Espressione** aggiungere una virgola dopo la funzione Members e prima della parentesi di chiusura, quindi trascinare **83 - 100** dal riquadro **Metadati** e posizionarlo dopo la virgola.  
  
     È stata ora completata l'espressione set Exists che restituirà il set di membri che si interseca con i due set specificati, ovvero il set di tutti i rivenditori e il set dei rivenditori con un numero di dipendenti compreso tra 83 e 100, quando il set denominato Large Resellers viene posto su un'asse.  
  
     La figura seguente mostra le **espressioni di calcolo** riquadro per il `[Large Resellers]` set denominato.  
  
     ![Riquadro espressioni di calcolo per [Large Resellers]](../../2014/tutorials/media/l6-named-set-02.gif "riquadro espressioni di calcolo per [Large Resellers]")  
  
14. Nella barra degli strumenti della scheda **Calcoli** fare clic su **Visualizzazione Script**e quindi controllare i due set denominati appena aggiunti allo script di calcolo.  
  
15. Aggiungere una nuova riga nello script di calcolo, immediatamente precedente al primo comando CREATE SET, e quindi aggiungere allo script il testo seguente su una riga a se stante:  
  
    ```  
    /* named sets */  
    ```  
  
     Sono stati ora definiti due set denominati, entrambi visibili nel riquadro **Libreria script** . È ora possibile passare alla distribuzione di tali set denominati, nonché esplorare tali misure nel cubo di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial.  
  
## <a name="browsing-the-cube-by-using-the-new-named-sets"></a>Esplorazione del cubo utilizzando i nuovi set denominati  
  
1.  Nel menu **Compila** di [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], scegliere **Distribuisci Analysis Services Tutorial**.  
  
2.  Al termine delle operazioni di distribuzione, fare clic sulla scheda **Esplorazione** e fare clic su **Riconnetti**.  
  
3.  Deselezionare la griglia nel riquadro Dati.  
  
4.  Aggiungere la misura **Reseller Sales-Sales Amount** all'area dati.  
  
5.  Espandere la dimensione Product, quindi aggiungere Category e Subcategory all'area riga, come illustrato nell'immagine seguente.  
  
     ![I membri dell'attributo Subcategory](../../2014/tutorials/media/l6-named-set-03.gif "membri dell'attributo Subcategory")  
  
6.  Nel riquadro **Metadati** , nella dimensione **Product** trascinare **Core Products** nell'area filtro.  
  
     Si noti che nel cubo restano solo il membro **Bike** dell'attributo **Category** e i membri delle sottocategorie **Bike** , poiché il set denominato **Core Products** viene usato per definire un sottocubo. Questo sottocubo limita i membri dell'attributo **Category** nella dimensione **Product** all'interno del sottocubo ai membri del set denominato **Core Product** , come illustrato nella figura seguente.  
  
     ![Set denominato di membri del prodotto principale](../../2014/tutorials/media/l6-named-set-04.gif "set denominato di membri del prodotto principale")  
  
7.  Nel riquadro **Metadati** espandere **Reseller**, quindi aggiungere **Large Resellers** all'area filtro.  
  
     Si noti che la misura Reseller Sales Amount nel riquadro Dati visualizza solo gli importi di vendita per rivenditori di bici di grandi dimensioni. Si noti inoltre che ora il riquadro Filtro visualizza i due set denominati utilizzati per definire questo sottocubo specifico, come illustrato nella figura seguente.  
  
     ![Riquadro filtro contenente due denominato imposta](../../2014/tutorials/media/l6-named-set-05.gif "imposta riquadro filtro contenente due denominato")  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Lezione 7: Definizione degli indicatori di prestazioni chiave &#40;indicatori KPI&#41;](../analysis-services/lesson-7-defining-key-performance-indicators-kpis.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Calcoli](multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [Creare set denominati](multidimensional-models/create-named-sets.md)  
  
  
