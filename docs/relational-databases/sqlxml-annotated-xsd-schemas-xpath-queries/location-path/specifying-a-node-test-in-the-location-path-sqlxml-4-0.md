---
title: Specifica di un test di nodo nel percorso (SQLXML)
description: Informazioni su come specificare un test di nodo nel percorso di una query XPath 4,0 XPath.
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
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b8fdee8bdc7f3fbc3281ecab7682efdc8378bbdf
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97414822"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Specifica di un test di nodo nel percorso (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Un test di nodo specifica il tipo di nodo selezionato dal passo. Ogni asse (**figlio**, **padre**, **attributo** o **auto**) ha un tipo di nodo principale. Per l'asse degli **attributi** , il tipo di nodo principale è **\<attribute>** . Per gli assi **padre**, **figlio** e **self** , il tipo di nodo principale è **\<element>** .  
  
> [!NOTE]  
>  Il test di nodo con carattere jolly *, ad esempio `child::*`, non è supportato.  
  
## <a name="node-test-example-1"></a>Test del nodo: esempio 1  
 Il percorso `child::Customer` Seleziona gli **\<Customer>** elementi figlio del nodo di contesto.  
  
 In questo esempio `child` è l'asse e `Customer` è il test di nodo. Il tipo di nodo principale per l'asse **figlio** è **\<element>** . Pertanto, il test di nodo è TRUE se il **\<Customer>** nodo è un **\<element>** nodo. Se il nodo di contesto non dispone **\<Customer>** di elementi figlio, viene restituito un set di nodi vuoto.  
  
## <a name="node-test-example-2"></a>Test di nodo: esempio 2  
 Il percorso consente `attribute::CustomerID` di selezionare l'attributo **CustomerID** del nodo di contesto.  
  
 Nell'esempio `attribute` è l'asse e `CustomerID` è il test di nodo. Il tipo di nodo principale dell'asse dell' **attributo** è **\<attribute>** . Pertanto, il test di nodo è TRUE se **CustomerID** è un **\<attribute>** nodo. Se il nodo di contesto non dispone di **CustomerID**, viene restituito un set di nodi vuoto.  
  
> [!NOTE]  
>  In questa implementazione di XPath, se un passaggio del percorso si riferisce a un **\<element>** **\<attribute>** tipo o non dichiarato nello schema, viene generato un errore. a differenza di quanto avviene con l'implementazione di XPath in MSXML, che restituisce un set di nodi vuoto.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintassi abbreviata per gli assi  
 Per il percorso è supportata la sintassi abbreviata seguente:  
  
-   `attribute::` può essere abbreviato utilizzando `@`.  
  
     Il percorso `Customer[@CustomerID="ALFKI"]` è uguale a `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` può essere omesso da un passo.  
  
     Quindi, **child** è l'asse predefinito. Il percorso `Customer/Order` è uguale a `child::Customer/child::Order`.  
  
-   `self::node()` può essere abbreviato utilizzando un punto (.), mentre `parent::node()` può essere abbreviato utilizzando due punti (..).  
  
  
