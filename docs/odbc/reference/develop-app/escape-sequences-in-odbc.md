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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d41b0c03ecbe6de63cba1a28a1f39f12a42dc86
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300421"
---
# <a name="escape-sequences-in-odbc"></a>Sequenze di escape in ODBC
Diverse funzionalità del linguaggio, ad esempio outer join e chiamate di funzioni scalari, sono comunemente implementate da DBMS. Tuttavia, le sintassi per queste funzionalità tendono a essere specifiche di DBMS, anche quando le sintassi standard sono definite dai vari corpi degli standard. Per questo motivo, ODBC definisce sequenze di escape che contengono sintassi standard per le funzionalità del linguaggio seguenti:  
  
-   Valori letterali di data, ora, timestamp e intervallo DateTime  
  
-   Funzioni scalari come funzioni di conversione di tipi di dati, stringhe e numerici  
  
-   Carattere di escape del predicato LIKE  
  
-   Outer join  
  
-   Chiamate di procedure  
  
 La sequenza di escape utilizzata da ODBC è la seguente:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Osservazioni  
 La sequenza di escape viene riconosciuta e analizzata dai driver, che sostituiscono le sequenze di escape con la grammatica specifica di DBMS. Per ulteriori informazioni sulla sintassi della sequenza di escape, vedere [sequenze di escape ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) nell'Appendice C: grammatica SQL.  
  
> [!NOTE]  
>  In ODBC 2. *x*, questa è la sintassi standard della sequenza di escape: **--(\*fornitore (**_nome-fornitore_**),****)**_estensione_ ** \*** prodotto (_nome prodotto_))--  
>   
>  Oltre a questa sintassi, è stata definita una sintassi abbreviata nel formato: **{**_Extension_**}**  
>   
>  In ODBC 3. *x*, la forma estesa della sequenza di escape è stata deprecata e il form abbreviato viene usato in modo esclusivo.  
  
 Poiché le sequenze di escape vengono mappate dal driver a sintassi specifiche di DBMS, un'applicazione può utilizzare la sequenza di escape o la sintassi specifica del sistema DBMS. Tuttavia, le applicazioni che utilizzano la sintassi specifica di DBMS non saranno interoperative. Quando si usa la sequenza di escape, le applicazioni devono verificare che l'attributo dell'istruzione SQL_ATTR_NOSCAN sia disattivato, che è per impostazione predefinita. In caso contrario, la sequenza di escape verrà inviata direttamente all'origine dati, in cui in genere viene generato un errore di sintassi.  
  
 I driver supportano solo le sequenze di escape di cui è possibile eseguire il mapping alle funzionalità del linguaggio sottostante. Se, ad esempio, l'origine dati non supporta outer join, il driver non viene né. Per determinare quali sequenze di escape sono supportate, un'applicazione chiama **SQLGetTypeInfo** e **SQLGetInfo**. Per ulteriori informazioni, vedere la sezione successiva, [data, ora e valori letterali timestamp](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Valori letterali data, ora e timestamp](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Chiamate di funzioni scalari](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [Carattere di escape nel predicato LIKE](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Outer join](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Chiamate di procedura](../../../odbc/reference/develop-app/procedure-calls.md)
