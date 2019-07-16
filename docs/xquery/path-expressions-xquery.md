---
title: Espressioni di percorso (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- path expressions [XQuery]
- expressions [XQuery], path
ms.assetid: b93fa36c-bf69-46b9-b137-f597d66fd0c0
author: rothja
ms.author: jroth
ms.openlocfilehash: 9be2fb8752f27164e0e6dbc59e499f4b048d8979
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946399"
---
# <a name="path-expressions-xquery"></a>Espressioni di percorso (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Le espressioni di percorso XQuery consentono di individuare nodi, ad esempio di testo, attributo o elemento, all'interno di un documento. Il risultato di un'espressione di percorso è sempre nell'ordine del documento, senza nodi duplicati nella sequenza risultante. Nello specificare un percorso è possibile utilizzare la sintassi abbreviata o non abbreviata. Le informazioni seguenti sono relative alla sintassi non abbreviata. La sintassi abbreviata è descritta di seguito in questo argomento.  
  
> [!NOTE]  
>  Poiché le query di esempio in questo argomento vengono specificate con il **xml** colonne di tipo **CatalogDescription** e **istruzioni**, nel  **ProductModel** tabella, è consigliabile acquisire familiarità con il contenuto e struttura del documenti XML archiviati in queste colonne.  
  
 Esistono espressioni di percorso relativo ed espressioni di percorso assoluto. Di seguito vengono descritti ambedue i tipi di espressione:  
  
-   Un'espressione di percorso relativo è costituita da uno o più passi separati da una o due barre (/ o //). Ad esempio, `child::Features` è un'espressione di percorso relativo in cui `Child` si riferisce solo ai nodi figlio del nodo di contesto attualmente elaborato. L'espressione recupera il \<funzionalità > nodi elemento figlio del nodo di contesto.  
  
-   Un'espressione di percorso assoluto inizia con una o due barre (/ o //), seguite da un percorso relativo facoltativo. Ad esempio, la barra iniziale nell'espressione `/child::ProductDescription` indica che si tratta di un'espressione di percorso assoluto. Poiché una barra all'inizio di un'espressione restituisce il nodo radice del documento del nodo di contesto, l'espressione restituisce tutti i \<ProductDescription > nodi elemento figlio della radice del documento.  
  
     Se un percorso assoluto inizia con una sola barra, può essere o meno seguito da un percorso relativo. Se si specifica una sola barra, l'espressione restituisce il nodo radice del nodo di contesto. Per un tipo di dati XML, si tratta del nodo del documento.  
  
 Una tipica espressione di percorso è costituita da passi. Ad esempio, l'espressione di percorso assoluto `/child::ProductDescription/child::Summary`, contiene due passi separati da una barra.  
  
-   Il primo passo recupera i \<ProductDescription > nodi elemento figlio della radice del documento.  
  
-   Il secondo passo recupera i \<Summary > nodi figlio dell'elemento per ogni recuperato \<ProductDescription > nodo elemento, che a sua volta diventa il nodo di contesto.  
  
 Un passo in un'espressione di percorso può essere un passo dell'asse o un passo generale.  
  
## <a name="axis-step"></a>Passo dell'asse  
 Un passo dell'asse in un'espressione di percorso è composto dalle parti seguenti.  
  
 [axis](../xquery/path-expressions-specifying-axis.md)  
 Definisce la direzione di spostamento. Un passo dell'asse in un'espressione di percorso che inizia dal nodo di contesto e si sposta ai nodi raggiungibili nella direzione specificata dall'asse.  
  
 [test di nodo](../xquery/path-expressions-specifying-node-test.md)  
 Specifica il tipo di nodo o i nomi dei nodi da selezionare.  
  
 Zero o più predicati facoltativi  
 Filtrano i nodi selezionandone alcuni e scartandone altri.  
  
 Gli esempi seguenti usano un **axisstep** nelle espressioni di percorso:  
  
-   L'espressione di percorso assoluto `/child::ProductDescription` contiene un solo passo. Specifica un asse (`child`) e un test di nodo (`ProductDescription`).  
  
-   L'espressione di percorso relativo `child::ProductDescription/child::Features` contiene due passi separati da una barra. Entrambi i passi specificano un asse child. ProductDescription e Features sono test di nodo.  
  
-   L'espressione di percorso relativo `child::root/child::Location[attribute::LocationID=10]`, contiene due passi separati da una barra. Il primo passo specifica un asse (`child`) e un test di nodo (`root`). Il secondo passo specifica tutti e tre i componenti di un passo dell'asse: un asse (child), un test di nodo (`Location`) e un predicato (`[attribute::LocationID=10]`).  
  
 Per altre informazioni sui componenti di un passo dell'asse, vedere [che specifica l'asse in un passo dell'espressione di percorso](../xquery/path-expressions-specifying-axis.md), [specificando i Test di nodo in un passo dell'espressione di percorso](../xquery/path-expressions-specifying-node-test.md), e [specifica di predicati in una Passo dell'espressione di percorso](../xquery/path-expressions-specifying-predicates.md).  
  
## <a name="general-step"></a>Passo generale  
 Un passo generale è semplicemente un'espressione che deve restituire una sequenza di nodi.  
  
 L'implementazione di XQuery in SQL Server supporta un passo generale come primo passo di un'espressione di percorso. Di seguito sono riportati alcuni esempi di espressioni di percorso che utilizzano passi generali.  
  
```  
(/a, /b)/c  
id(/a/b)  
```  
  
 Per altre informazioni sulla funzione id, vedere [funzione id &#40;XQuery&#41;](../xquery/functions-on-sequences-id.md).  
  
## <a name="in-this-section"></a>In questa sezione  
 [Definizione dell'asse in un passo dell'espressione di percorso](../xquery/path-expressions-specifying-axis.md)  
 Descrive l'utilizzo del passo dell'asse in un'espressione di percorso.  
  
 [Definizione di Test di nodo in un passo dell'espressione di percorso](../xquery/path-expressions-specifying-node-test.md)  
 Descrive l'utilizzo dei test di nodo in un'espressione di percorso.  
  
 [Specifica di predicati in un passo dell'espressione di percorso](../xquery/path-expressions-specifying-predicates.md)  
 Descrive l'utilizzo dei predicati in un'espressione di percorso.  
  
 [Utilizzo della sintassi abbreviata in un'espressione di percorso](../xquery/path-expressions-using-abbreviated-syntax.md)  
 Descrive l'utilizzo della sintassi abbreviata in un'espressione di percorso.  
  
  
