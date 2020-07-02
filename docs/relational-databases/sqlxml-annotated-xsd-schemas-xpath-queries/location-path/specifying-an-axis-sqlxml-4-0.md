---
title: Specifica di un asse (SQLXML)
description: Informazioni su come specificare un asse in una query XPath 4,0 XPath specifica la relazione di struttura ad albero tra i nodi selezionati dal location step e il nodo di contesto.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], axes
- XPath queries [SQLXML], location paths
- self axis
- attribute axis [SQLXML]
- axis [SQLXML]
- child axis
- parent axis
- location path for XPath query
- axes [SQLXML]
ms.assetid: 65631795-3389-40cf-90ea-85e9438956c5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: df40d531bcb9c1fddcad5d78cd76ca98831834ea
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85649732"
---
# <a name="specifying-an-axis-sqlxml-40"></a>Specifica di un asse (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
    
-   L'asse specifica la relazione all'interno dell'albero tra i nodi selezionati dal passo e dal nodo di contesto. Sono supportati gli assi seguenti: **figlio**  
  
     Contiene l'elemento figlio del nodo di contesto.  
  
     L'espressione XPath seguente (percorso) Seleziona dal nodo di contesto corrente tutti gli **\<Customer>** elementi figlio:  
  
    ```  
    child::Customer  
    ```  
  
     Nella query XPath seguente, `child` è l'asse. `Customer` è il test del nodo.  
  
-   **padre**  
  
     Contiene l'elemento padre del nodo di contesto.  
  
     L'espressione XPath seguente seleziona tutti gli **\<Customer>** elementi padre degli **\<Order>** elementi figlio:  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     L'espressione equivale a specificare `child::Customer`. In questa query XPath, `child` e `parent` sono le assi. `Customer` e `Order` sono i test di nodo.  
  
-   **attributo**  
  
     Contiene l'attributo del nodo di contesto.  
  
     L'espressione XPath seguente seleziona l'attributo **CustomerID** del nodo di contesto:  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **auto**  
  
     Contiene il nodo di contesto stesso.  
  
     L'espressione XPath seguente seleziona il nodo corrente se si tratta del **\<Order>** nodo:  
  
    ```  
    self::Order  
    ```  
  
     Nella query XPath seguente `self` è l'asse e `Order` è il test di nodo.  
  
  
