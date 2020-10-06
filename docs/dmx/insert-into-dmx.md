---
description: INSERT INTO (DMX)
title: INSERT INTO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 37a7a0e8be59136eb3ab6e0454c7910b9c9e3198
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726162"
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Consente di elaborare l'oggetto di data mining specificato. Per ulteriori informazioni sull'elaborazione di modelli e strutture di data mining, vedere [requisiti e considerazioni sull'elaborazione &#40;&#41;di data mining ](/analysis-services/data-mining/processing-requirements-and-considerations-data-mining).  
  
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
  
## <a name="remarks"></a>Osservazioni  
 Se non si specifica un **modello di data mining** o una **struttura di data mining**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Cerca il tipo di oggetto in base al nome ed elabora l'oggetto corretto. Se il server contiene una struttura di data mining e un modello di data mining con lo stesso nome, verrà restituito un errore.  
  
 Utilizzando la seconda forma di sintassi, inserire in *\<object>* . COLUMN_VALUES, è possibile inserire i dati direttamente nelle colonne del modello senza training del modello. Questo metodo consente di fornire dati di colonna al modello in un modo ordinato e conciso, che risulta utile quando si utilizzano set di dati che contengono gerarchie o colonne ordinate.  
  
 Se si utilizza **Insert into** con un modello di data mining o una struttura di data mining e si lasciano invariati gli \<mapped model columns> \<source data query> argomenti e, l'istruzione si comporta come **ProcessDefault**, utilizzando le associazioni già esistenti. Se le associazioni non esistono, l'istruzione restituirà un errore. Per ulteriori informazioni su **ProcessDefault**, vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services). La sintassi è illustrata nell'esempio seguente:  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 Se si specifica **modello di data mining** e si forniscono colonne mappate e una query sui dati di origine, il modello e la struttura associata vengono elaborati.  
  
 Nella tabella seguente sono descritti i risultati delle diverse forme dell'istruzione, a seconda dello stato degli oggetti.  
  
|Istruzione|Stato degli oggetti|Risultato|  
|---------------|----------------------|------------|  
|INSERISCI NEL MODELLO DI DATA MINING*\<model>*|La struttura di data mining viene elaborata.|Il modello di data mining viene elaborato.|  
||La struttura di data mining non è elaborata.|Vengono elaborati il modello e la struttura di data mining.|  
||La struttura di data mining contiene modelli di data mining aggiuntivi.|L'elaborazione non riesce. È necessario rielaborare la struttura e i modelli di data mining associati.|  
|INSERISCI NELLA STRUTTURA DI DATA MINING*\<structure>*|La struttura di data mining viene elaborata o non elaborata.|La struttura di data mining e i modelli di data mining associati vengono elaborati.|  
|INSERIRE nel modello di data MINING *\<model>* che contiene una query di origine<br /><br /> oppure<br /><br /> Inserisci nella struttura di data MINING *\<structure>* che contiene una query di origine|La struttura o il modello include già un contenuto.|L'elaborazione non riesce. È necessario cancellare gli oggetti prima di eseguire questa operazione, utilizzando [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md).|  
  
## <a name="mapped-model-columns"></a>Elemento mapped model columns  
 Utilizzando l' \<mapped model columns> elemento, è possibile eseguire il mapping delle colonne dall'origine dati alle colonne nel modello di data mining. L' \<mapped model columns> elemento ha il formato seguente:  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 Con **Skip**è possibile escludere determinate colonne che devono esistere nella query di origine, ma che non esistono nel modello di data mining. SKIP è utile quando non si dispone del controllo sulle colonne incluse nel set di righe di input. Se si scrive una propria funzione OPENQUERY, si consiglia di omettere la colonna dall'elenco di colonne SELECT anziché utilizzare SKIP.  
  
 SKIP è utile anche quando una colonna del set di righe di input è necessaria per eseguire un join, ma la colonna non è utilizzata dalla struttura di data mining. Un esempio tipico è rappresentato da una struttura di data mining e un modello di data mining che contengono una tabella nidificata. Il set di righe di input per questa struttura avrà una colonna di chiave esterna che viene utilizzata per creare un set di righe gerarchico utilizzando la clausola SHAPE, ma la colonna di chiave esterna non è quasi mai utilizzata nel modello.  
  
 La sintassi di SKIP richiede che SKIP venga inserito nella posizione della colonna singola nel set di righe di input che non dispone di una colonna della struttura di data mining corrispondente. Ad esempio, nella seguente tabella nidificata, OrderNumber deve essere selezionato nella clausola APPEND in modo da poter essere utilizzato nella clausola RELATE per specificare il join. Tuttavia, non si desidera inserire i dati di OrderNumber nella tabella nidificata nella struttura di data mining. Nell'esempio è utilizzata pertanto la parola chiave SKIP anziché OrderNumber nell'argomento INSERT INTO.  
  
## <a name="source-data-query"></a>Elemento &lt;source data query&gt;  
 L' \<source data query> elemento può includere i tipi di origine dati seguenti:  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **FORMA**  
  
-   Qualsiasi query di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che restituisce un set di righe.  
  
 Per altre informazioni sui tipi di origine dati, vedere [&#60;&#62;query sui dati di origine ](../dmx/source-data-query.md).  
  
## <a name="basic-example"></a>Esempio di base  
 Nell'esempio seguente viene usato **OPENQUERY** per eseguire il training di un modello Naive Bayes basato sui dati di mailing diretto nel [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] database.  
  
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
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
