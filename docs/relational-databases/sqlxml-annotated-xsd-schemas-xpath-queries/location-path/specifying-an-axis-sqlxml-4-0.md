---
title: Specifica un asse (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 29d97b92f6979a7e5bbc67185f6e5a47ff82af68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073278"
---
# <a name="specifying-an-axis-sqlxml-40"></a>Specifica di un asse (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
-   L'asse specifica la relazione all'interno dell'albero tra i nodi selezionati dal passo e dal nodo di contesto. Sono supportati gli assi seguenti: **figlio**  
  
     Contiene l'elemento figlio del nodo di contesto.  
  
     L'espressione XPath seguente (percorso) seleziona dal nodo di contesto corrente tutti i  **\<cliente >** figli:  
  
    ```  
    child::Customer  
    ```  
  
     Nella query XPath seguente, `child` è l'asse. `Customer` è il test del nodo.  
  
-   **parent**  
  
     Contiene l'elemento padre del nodo di contesto.  
  
     L'espressione XPath seguente seleziona tutti i  **\<cliente >** padri del  **\<ordine >** figli:  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     L'espressione equivale a specificare `child::Customer`. In questa query XPath, `child` e `parent` sono le assi. `Customer` e `Order` sono i test di nodo.  
  
-   **attribute**  
  
     Contiene l'attributo del nodo di contesto.  
  
     L'espressione XPath seguente seleziona il **CustomerID** attributo del nodo di contesto:  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **self**  
  
     Contiene il nodo di contesto stesso.  
  
     L'espressione XPath seguente seleziona il nodo corrente se è il  **\<ordine >** nodo:  
  
    ```  
    self::Order  
    ```  
  
     Nella query XPath seguente `self` è l'asse e `Order` è il test di nodo.  
  
  
