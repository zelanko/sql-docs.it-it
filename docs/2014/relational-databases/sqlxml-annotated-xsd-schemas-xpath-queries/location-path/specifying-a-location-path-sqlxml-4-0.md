---
title: Specifica di un percorso (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d769bbb8c1d3890f80c89c32e7ddfc913dd517a8
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703107"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>Definizione di un percorso (SQLXML 4.0)
  Le query XPath vengono specificate sotto forma di espressione. Sono disponibili diversi tipi di espressioni. Un percorso è un'espressione che seleziona un set di nodi relativo al nodo di contesto. Il risultato della valutazione di un percorso è un set di nodi.  
  
## <a name="types-of-location-paths"></a>Tipi di percorsi  
 È possibile definire un percorso in una delle forme seguenti:  
  
-   **Percorso assoluto**  
  
     Un percorso assoluto inizia in corrispondenza del nodo radice del documento ed è costituito da una barra (/), eventualmente seguita da un percorso relativo. La barra (/) seleziona il nodo radice del documento.  
  
-   **Percorso relativo**  
  
     Un percorso relativo inizia in corrispondenza del nodo di contesto nel documento. Un percorso è costituito da una sequenza di uno o più passi separati da una barra (/). Ogni passo seleziona un set di nodi relativi al nodo di contesto. La sequenza iniziale dei passi seleziona un set di nodi relativi a un nodo di contesto. Ogni nodo nel set viene utilizzato come nodo di contesto per il passo successivo. I set di nodi identificati dal passo vengono uniti in join. Ad esempio, **child:: Order/child:: OrderDetail** seleziona ** \< OrderDetail>** elemento figlio dell' ** \< ordine>** elementi figlio del nodo di contesto.  
  
    > [!NOTE]  
    >  Nell'implementazione SQLXML 4.0 di XPath, ogni query XPath inizia in corrispondenza del contesto radice, anche se XPath non è assoluto in modo esplicito. Una query XPath che inizia con "Customer", ad esempio, viene considerata come "/Customer". Nella query XPath **Customer [Order]** il cliente inizia in corrispondenza del contesto radice, ma Order inizia in corrispondenza del contesto del cliente. Per ulteriori informazioni, vedere [Introduzione all'utilizzo di query XPath &#40;SQLXML 4,0&#41;](../introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="location-steps"></a>Passi  
 Un percorso (assoluto o relativo) è costituito da passi che contengono tre parti:  
  
-   **Asse**  
  
     L'asse specifica la relazione all'interno dell'albero tra i nodi selezionati dal passo e dal nodo di contesto. Sono supportati gli assi `parent`, `child`, `attribute` e `self`. Se nel percorso viene specificato un asse `child`, tutti i nodi selezionati dalla query sono figli del nodo di contesto. Se viene specificato un asse `parent`, il nodo selezionato è il nodo padre del nodo di contesto. Se viene specificato un asse `attribute`, i nodi selezionati sono gli attributi del nodo di contesto.  
  
-   **Test di nodo**  
  
     Un test di nodo specifica il tipo di nodo selezionato dal passo. Ogni asse, `child`, `parent`, `attribute` e `self`, è associato a un tipo di nodo principale. Per l' `attribute` asse, il tipo di nodo principale è ** \< attribute>**. Per gli `parent` `child` assi, e `self` , il tipo di nodo principale è ** \< elemento>**.  
  
     Se, ad esempio, il percorso specifica **child:: Customer**, verranno selezionati gli elementi figlio del ** \<>Customer** del nodo di contesto. Poiché l' `child` asse ha ** \<>elemento** come tipo di nodo principale, il test di nodo Customer è true se Customer è un ** \< elemento>** nodo.  
  
-   **Predicati di selezione (zero o più predicati)**  
  
     Un predicato filtra un set di nodi rispetto a un asse. La definizione di predicati di selezione in un'espressione XPath è un'operazione simile alla definizione di una clausola WHERE in un'istruzione SELECT. Il predicato viene specificato tra parentesi. L'applicazione del test specificato nei predicati di selezione filtra i nodi restituiti dal test di nodo. Per filtrare ogni nodo nel set di nodi, l'espressione del predicato viene valutata con il nodo come nodo di contesto e con il numero di nodi nel set di nodi come dimensioni del contesto. Se l'espressione del predicato restituisce TRUE per il nodo, il nodo viene incluso nel set di nodi risultante.  
  
     La sintassi per un passo è costituita dal nome dell'asse e dal test di nodo separati da due caratteri due punti (::), seguiti da zero o più espressioni, ciascuna tra parentesi quadre. Ad esempio, l'espressione XPath (percorso) **child:: Customer [ @CustomerID =' ALFKI ']** seleziona tutti gli elementi figlio del ** \<>Customer** del nodo di contesto. Il test nel predicato viene quindi applicato al set di nodi, che restituisce solo i nodi elemento ** \<>del cliente** con valore di attributo ' ALFKI ' per il relativo attributo **CustomerID** .  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Specifica di un asse &#40;SQLXML 4,0&#41;](specifying-an-axis-sqlxml-4-0.md)  
 Vengono forniti esempi di definizione di un asse.  
  
 [Specifica di un test di nodo nel percorso &#40;SQLXML 4,0&#41;](specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 Vengono forniti esempi di definizione di un test di nodo.  
  
 [Specifica di predicati di selezione nel percorso &#40;SQLXML 4,0&#41;](specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 Vengono forniti esempi di definizione di predicati di selezione.  
  
  
