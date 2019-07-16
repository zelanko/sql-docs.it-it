---
title: Uso di sintassi in un'espressione di percorso abbreviata | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e75db08f283631cf9b5daf064790786a1abc10f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946410"
---
# <a name="path-expressions---using-abbreviated-syntax"></a>Espressioni di percorso - Uso di sintassi abbreviata
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Tutti gli esempi [espressioni di percorso in XQuery](../xquery/path-expressions-xquery.md) utilizzata la sintassi abbreviata per le espressioni di percorso. La sintassi non abbreviata per un passo dell'asse in un'espressione di percorso include il nome dell'asse e il test di nodo, separati da una coppia di due punti e seguiti da zero o più qualificatori di passo.  
  
 Ad esempio:  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 Nelle espressioni di percorso, XQuery supporta le abbreviazioni seguenti:  
  
-   Il **figlio** asse è l'asse predefinito. Pertanto, il **figlio::** asse può essere omesso da un passaggio in un'espressione. Ad esempio, è possibile scrivere `/child::ProductDescription/child::Summary` nel formato `/ProductDescription/Summary`.  
  
-   Un' **attributo** asse può essere abbreviato in @. Ad esempio, è possibile scrivere `/child::ProductDescription[attribute::ProductModelID=10]` nel formato `/ProudctDescription[@ProductModelID=10]`.  
  
-   Oggetto **descendant-or-self::node()/** può essere abbreviato in / /. Ad esempio, è possibile scrivere `/descendant-or-self::node()/child::act:telephoneNumber` nel formato `//act:telephoneNumber`.  
  
     La query precedente recupera tutti i numeri di telefono archiviati nella colonna AdditionalContactInfo della tabella Contact. Lo schema per la colonna AdditionalContactInfo viene definito in modo che un \<telephoneNumber > elemento può essere visualizzato in qualsiasi punto del documento. Per recuperare tutti i numeri di telefono, pertanto, è necessario eseguire la ricerca in ogni nodo del documento. La ricerca inizia alla radice del documento e continua in tutti i nodi discendenti.  
  
     La query seguente recupera tutti i numeri di telefono relativi a un contatto di un cliente specifico:  
  
    ```  
    SELECT AdditionalContactInfo.query('             
                declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";             
                declare namespace crm="https://schemas.adventure-works.com/Contact/Record";             
                declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";             
                /descendant-or-self::node()/child::act:telephoneNumber             
                ') as result             
    FROM Person.Contact             
    WHERE ContactID=1             
    ```  
  
     Se si sostituisce l'espressione di percorso con la sintassi abbreviata `//act:telephoneNumber`, si ottengono gli stessi risultati.  
  
-   Il **self:: node ()** in un passaggio può essere abbreviato utilizzando un punto singolo (.). Tuttavia, il punto non è equivalente o interscambiabile con il **self:: node ()** .  
  
     Ad esempio, nella query seguente, l'utilizzo di un punto rappresenta un valore e non un nodo:  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   Il **padre:: node ()** in un passaggio può essere abbreviato utilizzando un doppio punto (.).  
  
  
