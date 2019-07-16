---
title: Esempio di Data Shaping | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a946329ad95a2b226f186e571152268baa5f37c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925660"
---
# <a name="data-shaping-example"></a>Esempio di data shaping
I seguenti dati di data shaping comando illustra come compilare un modello gerarchico **Recordset** dalle **clienti** e **ordini** tabelle nel database Northwind.  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 Quando questo comando consente di aprire una **Recordset** oggetto (come illustrato [Visual Basic riportato di Data Shaping](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)), viene creato un capitolo (**chapOrders**) per ogni record restituito dal **clienti** tabella. In questo capitolo è costituito da un subset del **Recordset** restituiti dal **ordini** tabella. Il **chapOrders** capitolo contiene tutte le informazioni richieste relative agli ordini effettuati dal cliente specificato. In questo esempio, il capitolo è costituito da tre colonne: **OrderID**, **OrderDate**, e **CustomerID**.  
  
 Le prime due voci di risultante data shaping **Recordset** sono i seguenti:  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria inferiore|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 In un comando SHAPE, Accodamento consente di creare un elemento figlio **Recordset** correlato al padre **Recordset** (come restituito dal comando specifico del provider immediatamente dopo la parola chiave forma cui avevo precedente) dalla clausola RELATE. L'elemento padre e figlio è in genere hanno almeno una colonna in comune: Il valore della colonna in una riga dell'elemento padre è identico al valore della colonna in tutte le righe dell'elemento figlio.  
  
 È possibile usare i comandi di forma secondo: vale a dire, per generare un elemento padre **Recordset** da un elemento figlio **Recordset**. I record nell'elemento figlio **Recordset** sono raggruppati, in genere con la clausola BY e una riga viene aggiunta all'elemento padre **Recordset** per ogni gruppo di nell'elemento figlio risulta. Se la clausola BY viene omessa, l'elemento figlio **Recordset** verranno form un singolo gruppo e l'elemento padre **Recordset** conterranno esattamente una riga. Ciò è utile per il calcolo di aggregazioni "totale complessivo" sull'intero figlio **Recordset**.  
  
 Il costrutto di comandi di forma consente inoltre di creare a livello di codice una data shaping **Recordset**. È quindi possibile accedere ai componenti del **Recordset** a livello di codice o tramite un controllo visuale appropriato. Viene eseguito un comando di forma come qualsiasi altro testo comando ADO. Per altre informazioni, vedere [forma comandi in genere](../../../ado/guide/data/shape-commands-in-general.md).  
  
 Indipendentemente dalla modalità padre **Recordset** è un formato, conterrà una colonna a capitoli che viene utilizzata per metterlo a un elemento figlio **Recordset**. Se si desidera, l'elemento padre **Recordset** può anche avere colonne che contengono funzioni di aggregazione (SUM, MIN, MAX e così via) nelle righe figlio. L'elemento padre sia l'elemento figlio **Recordset** può includere colonne che contengono un'espressione nella riga nel **Recordset**, nonché le colonne che sono nuovi e inizialmente vuota.  
  
 In questa sezione continua con l'argomento seguente.  
  
-   [Esempio di data shaping in Visual Basic](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
