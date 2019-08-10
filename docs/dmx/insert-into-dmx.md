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
ms.openlocfilehash: 210ab8c5750fdcb38bcbca324d77eecd926042d1
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892718"
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Consente di elaborare l'oggetto di data mining specificato. Per ulteriori informazioni sull'elaborazione di modelli di data mining e strutture di data mining, vedere [requisiti di elaborazione e &#40;considerazioni sul data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/processing-requirements-and-considerations-data-mining).  
  
 Se è specificata una struttura di data mining, l'istruzione elabora la struttura e tutti i modelli di data mining associati. Se è specificato un modello di data mining, l'istruzione elabora solo tale modello.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>Argomenti  
 *model*  
 Identificatore del modello.  
  
 *struttura*  
 Identificatore della struttura.  
  
 *colonne del modello mappato*  
 Elenco delimitato da virgole contenente identificatori di colonna e identificatori nidificati.  
  
 *query sui dati di origine*  
 Query di origine nel formato definito dal provider.  
  
## <a name="remarks"></a>Note  
 Se non si specifica un **modello di data mining** o una [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] **struttura di data mining**, Cerca il tipo di oggetto in base al nome ed elabora l'oggetto corretto. Se il server contiene una struttura di data mining e un modello di data mining con lo stesso nome, verrà restituito un errore.  
  
 Utilizzando la seconda forma di sintassi, inserire in *\<> di oggetti*. COLUMN_VALUES, è possibile inserire i dati direttamente nelle colonne del modello senza training del modello. Questo metodo consente di fornire dati di colonna al modello in un modo ordinato e conciso, che risulta utile quando si utilizzano set di dati che contengono gerarchie o colonne ordinate.  
  
 Se si utilizza l'istruzione **Insert into** con un modello di data mining o una struttura di data \<mining e si lasciano le \<colonne del modello mappate > e la query dei dati di origine > argomenti, l'istruzione si comporta come **ProcessDefault**, utilizzando Binding che esiste già. Se le associazioni non esistono, l'istruzione restituirà un errore. Per ulteriori informazioni su **ProcessDefault**, vedere [Opzioni e impostazioni &#40;di elaborazione&#41;Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services). La sintassi è illustrata nell'esempio seguente:  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 Se si specifica **modello di data mining** e si forniscono colonne mappate e una query sui dati di origine, il modello e la struttura associata vengono elaborati.  
  
 Nella tabella seguente sono descritti i risultati delle diverse forme dell'istruzione, a seconda dello stato degli oggetti.  
  
|.|Stato degli oggetti|Risultato|  
|---------------|----------------------|------------|  
|Inserisci nel modello di *\<modello di data mining >*|La struttura di data mining viene elaborata.|Il modello di data mining viene elaborato.|  
||La struttura di data mining non è elaborata.|Vengono elaborati il modello e la struttura di data mining.|  
||La struttura di data mining contiene modelli di data mining aggiuntivi.|L'elaborazione non riesce. È necessario rielaborare la struttura e i modelli di data mining associati.|  
|Inserisci nella struttura della *\<struttura di data mining >*|La struttura di data mining viene elaborata o non elaborata.|La struttura di data mining e i modelli di data mining associati vengono elaborati.|  
|Inserimenti nel *\<* modello di modello di data mining > che contiene una query di origine<br /><br /> oppure<br /><br /> Inserisci nella *\<struttura* della struttura di data mining > che contiene una query di origine|La struttura o il modello include già un contenuto.|L'elaborazione non riesce. È necessario cancellare gli oggetti prima di eseguire questa operazione, utilizzando [Delete &#40;DMX&#41;](../dmx/delete-dmx.md).|  
  
## <a name="mapped-model-columns"></a>Elemento mapped model columns  
 Utilizzando le colonne \<del modello mappate > elemento, è possibile eseguire il mapping delle colonne dall'origine dati alle colonne nel modello di data mining. Le \<colonne del modello di cui è stato eseguito il mapping > elemento hanno il formato seguente:  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 Con **Skip**è possibile escludere determinate colonne che devono esistere nella query di origine, ma che non esistono nel modello di data mining. SKIP è utile quando non si dispone del controllo sulle colonne incluse nel set di righe di input. Se si scrive una propria funzione OPENQUERY, si consiglia di omettere la colonna dall'elenco di colonne SELECT anziché utilizzare SKIP.  
  
 SKIP è utile anche quando una colonna del set di righe di input è necessaria per eseguire un join, ma la colonna non è utilizzata dalla struttura di data mining. Un esempio tipico è rappresentato da una struttura di data mining e un modello di data mining che contengono una tabella nidificata. Il set di righe di input per questa struttura avrà una colonna di chiave esterna che viene utilizzata per creare un set di righe gerarchico utilizzando la clausola SHAPE, ma la colonna di chiave esterna non è quasi mai utilizzata nel modello.  
  
 La sintassi di SKIP richiede che SKIP venga inserito nella posizione della colonna singola nel set di righe di input che non dispone di una colonna della struttura di data mining corrispondente. Ad esempio, nella seguente tabella nidificata, OrderNumber deve essere selezionato nella clausola APPEND in modo da poter essere utilizzato nella clausola RELATE per specificare il join. Tuttavia, non si desidera inserire i dati di OrderNumber nella tabella nidificata nella struttura di data mining. Nell'esempio è utilizzata pertanto la parola chiave SKIP anziché OrderNumber nell'argomento INSERT INTO.  
  
## <a name="source-data-query"></a>Elemento &lt;source data query&gt;  
 L' \<elemento > di query sui dati di origine può includere i tipi di origine dati seguenti:  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **FORMA**  
  
-   Qualsiasi query di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che restituisce un set di righe.  
  
 Per altre informazioni sui tipi di origine dati, vedere [ &#60;query&#62;sui dati di origine](../dmx/source-data-query.md).  
  
## <a name="basic-example"></a>Esempio di base  
 Nell'esempio seguente viene usato **OPENQUERY** per eseguire il training di un modello Naive Bayes basato sui dati di [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] mailing diretto nel database.  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>Esempio con tabella nidificata  
 Nell'esempio seguente viene utilizzata la **forma** per eseguire il training di un modello di data mining di associazione che contiene una tabella nidificata. Si noti che la prima riga contiene **Skip** invece OrderNumber, che è obbligatorio nell'istruzione **SHAPE_APPEND** ma non viene utilizzata nel modello di data mining.  
  
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
 [Istruzioni DMX per &#40;la&#41; definizione dei dati DMX di Data Mining Extensions](../dmx/dmx-statements-data-definition.md)   
 [Istruzioni di manipolazione &#40;dei&#41; dati DMX di Data Mining Extensions](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
