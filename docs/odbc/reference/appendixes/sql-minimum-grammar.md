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
ms.openlocfilehash: 85b1f59efd809c604458bd7b99882705db240e9a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057016"
---
# <a name="sql-minimum-grammar"></a>Grammatica SQL di base
Questa sezione descrive la sintassi SQL minima che deve supportare un driver ODBC. La sintassi descritta in questa sezione è un subset della sintassi voce a livello di SQL-92.  
  
 Un'applicazione può usare qualsiasi della sintassi in questa sezione e avere la certezza che qualsiasi driver conforme a ODBC supporta tale sintassi. Per determinare se sono supportate le funzionalità aggiuntive di SQL-92 non in questa sezione, l'applicazione deve chiamare **SQLGetInfo** con il tipo di informazioni SQL_SQL_CONFORMANCE. Anche se il driver non corrisponde a qualsiasi livello di conformità SQL-92, un'applicazione può ancora usare la sintassi descritta in questa sezione. Se un driver conforme a un livello di SQL-92, d'altra parte, supporta tutte le sintassi inclusa in tale livello. Ciò include la sintassi in questa sezione perché la grammatica descritta di seguito è un subset puro di livello più basso della conformità SQL-92. Dopo l'applicazione conosce a livello di SQL-92 supportato, è possibile determinare se una funzionalità di livello superiore è supportata (se presente) chiamando **SQLGetInfo** con il tipo di informazioni singoli corrispondente a tale funzionalità.  
  
 I driver che funzionano solo con le origini dati di sola lettura potrebbero non supportare le parti della grammatica di cui è incluso in questa sezione che gestiscono la modifica dei dati. Un'applicazione può determinare se un'origine dati è di sola lettura chiamando **SQLGetInfo** con il tipo di informazioni SQL_DATA_SOURCE_READ_ONLY.  
  
## <a name="statement"></a>.  
 *istruzione create table* :: =  
  
 CREATE TABLE *nome-tabella di base*  
  
 ( *-tipo di dati colonna-identifier* [ *, tipo di dati colonna identificatore*]...)  
  
> [!IMPORTANT]  
>  Come un *tipo di dati* in un *-istruzione create table*, le applicazioni devono utilizzare un tipo di dati dalla colonna TYPE_NAME del set di risultati restituito da **SQLGetTypeInfo**.  
  
 *Delete-istruzione, eseguire la ricerca* :: =  
  
 DELETE FROM *-nome della tabella* [dove *condizione di ricerca*]  
  
 *istruzione DROP-tabella* :: =  
  
 DROP TABLE *nome-tabella di base*  
  
 *istruzione INSERT* :: =  
  
 INSERT INTO *-nome della tabella* [( *colonna identificatore* [, *colonna identificatore*]...)]      I valori (*insert-value*[, *insert-valore*]...)  
  
 *istruzione SELECT* :: =  
  
 Selezionare [tutti i &#124; DISTINCT] *elenco select*  
  
 DA *elenco di riferimento di tabella*  
  
 [In cui *condizione di ricerca*]  
  
 [*clausola order by*]  
  
 *informativa* :: = *dall'istruzione create table*  
  
 &#124; *delete-statement-searched*  
  
 &#124;*drop-tabella-istruzione*  
  
 &#124; *insert-statement*  
  
 &#124;*select-istruzione*  
  
 &#124; *update-statement-searched*  
  
 *update-statement-searched*  
  
 AGGIORNAMENTO *-nome della tabella*  
  
 IMPOSTARE *identificatore di colonna* = {*expression* &#124; NULL}  
  
 [, *column-identifier* = {*expression* &#124; NULL}]...  
  
 [In cui *condizione di ricerca*]  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Elementi usati nelle istruzioni SQL](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Supporto dei tipi di dati](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Tipi di dati parametro](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Marcatori di parametro](../../../odbc/reference/appendixes/parameter-markers.md)
