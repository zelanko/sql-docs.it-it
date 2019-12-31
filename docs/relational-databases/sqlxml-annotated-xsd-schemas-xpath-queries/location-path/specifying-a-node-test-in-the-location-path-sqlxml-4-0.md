---
title: Specifica di un test di nodo nel percorso (SQLXML)
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f94f155ee86df6daf0c039a18f27c30e294d57df
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254742"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Specifica di un test di nodo nel percorso (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un test di nodo specifica il tipo di nodo selezionato dal passo. Ogni asse (**figlio**, **padre**, **attributo**o **auto**) ha un tipo di nodo principale. Per l'asse degli **attributi** , il tipo di nodo principale è ** \<attribute>**. Per gli assi **padre**, **figlio**e **self** , il tipo di nodo principale è ** \<elemento>**.  
  
> [!NOTE]  
>  Il test di nodo con carattere jolly *, ad esempio `child::*`, non è supportato.  
  
## <a name="node-test-example-1"></a>Test del nodo: esempio 1  
 Il percorso `child::Customer` seleziona ** \<il cliente>** elementi figlio del nodo di contesto.  
  
 In questo esempio `child` è l'asse e `Customer` è il test di nodo. Il tipo di nodo principale per l'asse **figlio** è ** \<>elemento **. Pertanto, il test di nodo è true se il ** \<nodo Customer>** è un ** \<elemento>** nodo. Se il nodo di contesto non ha alcun ** \<cliente>** figli, viene restituito un set di nodi vuoto.  
  
## <a name="node-test-example-2"></a>Test di nodo: esempio 2  
 Il percorso `attribute::CustomerID` consente di selezionare l'attributo **CustomerID** del nodo di contesto.  
  
 Nell'esempio `attribute` è l'asse e `CustomerID` è il test di nodo. Il tipo di nodo principale dell'asse dell' **attributo** è ** \<>attributo **. Pertanto, il test di nodo è true se **CustomerID** è un ** \<attributo>** nodo. Se il nodo di contesto non dispone di **CustomerID**, viene restituito un set di nodi vuoto.  
  
> [!NOTE]  
>  In questa implementazione di XPath, se un passaggio del percorso fa riferimento a un ** \<elemento>** o a un ** \<** tipo di>di attributo non dichiarato nello schema, viene generato un errore. a differenza di quanto avviene con l'implementazione di XPath in MSXML, che restituisce un set di nodi vuoto.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintassi abbreviata per gli assi  
 Per il percorso è supportata la sintassi abbreviata seguente:  
  
-   
  `attribute::` può essere abbreviato utilizzando `@`.  
  
     Il percorso `Customer[@CustomerID="ALFKI"]` è uguale a `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   
  `child::` può essere omesso da un passo.  
  
     Quindi, **child** è l'asse predefinito. Il percorso `Customer/Order` è uguale a `child::Customer/child::Order`.  
  
-   
  `self::node()` può essere abbreviato utilizzando un punto (.), mentre `parent::node()` può essere abbreviato utilizzando due punti (..).  
  
  
