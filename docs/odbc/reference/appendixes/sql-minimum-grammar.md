---
title: Grammatica minima SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85b1f59efd809c604458bd7b99882705db240e9a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057016"
---
# <a name="sql-minimum-grammar"></a>Grammatica SQL di base
In questa sezione viene descritta la sintassi SQL minima che un driver ODBC deve supportare. La sintassi descritta in questa sezione è un subset della sintassi a livello di voce di SQL-92.  
  
 Un'applicazione può utilizzare una qualsiasi sintassi di questa sezione e garantire che qualsiasi driver conforme a ODBC supporti tale sintassi. Per determinare se le funzionalità aggiuntive di SQL-92 non incluse in questa sezione sono supportate, l'applicazione deve chiamare **SQLGetInfo** con il tipo di informazioni SQL_SQL_CONFORMANCE. Anche se il driver non è conforme a un livello di conformità SQL-92, un'applicazione può comunque utilizzare la sintassi descritta in questa sezione. Se un driver è conforme a un livello SQL-92, al contrario, supporta tutta la sintassi inclusa in tale livello. Questo include la sintassi in questa sezione perché la grammatica minima descritta qui è un subset puro del livello di conformità SQL-92 più basso. Quando l'applicazione riconosce il livello SQL-92 supportato, può determinare se una funzionalità di livello superiore è supportata, se presente, chiamando **SQLGetInfo** con il tipo di informazioni singolo corrispondente a tale funzionalità.  
  
 I driver che funzionano solo con origini dati di sola lettura potrebbero non supportare le parti della grammatica inclusa in questa sezione che riguardano la modifica dei dati. Un'applicazione può determinare se un'origine dati è di sola lettura chiamando **SQLGetInfo** con il tipo di informazioni SQL_DATA_SOURCE_READ_ONLY.  
  
## <a name="statement"></a>.  
 *CREATE-TABLE-Statement* :: =  
  
 CREATE TABLE *nome-tabella-base*  
  
 (*tipo di dati identificatore di colonna* [*, tipo di dati identificatore di colonna*]...)  
  
> [!IMPORTANT]  
>  Come *tipo di dati* in un' *istruzione CREATE-TABLE*, le applicazioni devono utilizzare un tipo di dati della colonna TYPE_NAME del set di risultati restituito da **SQLGetTypeInfo**.  
  
 *Delete-Statement-cercato* :: =  
  
 Elimina da *nome-tabella* [WHERE *Search-Condition*]  
  
 *Drop-Table-Statement* :: =  
  
 DROP TABLE *-base-nome-tabella*  
  
 *INSERT-Statement* :: =  
  
 INSERT INTO *Table-Name* [( *column-identifier* [, *column-identifier*]...)]      VALORI (*Insert-value*[, *Insert-value*]...)  
  
 *SELECT-Statement* :: =  
  
 Select [ALL &#124; DISTINCT] *select-list*  
  
 DA *table-reference-list*  
  
 [Dove *ricerca-condizione*]  
  
 [*ORDER-BY-clause*]  
  
 *istruzione* :: = *CREATE-TABLE-Statement*  
  
 &#124; *Delete-Statement-* searched  
  
 &#124; *Drop-Table-Statement*  
  
 &#124; *INSERT-Statement*  
  
 &#124; *SELECT-Statement*  
  
 &#124; *Update-Statement-cercato*  
  
 *UPDATE-statement-ricerca eseguita*  
  
 Aggiorna *nome tabella*  
  
 SET *column-identifier* = {*Expression* &#124; null}  
  
 [, *identificatore di colonna* = {*Expression* &#124; null}]...  
  
 [Dove *ricerca-condizione*]  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Elementi usati nelle istruzioni SQL](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Supporto dei tipi di dati](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Tipi di dati parametro](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Marcatori di parametro](../../../odbc/reference/appendixes/parameter-markers.md)
