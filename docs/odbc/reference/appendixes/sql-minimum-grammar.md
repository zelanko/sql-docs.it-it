---
title: La grammatica SQL minima | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 26cf76200010edae7f85993ec33eb3722f35e94e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270502"
---
# <a name="sql-minimum-grammar"></a>Grammatica SQL di base
Questa sezione descrive la sintassi SQL minima che deve supportare un driver ODBC. La sintassi descritta in questa sezione è un subset della sintassi voce a livello di SQL-92.  
  
 Un'applicazione può usare qualsiasi della sintassi in questa sezione e avere la certezza che qualsiasi driver conforme a ODBC supporta tale sintassi. Per determinare se sono supportate le funzionalità aggiuntive di SQL-92 non in questa sezione, l'applicazione deve chiamare **SQLGetInfo** con il tipo di informazioni SQL_SQL_CONFORMANCE. Anche se il driver non corrisponde a qualsiasi livello di conformità SQL-92, un'applicazione può ancora usare la sintassi descritta in questa sezione. Se un driver conforme a un livello di SQL-92, d'altra parte, supporta tutte le sintassi inclusa in tale livello. Ciò include la sintassi in questa sezione perché la grammatica descritta di seguito è un subset puro di livello più basso della conformità SQL-92. Dopo l'applicazione conosce a livello di SQL-92 supportato, è possibile determinare se una funzionalità di livello superiore è supportata (se presente) chiamando **SQLGetInfo** con il tipo di informazioni singoli corrispondente a tale funzionalità.  
  
 I driver che funzionano solo con le origini dati di sola lettura potrebbero non supportare le parti della grammatica di cui è incluso in questa sezione che gestiscono la modifica dei dati. Un'applicazione può determinare se un'origine dati è di sola lettura chiamando **SQLGetInfo** con il tipo di informazioni SQL_DATA_SOURCE_READ_ONLY.  
  
## <a name="statement"></a>.  
 *create-table-statement* ::=  
  
 CREATE TABLE *nome-tabella di base*  
  
 (*column-identifier data-type* [ *,column-identifier data-type*]...)  
  
> [!IMPORTANT]  
>  Come un *tipo di dati* in un *-istruzione create table*, le applicazioni devono utilizzare un tipo di dati dalla colonna TYPE_NAME del set di risultati restituito da **SQLGetTypeInfo**.  
  
 *Delete-istruzione, eseguire la ricerca* :: =  
  
 DELETE FROM *-nome della tabella* [dove *condizione di ricerca*]  
  
 *istruzione DROP-tabella* :: =  
  
 DROP TABLE *nome-tabella di base*  
  
 *insert-statement* ::=  
  
 INSERT INTO *-nome della tabella* [( *colonna identificatore* [, *colonna identificatore*]...)]      I valori (*insert-value*[, *insert-valore*]...)  
  
 *istruzione SELECT* :: =  
  
 Selezionare [tutti i &#124; DISTINCT] *elenco select*  
  
 FROM *table-reference-list*  
  
 [In cui *condizione di ricerca*]  
  
 [*order-by-clause*]  
  
 *informativa* :: = *dall'istruzione create table*  
  
 &#124; *delete-statement-searched*  
  
 &#124; *drop-table-statement*  
  
 &#124; *insert-statement*  
  
 &#124; *select-statement*  
  
 &#124; *update-statement-searched*  
  
 *update-statement-searched*  
  
 AGGIORNAMENTO *-nome della tabella*  
  
 SET *column-identifier* = {*expression* &#124; NULL }  
  
 [, *column-identifier* = {*expression* &#124; NULL}]...  
  
 [In cui *condizione di ricerca*]  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Elementi usati nelle istruzioni SQL](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Supporto dei tipi di dati](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Tipi di dati parametro](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Marcatori di parametro](../../../odbc/reference/appendixes/parameter-markers.md)
