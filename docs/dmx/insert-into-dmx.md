---
title: INSERT INTO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 16732c1d889f7125d71d01bd0804b4202daceb7e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62505151"
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Consente di elaborare l'oggetto di data mining specificato. Per altre informazioni sull'elaborazione di modelli di data mining e strutture di data mining, vedere [considerazioni e requisiti di elaborazione &#40;Data Mining&#41;](../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Se è specificata una struttura di data mining, l'istruzione elabora la struttura e tutti i modelli di data mining associati. Se è specificato un modello di data mining, l'istruzione elabora solo tale modello.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>Argomenti  
 *model*  
 Identificatore del modello.  
  
 *structure*  
 Identificatore della struttura.  
  
 *colonne del modello con mapping*  
 Elenco delimitato da virgole contenente identificatori di colonna e identificatori nidificati.  
  
 *query sull'origine dati*  
 Query di origine nel formato definito dal provider.  
  
## <a name="remarks"></a>Note  
 Se non si specifica **modello di data MINING** oppure **struttura di data MINING**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Cerca il tipo di oggetto in base al nome ed elabora l'oggetto corretto. Se il server contiene una struttura di data mining e un modello di data mining con lo stesso nome, verrà restituito un errore.  
  
 Tramite la seconda forma della sintassi, INSERT INTO*\<oggetto >*. COLUMN_VALUES è possibile inserire dati direttamente nelle colonne del modello senza training del modello. Questo metodo consente di fornire dati di colonna al modello in un modo ordinato e conciso, che risulta utile quando si utilizzano set di dati che contengono gerarchie o colonne ordinate.  
  
 Se si usa **INSERT INTO** con un modello di data mining o una struttura di data mining e lasciare disattivato il \<eseguito il mapping delle colonne del modello di > e \<query sull'origine dati > argomenti, l'istruzione si comporta come  **ProcessDefault**, utilizzando associazioni già esistenti. Se le associazioni non esistono, l'istruzione restituirà un errore. Per altre informazioni sulle **ProcessDefault**, vedere [opzioni di elaborazione e le impostazioni &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md). La sintassi è illustrata nell'esempio seguente:  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 Se si specifica **modello di data MINING** e forniscono colonne con mapping e query di dati di origine, il modello e struttura associata viene elaborata.  
  
 Nella tabella seguente sono descritti i risultati delle diverse forme dell'istruzione, a seconda dello stato degli oggetti.  
  
|.|Stato degli oggetti|Risultato|  
|---------------|----------------------|------------|  
|INSERT INTO MINING MODEL*\<modello >*|La struttura di data mining viene elaborata.|Il modello di data mining viene elaborato.|  
||La struttura di data mining non è elaborata.|Vengono elaborati il modello e la struttura di data mining.|  
||La struttura di data mining contiene modelli di data mining aggiuntivi.|L'elaborazione non riesce. È necessario rielaborare la struttura e i modelli di data mining associati.|  
|INSERT INTO MINING STRUCTURE*\<struttura >*|La struttura di data mining viene elaborata o non elaborata.|La struttura di data mining e i modelli di data mining associati vengono elaborati.|  
|INSERT INTO MINING MODEL*\<modello >* contenente una query di origine<br /><br /> o Gestione configurazione<br /><br /> INSERT INTO MINING STRUCTURE*\<struttura >* contenente una query di origine|La struttura o il modello include già un contenuto.|L'elaborazione non riesce. È necessario deselezionare gli oggetti prima di eseguire questa operazione, utilizzando [eliminare &#40;DMX&#41;](../dmx/delete-dmx.md).|  
  
## <a name="mapped-model-columns"></a>Elemento mapped model columns  
 Tramite il \<il mapping delle colonne del modello > elemento, è possibile mappare le colonne dall'origine dati alle colonne nel modello di data mining. Il \<il mapping delle colonne del modello > elemento ha il formato seguente:  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 Usando **SKIP**, è possibile escludere determinate colonne che devono esistere nella query di origine, ma che non esistono nel modello di data mining. SKIP è utile quando non si dispone del controllo sulle colonne incluse nel set di righe di input. Se si scrive una propria funzione OPENQUERY, si consiglia di omettere la colonna dall'elenco di colonne SELECT anziché utilizzare SKIP.  
  
 SKIP è utile anche quando una colonna del set di righe di input è necessaria per eseguire un join, ma la colonna non è utilizzata dalla struttura di data mining. Un esempio tipico è rappresentato da una struttura di data mining e un modello di data mining che contengono una tabella nidificata. Il set di righe di input per questa struttura avrà una colonna di chiave esterna che viene utilizzata per creare un set di righe gerarchico utilizzando la clausola SHAPE, ma la colonna di chiave esterna non è quasi mai utilizzata nel modello.  
  
 La sintassi di SKIP richiede che SKIP venga inserito nella posizione della colonna singola nel set di righe di input che non dispone di una colonna della struttura di data mining corrispondente. Ad esempio, nella seguente tabella nidificata, OrderNumber deve essere selezionato nella clausola APPEND in modo da poter essere utilizzato nella clausola RELATE per specificare il join. Tuttavia, non si desidera inserire i dati di OrderNumber nella tabella nidificata nella struttura di data mining. Nell'esempio è utilizzata pertanto la parola chiave SKIP anziché OrderNumber nell'argomento INSERT INTO.  
  
## <a name="source-data-query"></a>Elemento &lt;source data query&gt;  
 Il \<query sull'origine dati > elemento può includere tipi di origine dati seguenti:  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **SHAPE**  
  
-   Qualsiasi query di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che restituisce un set di righe.  
  
 Per altre informazioni sui tipi di origini dati, vedere [ &#60;query sull'origine dati&#62;](../dmx/source-data-query.md).  
  
## <a name="basic-example"></a>Esempio di base  
 L'esempio seguente usa **OPENQUERY** per eseguire il training di un modello Naive Bayes basato sui dati mirati mailing diretto nel [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] database.  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>Esempio con tabella nidificata  
 L'esempio seguente usa **forma** per il training di un modello di data mining di associazione che contiene una tabella nidificata. Si noti che la prima riga contiene **SKIP** invece OrderNumber, necessario per il **SHAPE_APPEND** istruzione ma non utilizzata nel modello di data mining.  
  
```  
INSERT INTO MyAssociationModel  
    ([OrderNumber],[Models] (SKIP, [Model])  
    )  
SHAPE {  
    OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
AS [Models]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
