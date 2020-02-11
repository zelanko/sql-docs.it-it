---
title: Specifica di un test di nodo nel percorso (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d0a3dd41259bcbf2567d34a86527865de011faf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66012670"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Specifica di un test di nodo nel percorso (SQLXML 4.0)
  Un test di nodo specifica il tipo di nodo selezionato dal passo. Ogni asse (`child`, `parent`, `attribute` o `self`) dispone di un tipo di nodo principale. Per l' `attribute` asse, il tipo di nodo principale è ** \<attribute>**. Per gli `parent`assi `child`, e `self` , il tipo di nodo principale è ** \<elemento>**.  
  
> [!NOTE]  
>  Il test di nodo con carattere jolly *, ad esempio `child::*`, non è supportato.  
  
## <a name="node-test-example-1"></a>Test del nodo: esempio 1  
 Il percorso `child::Customer` seleziona ** \<il cliente>** elementi figlio del nodo di contesto.  
  
 In questo esempio `child` è l'asse e `Customer` è il test di nodo. Il tipo di nodo principale per `child` l'asse è ** \<>elemento **. Pertanto, il test di nodo è true se il ** \<nodo Customer>** è un ** \<elemento>** nodo. Se il nodo di contesto non ha alcun ** \<cliente>** figli, viene restituito un set di nodi vuoto.  
  
## <a name="node-test-example-2"></a>Test di nodo: esempio 2  
 Il percorso `attribute::CustomerID` consente di selezionare l'attributo **CustomerID** del nodo di contesto.  
  
 Nell'esempio `attribute` è l'asse e `CustomerID` è il test di nodo. Il tipo di nodo principale dell' `attribute` asse è ** \<>attributo **. Pertanto, il test di nodo è true se **CustomerID** è un ** \<attributo>** nodo. Se il nodo di contesto non dispone di **CustomerID**, viene restituito un set di nodi vuoto.  
  
> [!NOTE]  
>  In questa implementazione di XPath, se un passaggio del percorso fa riferimento a un ** \<elemento>** o a un ** \<** tipo di>di attributo non dichiarato nello schema, viene generato un errore. a differenza di quanto avviene con l'implementazione di XPath in MSXML, che restituisce un set di nodi vuoto.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintassi abbreviata per gli assi  
 Per il percorso è supportata la sintassi abbreviata seguente:  
  
-   
  `attribute::` può essere abbreviato utilizzando `@`.  
  
     Il percorso `Customer[@CustomerID="ALFKI"]` è uguale a `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   
  `child::` può essere omesso da un passo.  
  
     In questo caso, `child` è l'asse predefinito. Il percorso `Customer/Order` è uguale a `child::Customer/child::Order`.  
  
-   
  `self::node()` può essere abbreviato utilizzando un punto (.), mentre `parent::node()` può essere abbreviato utilizzando due punti (..).  
  
  
