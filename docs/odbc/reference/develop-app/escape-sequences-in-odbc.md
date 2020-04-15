---
title: Sequenze di escape in ODBC . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d41b0c03ecbe6de63cba1a28a1f39f12a42dc86
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300421"
---
# <a name="escape-sequences-in-odbc"></a>Sequenze di escape in ODBC
Un certo numero di funzionalità del linguaggio, ad esempio outer join e chiamate di funzione scalari, sono comunemente implementate da DBMS. Tuttavia, le sintassi per queste funzionalità tendono ad essere specifiche di DBMS, anche quando le sintassi standard sono definite dai vari organismi di standard. Per questo motivo, ODBC definisce le sequenze di escape che contengono sintassi standard per le seguenti funzionalità del linguaggio:  
  
-   Valori letterali di intervallo di data, ora, timestamp e datetime  
  
-   Funzioni scalari come le funzioni numeriche, stringa e conversione dei tipi di dati  
  
-   Carattere di escape predicato LIKE  
  
-   Outer join  
  
-   Chiamate procedurali  
  
 La sequenza di escape utilizzata da ODBC è la seguente:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Osservazioni  
 La sequenza di escape viene riconosciuta e analizzata dai driver, che sostituiscono le sequenze di escape con la grammatica specifica di DBMS. Per ulteriori informazioni sulla sintassi della sequenza di escape, vedere [Sequenze](../../../odbc/reference/appendixes/odbc-escape-sequences.md) di escape ODBC nell'Appendice C: grammatica SQL.  
  
> [!NOTE]  
>  In ODBC 2. *x*, questa era la sintassi standard della sequenza di escape: **--(\*vendor(**_vendor-name_**), product(**_product-name_**)**_extension_ ** \*)-- --**  
>   
>  Oltre a questa sintassi, è stata definita una sintassi abbreviata nel formato:**}** **estensione**_extension_  
>   
>  In ODBC 3. *x*, la forma lunga della sequenza di escape è stata deprecata e la forma abbreviata viene utilizzata in modo esclusivo.  
  
 Poiché le sequenze di escape vengono mappate dal driver alle sintassi specifiche di DBMS, un'applicazione può utilizzare la sequenza di escape o la sintassi specifica di DBMS. Tuttavia, le applicazioni che utilizzano la sintassi specifica di DBMS non saranno interoperabili. Quando si usa la sequenza di escape, le applicazioni devono assicurarsi che l'attributo dell'istruzione SQL_ATTR_NOSCAN sia disattivato, che è per impostazione predefinita. In caso contrario, la sequenza di escape verrà inviata direttamente all'origine dati, dove in genere causerà un errore di sintassi.  
  
 I driver supportano solo le sequenze di escape che possono eseguire il mapping alle funzionalità del linguaggio sottostante. Ad esempio, se l'origine dati non supporta outer join, il driver non lo sarà nemmeno il driver. Per determinare quali sequenze di escape sono supportate, un'applicazione chiama **SQLGetTypeInfo** e **SQLGetInfo**. Per ulteriori informazioni, vedere la sezione [successiva, Data, ora e Valori letterali timestamp](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Valori letterali data, ora e timestamp](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Chiamate di funzioni scalari](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [Carattere di escape nel predicato LIKE](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Outer join](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Chiamate di procedura](../../../odbc/reference/develop-app/procedure-calls.md)
