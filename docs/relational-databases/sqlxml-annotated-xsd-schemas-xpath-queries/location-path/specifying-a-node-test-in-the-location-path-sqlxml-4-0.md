---
title: Specifica di un Test di nodo nel percorso (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8d0913a6066ddc0faec657a5e4857e206c227d5e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073300"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Specifica di un test di nodo nel percorso (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un test di nodo specifica il tipo di nodo selezionato dal passo. Ogni asse (**figlio**, **padre**, **attributo**, oppure **self**) dispone di un tipo di nodo principale. Per il **attributo** asse, il tipo di nodo principale viene  **\<attributo >** . Per il **padre**, **figlio**, e **self** assi, il tipo di nodo principale è  **\<elemento >** .  
  
> [!NOTE]  
>  Il test di nodo con carattere jolly *, ad esempio `child::*`, non è supportato.  
  
## <a name="node-test-example-1"></a>Test di nodo: Esempio 1  
 Percorso della posizione `child::Customer` seleziona  **\<cliente >** gli elementi figlio del nodo di contesto.  
  
 In questo esempio `child` è l'asse e `Customer` è il test di nodo. Il tipo di nodo principale per il **figlio** asse viene  **\<elemento >** . Pertanto, il test di nodo è TRUE se il  **\<cliente >** nodo è un  **\<elemento >** nodo. Se il nodo di contesto non dispone  **\<cliente >** elementi figlio, viene restituito un set di nodi vuoto.  
  
## <a name="node-test-example-2"></a>Test di nodo: Esempio 2  
 Percorso della posizione `attribute::CustomerID` consente di selezionare il **CustomerID** attributo del nodo di contesto.  
  
 Nell'esempio `attribute` è l'asse e `CustomerID` è il test di nodo. Il tipo di nodo principale di **attributo** asse viene  **\<attributo >** . Pertanto, il test di nodo è TRUE se **CustomerID** è un  **\<attributo >** nodo. Se il nodo di contesto non dispone **CustomerID**, viene restituito un set di nodi vuoto.  
  
> [!NOTE]  
>  In questa implementazione di XPath, se un passo si riferisce a un  **\<elemento >** o un'  **\<attributo >** tipo che non è dichiarato nello schema, viene generato un errore. a differenza di quanto avviene con l'implementazione di XPath in MSXML, che restituisce un set di nodi vuoto.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintassi abbreviata per gli assi  
 Per il percorso è supportata la sintassi abbreviata seguente:  
  
-   `attribute::` può essere abbreviato utilizzando `@`.  
  
     Il percorso `Customer[@CustomerID="ALFKI"]` è uguale a `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` può essere omesso da un passo.  
  
     Pertanto **figlio** è l'asse predefinito. Il percorso `Customer/Order` è uguale a `child::Customer/child::Order`.  
  
-   `self::node()` può essere abbreviato utilizzando un punto (.), mentre `parent::node()` può essere abbreviato utilizzando due punti (..).  
  
  
