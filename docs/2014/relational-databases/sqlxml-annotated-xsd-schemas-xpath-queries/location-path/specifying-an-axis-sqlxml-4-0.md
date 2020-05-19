---
title: Specifica di un asse (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 05891576872818e0d15d7bcae728dd3f19cdc252
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703088"
---
# <a name="specifying-an-axis-sqlxml-40"></a>Specifica di un asse (SQLXML 4.0)
    
-   L'asse specifica la relazione all'interno dell'albero tra i nodi selezionati dal passo e dal nodo di contesto. Sono supportati gli assi seguenti:  `child`  
  
     Contiene l'elemento figlio del nodo di contesto.  
  
     L'espressione XPath seguente (percorso) Seleziona dal nodo di contesto corrente tutti gli elementi figlio del ** \< cliente>** :  
  
    ```  
    child::Customer  
    ```  
  
     Nella query XPath seguente, `child` è l'asse. `Customer` è il test del nodo.  
  
-   `parent`  
  
     Contiene l'elemento padre del nodo di contesto.  
  
     L'espressione XPath seguente seleziona tutti gli elementi padre ** \<>del cliente** dell' ** \< ordine>** figli:  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     L'espressione equivale a specificare `child::Customer`. In questa query XPath, `child` e `parent` sono le assi. `Customer` e `Order` sono i test di nodo.  
  
-   `attribute`  
  
     Contiene l'attributo del nodo di contesto.  
  
     L'espressione XPath seguente seleziona l'attributo **CustomerID** del nodo di contesto:  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   `self`  
  
     Contiene il nodo di contesto stesso.  
  
     L'espressione XPath seguente seleziona il nodo corrente se si tratta dell' ** \< ordine>** nodo:  
  
    ```  
    self::Order  
    ```  
  
     Nella query XPath seguente `self` è l'asse e `Order` è il test di nodo.  
  
  
