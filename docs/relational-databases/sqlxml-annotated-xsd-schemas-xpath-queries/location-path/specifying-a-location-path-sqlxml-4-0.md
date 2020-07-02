---
title: Specifica di un percorso (SQLXML)
description: Informazioni su come specificare un percorso in una query XPath di SQLXML 4,0 per selezionare un set di nodi relativo al nodo di contesto e generare un set di nodi.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- absolute location path
- node-set [SQLXML]
- XPath queries [SQLXML], location paths
- relative location path [SQLXML]
- location path for XPath query
ms.assetid: a23a2b75-bc69-49f0-99db-05e14dc15bc0
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9f5793bef7a6b025198972b1be40fc9f482fd53c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85649740"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>Definizione di un percorso (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Le query XPath vengono specificate sotto forma di espressione. Sono disponibili diversi tipi di espressioni. Un percorso è un'espressione che seleziona un set di nodi relativo al nodo di contesto. Il risultato della valutazione di un percorso è un set di nodi.  
  
## <a name="types-of-location-paths"></a>Tipi di percorsi  
 È possibile definire un percorso in una delle forme seguenti:  
  
-   **Percorso assoluto**  
  
     Un percorso assoluto inizia in corrispondenza del nodo radice del documento ed è costituito da una barra (/), eventualmente seguita da un percorso relativo. La barra (/) seleziona il nodo radice del documento.  
  
-   **Percorso relativo**  
  
     Un percorso relativo inizia in corrispondenza del nodo di contesto nel documento. Un percorso è costituito da una sequenza di uno o più passi separati da una barra (/). Ogni passo seleziona un set di nodi relativi al nodo di contesto. La sequenza iniziale dei passi seleziona un set di nodi relativi a un nodo di contesto. Ogni nodo nel set viene utilizzato come nodo di contesto per il passo successivo. I set di nodi identificati dal passo vengono uniti in join. Ad esempio, **child:: Order/child:: OrderDetail** seleziona gli **\<OrderDetail>** elementi figlio degli **\<Order>** elementi figlio del nodo di contesto.  
  
    > [!NOTE]  
    >  Nell'implementazione SQLXML 4.0 di XPath, ogni query XPath inizia in corrispondenza del contesto radice, anche se XPath non è assoluto in modo esplicito. Una query XPath che inizia con "Customer", ad esempio, viene considerata come "/Customer". Nella query XPath **Customer [Order]** il cliente inizia in corrispondenza del contesto radice, ma Order inizia in corrispondenza del contesto del cliente. Per ulteriori informazioni, vedere [Introduzione all'utilizzo di query XPath &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="location-steps"></a>Passi  
 Un percorso (assoluto o relativo) è costituito da passi che contengono tre parti:  
  
-   **Asse**  
  
     L'asse specifica la relazione all'interno dell'albero tra i nodi selezionati dal passo e dal nodo di contesto. Gli assi **padre**, **figlio**, **attributo**e **self** sono supportati. Se un asse **figlio** viene specificato nel percorso, tutti i nodi selezionati dalla query sono gli elementi figlio del nodo di contesto. Se viene specificato un asse **padre** , il nodo selezionato corrisponde al nodo padre del nodo di contesto. Se viene specificato un asse degli **attributi** , i nodi selezionati sono gli attributi del nodo di contesto.  
  
-   **Test di nodo**  
  
     Un test di nodo specifica il tipo di nodo selezionato dal passo. Ogni asse (**figlio**, **padre**, **attributo**e **auto**) ha un tipo di nodo principale. Per l'asse degli **attributi** , il tipo di nodo principale è **\<attribute>** . Per gli assi **padre**, **figlio**e **self** , il tipo di nodo principale è **\<element>** .  
  
     Se, ad esempio, il percorso specifica **child:: Customer**, **\<Customer>** verranno selezionati gli elementi figlio del nodo di contesto. Poiché l'asse **figlio** ha **\<element>** come tipo di nodo principale, il test di nodo Customer è true se Customer è un **\<element>** nodo.  
  
-   **Predicati di selezione (zero o più predicati)**  
  
     Un predicato filtra un set di nodi rispetto a un asse. La definizione di predicati di selezione in un'espressione XPath è un'operazione simile alla definizione di una clausola WHERE in un'istruzione SELECT. Il predicato viene specificato tra parentesi. L'applicazione del test specificato nei predicati di selezione filtra i nodi restituiti dal test di nodo. Per filtrare ogni nodo nel set di nodi, l'espressione del predicato viene valutata con il nodo come nodo di contesto e con il numero di nodi nel set di nodi come dimensioni del contesto. Se l'espressione del predicato restituisce TRUE per il nodo, il nodo viene incluso nel set di nodi risultante.  
  
     La sintassi per un passo è costituita dal nome dell'asse e dal test di nodo separati da due caratteri due punti (::), seguiti da zero o più espressioni, ciascuna tra parentesi quadre. Ad esempio, l'espressione XPath (percorso) **child:: Customer [ @CustomerID =' ALFKI ']** seleziona tutti gli **\<Customer>** elementi figlio del nodo di contesto. Il test nel predicato viene quindi applicato al set di nodi, che restituisce solo i **\<Customer>** nodi degli elementi con il valore di attributo ' ALFKI ' per il relativo attributo **CustomerID** .  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Specifica di un asse &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-an-axis-sqlxml-4-0.md)  
 Vengono forniti esempi di definizione di un asse.  
  
 [Specifica di un test di nodo nel percorso &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 Vengono forniti esempi di definizione di un test di nodo.  
  
 [Specifica di predicati di selezione nel percorso &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 Vengono forniti esempi di definizione di predicati di selezione.  
  
  
