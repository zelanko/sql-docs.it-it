---
title: Specifica di un Test di nodo nel percorso (SQLXML 4.0) | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012670"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Specifica di un test di nodo nel percorso (SQLXML 4.0)
  Un test di nodo specifica il tipo di nodo selezionato dal passo. Ogni asse (`child`, `parent`, `attribute` o `self`) dispone di un tipo di nodo principale. Per il `attribute` asse, il tipo di nodo principale viene  **\<attributo >** . Per il `parent`, `child`, e `self` assi, il tipo di nodo principale viene  **\<elemento >** .  
  
> [!NOTE]  
>  Il test di nodo con carattere jolly *, ad esempio `child::*`, non è supportato.  
  
## <a name="node-test-example-1"></a>Test di nodo: Esempio 1  
 Percorso della posizione `child::Customer` seleziona  **\<cliente >** gli elementi figlio del nodo di contesto.  
  
 In questo esempio `child` è l'asse e `Customer` è il test di nodo. Il tipo di nodo principale per il `child` asse viene  **\<elemento >** . Pertanto, il test di nodo è TRUE se il  **\<cliente >** nodo è un  **\<elemento >** nodo. Se il nodo di contesto non dispone  **\<cliente >** elementi figlio, viene restituito un set di nodi vuoto.  
  
## <a name="node-test-example-2"></a>Test di nodo: Esempio 2  
 Percorso della posizione `attribute::CustomerID` consente di selezionare il **CustomerID** attributo del nodo di contesto.  
  
 Nell'esempio `attribute` è l'asse e `CustomerID` è il test di nodo. Il tipo di nodo principale di `attribute` asse viene  **\<attributo >** . Pertanto, il test di nodo è TRUE se **CustomerID** è un  **\<attributo >** nodo. Se il nodo di contesto non dispone **CustomerID**, viene restituito un set di nodi vuoto.  
  
> [!NOTE]  
>  In questa implementazione di XPath, se un passo si riferisce a un  **\<elemento >** o un'  **\<attributo >** tipo che non è dichiarato nello schema, viene generato un errore. a differenza di quanto avviene con l'implementazione di XPath in MSXML, che restituisce un set di nodi vuoto.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintassi abbreviata per gli assi  
 Per il percorso è supportata la sintassi abbreviata seguente:  
  
-   `attribute::` può essere abbreviato utilizzando `@`.  
  
     Il percorso `Customer[@CustomerID="ALFKI"]` è uguale a `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` può essere omesso da un passo.  
  
     In questo caso, `child` è l'asse predefinito. Il percorso `Customer/Order` è uguale a `child::Customer/child::Order`.  
  
-   `self::node()` può essere abbreviato utilizzando un punto (.), mentre `parent::node()` può essere abbreviato utilizzando due punti (..).  
  
  
