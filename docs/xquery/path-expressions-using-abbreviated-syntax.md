---
title: Uso della sintassi abbreviata in un'espressione di percorso | Microsoft Docs
description: Informazioni su come utilizzare la sintassi abbreviata nelle espressioni di percorso XQuery.
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
ms.openlocfilehash: eeb7026f341af60f289a1d3854e24656073add61
ms.sourcegitcommit: 6593b3b6365283bb76c31102743cdccc175622fe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84306010"
---
# <a name="path-expressions---using-abbreviated-syntax"></a>Espressioni di percorso - Uso di sintassi abbreviata
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Tutti gli esempi di [informazioni sulle espressioni di percorso in XQuery utilizzano la](../xquery/path-expressions-xquery.md) sintassi non abbreviata per le espressioni di percorso. La sintassi non abbreviata per un passo dell'asse in un'espressione di percorso include il nome dell'asse e il test di nodo, separati da una coppia di due punti e seguiti da zero o più qualificatori di passo.  
  
 Ad esempio:  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 Nelle espressioni di percorso, XQuery supporta le abbreviazioni seguenti:  
  
-   L'asse **figlio** è l'asse predefinito. Pertanto, l'asse **child::** può essere omesso da un passaggio in un'espressione. Ad esempio, è possibile scrivere `/child::ProductDescription/child::Summary` nel formato `/ProductDescription/Summary`.  
  
-   Un asse dell' **attributo** può essere abbreviato come @ . Ad esempio, è possibile scrivere `/child::ProductDescription[attribute::ProductModelID=10]` nel formato `/ProudctDescription[@ProductModelID=10]`.  
  
-   Un **/descendant-or-self:: node ()/** può essere abbreviato come//. Ad esempio, è possibile scrivere `/descendant-or-self::node()/child::act:telephoneNumber` nel formato `//act:telephoneNumber`.  
  
     La query precedente recupera tutti i numeri di telefono archiviati nella colonna AdditionalContactInfo della tabella Contact. Lo schema per AdditionalContactInfo viene definito in modo che un \<telephoneNumber> elemento possa essere visualizzato in qualsiasi punto del documento. Per recuperare tutti i numeri di telefono, pertanto, è necessario eseguire la ricerca in ogni nodo del documento. La ricerca inizia alla radice del documento e continua in tutti i nodi discendenti.  
  
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
  
-   **Self:: node ()** in un passaggio può essere abbreviato in un singolo punto (.). Tuttavia, il punto non è equivalente o interscambiabile con l'operatore **self:: node ()**.  
  
     Ad esempio, nella query seguente, l'utilizzo di un punto rappresenta un valore e non un nodo:  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   L' **elemento padre:: node ()** in un passaggio può essere abbreviato in un punto doppio (..).  
  
  
