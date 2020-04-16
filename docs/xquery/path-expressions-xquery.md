---
title: Espressioni di percorso (XQuery) Documenti Microsoft
description: Informazioni su come le espressioni di percorso XQuery individuano i nodi, ad esempio i nodi elemento, attributo e testo, in un documento.
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
ms.openlocfilehash: 0e4c87a0695c57461f444c8be4318bcd06cfdefe
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388063"
---
# <a name="path-expressions-xquery"></a>Espressioni di percorso (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Le espressioni di percorso XQuery consentono di individuare nodi, ad esempio di testo, attributo o elemento, all'interno di un documento. Il risultato di un'espressione di percorso è sempre nell'ordine del documento, senza nodi duplicati nella sequenza risultante. Nello specificare un percorso è possibile utilizzare la sintassi abbreviata o non abbreviata. Le informazioni seguenti sono relative alla sintassi non abbreviata. La sintassi abbreviata è descritta di seguito in questo argomento.  
  
> [!NOTE]  
>  Poiché le query di esempio in questo argomento vengono specificate in base alle colonne di tipo **xml,** **CatalogDescription** e **Instructions**, nella tabella **ProductModel,** è necessario acquisire familiarità con il contenuto e la struttura dei documenti XML archiviati in queste colonne.  
  
 Esistono espressioni di percorso relativo ed espressioni di percorso assoluto. Di seguito vengono descritti ambedue i tipi di espressione:  
  
-   Un'espressione di percorso relativo è costituita da uno o più passi separati da una o due barre (/ o //). Ad esempio, `child::Features` è un'espressione di percorso relativo in cui `Child` si riferisce solo ai nodi figlio del nodo di contesto attualmente elaborato. L'espressione recupera \<le caratteristiche> nodo elemento del nodo di contesto.  
  
-   Un'espressione di percorso assoluto inizia con una o due barre (/ o //), seguite da un percorso relativo facoltativo. Ad esempio, la barra iniziale nell'espressione `/child::ProductDescription` indica che si tratta di un'espressione di percorso assoluto. Poiché una barra all'inizio di un'espressione restituisce il nodo radice \<del documento del nodo di contesto, l'espressione restituisce tutti i ProductDescription> nodo elemento della radice del documento.  
  
     Se un percorso assoluto inizia con una sola barra, può essere o meno seguito da un percorso relativo. Se si specifica una sola barra, l'espressione restituisce il nodo radice del nodo di contesto. Per un tipo di dati XML, si tratta del nodo del documento.  
  
 Una tipica espressione di percorso è costituita da passi. Ad esempio, l'espressione `/child::ProductDescription/child::Summary`di percorso assoluto, ,contiene due passaggi separati da una barra.  
  
-   Il primo passaggio \<recupera il ProductDescription> elemento figli della radice del documento.  
  
-   Il secondo passaggio \<recupera il Summary> \<element node children per ogni nodo elemento ProductDescription temato> nodo elemento, che a sua volta diventa il nodo di contesto.  
  
 Un passo in un'espressione di percorso può essere un passo dell'asse o un passo generale.  
  
## <a name="axis-step"></a>Passo dell'asse  
 Un passo dell'asse in un'espressione di percorso è composto dalle parti seguenti.  
  
 [Asse](../xquery/path-expressions-specifying-axis.md)  
 Definisce la direzione di spostamento. Un passo dell'asse in un'espressione di percorso che inizia dal nodo di contesto e si sposta ai nodi raggiungibili nella direzione specificata dall'asse.  
  
 [test del nodo](../xquery/path-expressions-specifying-node-test.md)  
 Specifica il tipo di nodo o i nomi dei nodi da selezionare.  
  
 Zero o più predicati facoltativi  
 Filtrano i nodi selezionandone alcuni e scartandone altri.  
  
 Negli esempi seguenti viene utilizzato un **passaggio dell'asse** nelle espressioni di percorso:The following examples use an axisstep in the path expressions:  
  
-   L'espressione di percorso assoluto `/child::ProductDescription` contiene un solo passo. Specifica un asse (`child`) e un test di nodo (`ProductDescription`).  
  
-   L'espressione di percorso relativo `child::ProductDescription/child::Features` contiene due passi separati da una barra. Entrambi i passi specificano un asse child. ProductDescription e Features sono test di nodo.  
  
-   L'espressione di `child::root/child::Location[attribute::LocationID=10]`percorso relativo, ,contiene due passaggi separati da una barra. Il primo passo specifica un asse (`child`) e un test di nodo (`root`). Il secondo passo specifica tutti e tre i componenti di un passo dell'asse: un asse (child), un test di nodo (`Location`) e un predicato (`[attribute::LocationID=10]`).  
  
 Per ulteriori informazioni sui componenti di un passaggio dell'asse, vedere [Specifica dell'asse in un passaggio dell'espressione](../xquery/path-expressions-specifying-axis.md)di percorso , Specifica del test dei nodi in un [passaggio dell'espressione](../xquery/path-expressions-specifying-node-test.md)di percorso e Specifica dei [predicati in un passaggio dell'espressione](../xquery/path-expressions-specifying-predicates.md)di percorso.  
  
## <a name="general-step"></a>Passo generale  
 Un passo generale è semplicemente un'espressione che deve restituire una sequenza di nodi.  
  
 L'implementazione di XQuery in SQL Server supporta un passo generale come primo passo di un'espressione di percorso. Di seguito sono riportati alcuni esempi di espressioni di percorso che utilizzano passi generali.  
  
```  
(/a, /b)/c  
id(/a/b)  
```  
  
 Per ulteriori informazioni sulla funzione id, vedere [Funzione id &#40;xQuery&#41;](../xquery/functions-on-sequences-id.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Definizione dell'asse in un passo dell'espressione di percorso](../xquery/path-expressions-specifying-axis.md)  
 Descrive l'utilizzo del passo dell'asse in un'espressione di percorso.  
  
 [Definizione del test di nodo in un passo dell'espressione di percorso](../xquery/path-expressions-specifying-node-test.md)  
 Descrive l'utilizzo dei test di nodo in un'espressione di percorso.  
  
 [Specifica di predicati in un passo dell'espressione di percorso](../xquery/path-expressions-specifying-predicates.md)  
 Descrive l'utilizzo dei predicati in un'espressione di percorso.  
  
 [Utilizzo della sintassi abbreviata in un'espressione di percorso](../xquery/path-expressions-using-abbreviated-syntax.md)  
 Descrive l'utilizzo della sintassi abbreviata in un'espressione di percorso.  
  
  
