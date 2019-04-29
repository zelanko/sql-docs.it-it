---
title: Sequenze di escape in ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3866a45a2b55a5372769eacc0bb6b0eb1e5c088f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62942974"
---
# <a name="escape-sequences-in-odbc"></a>Sequenze di escape in ODBC
Un numero di funzionalità del linguaggio, ad esempio gli outer join e le chiamate di funzione scalare, è in genere implementato dai sistemi DBMS. Tuttavia, la sintassi per queste funzionalità tendono a essere specifici del DBMS, anche quando la sintassi standard sono definita da vari organismi standard. Per questo motivo, ODBC definisce sequenze di escape contenenti le sintassi standard per le funzionalità del linguaggio seguenti:  
  
-   Valori letterali di intervallo di date, time, timestamp e datetime  
  
-   Funzioni scalari, ad esempio numerici, stringa e funzioni di conversione di tipi di dati  
  
-   COME carattere di escape nel predicato  
  
-   Outer join  
  
-   Chiamate di procedura  
  
 La sequenza di escape utilizzata da ODBC è il seguente:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Note  
 La sequenza di escape viene riconosciuta e analizzata dal driver, che sostituiscono le sequenze di escape con la grammatica per DBMS specifici. Per altre informazioni sulla sintassi della sequenza di escape, vedere [sequenze di Escape ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) nell'appendice c: Grammatica SQL.  
  
> [!NOTE]  
>  In ODBC 2. *x*, questo era la sintassi standard della sequenza di escape: **-(\*vendor (**_-nome del fornitore_**), prodotto (** _-nome del prodotto_**)**_estensione_  **\*):**  
>   
>  Oltre a questa sintassi, è stata definita una sintassi abbreviata nel formato: **{**_estensione_**}**  
>   
>  In ODBC 3. *x*, la forma estesa della sequenza di escape è deprecata e viene usato esclusivamente la sintassi abbreviata.  
  
 Poiché le sequenze di escape vengono mappate dal driver per tipi di sintassi specifici del DBMS, un'applicazione può utilizzare la sequenza di escape o sintassi specifici del DBMS. Le applicazioni che usano la sintassi specifici del DBMS, tuttavia, non sarà interoperative. Quando si usa la sequenza di escape, le applicazioni devono assicurarsi che l'attributo di istruzione SQL_ATTR_NOSCAN è disattivato, ovvero l'impostazione predefinita. In caso contrario, la sequenza di escape verrà inviata direttamente all'origine dati, in cui in genere causerà un errore di sintassi.  
  
 I driver supportano solo le sequenze di escape che possono eseguire il mapping alle caratteristiche linguistiche sottostante. Ad esempio, se l'origine dati non supporta gli outer join, verranno né il driver. Per determinare quali sequenze di escape sono supportate, un'applicazione chiama **SQLGetTypeInfo** e **SQLGetInfo**. Per altre informazioni, vedere la sezione successiva [Date, Time e Timestamp valori letterali](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Valori letterali data, ora e timestamp](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Chiamate di funzioni scalari](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [Carattere di escape nel predicato LIKE](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Outer Join](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Chiamate di procedura](../../../odbc/reference/develop-app/procedure-calls.md)
