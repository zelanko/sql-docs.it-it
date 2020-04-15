---
title: Grammatica minima di SQL Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20eee34feadb8e3140f25019ec6b0d036ff02e14
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304992"
---
# <a name="sql-minimum-grammar"></a>Grammatica SQL di base
In questa sezione viene descritta la sintassi SQL minima che un driver ODBC deve supportare. La sintassi descritta in questa sezione è un sottoinsieme della sintassi del livello Entry di SQL-92.  
  
 Un'applicazione può utilizzare qualsiasi sintassi in questa sezione ed essere certi che qualsiasi driver compatibile con ODBC supporterà tale sintassi. Per determinare se sono supportate funzionalità aggiuntive di SQL-92 non presenti in questa sezione, l'applicazione deve chiamare **SQLGetInfo** con il tipo di informazioni SQL_SQL_CONFORMANCE. Anche se il driver non è conforme a qualsiasi livello di conformità SQL-92, un'applicazione può comunque utilizzare la sintassi descritta in questa sezione. Se un driver è conforme a un livello SQL-92, d'altra parte, supporta tutta la sintassi inclusa in tale livello. Ciò include la sintassi in questa sezione perché la grammatica minima descritta di seguito è un sottoinsieme puro del livello di conformità SQL-92 più basso. Una volta che l'applicazione conosce il livello SQL-92 supportato, può determinare se una funzionalità di livello superiore è supportata (se presente) chiamando **SQLGetInfo** con il tipo di informazioni singolo corrispondente a tale funzionalità.  
  
 I driver che funzionano solo con origini dati di sola lettura potrebbero non supportare quelle parti della grammatica incluse in questa sezione che gestiscono la modifica dei dati. Un'applicazione può determinare se un'origine dati è di sola lettura chiamando **SQLGetInfo** con il tipo di informazioni SQL_DATA_SOURCE_READ_ONLY.  
  
## <a name="statement"></a>.  
 *istruzione di tabella di creazione* ::  
  
 CREATE TABLE *nome-tabella di base*  
  
 (*tipo di dati dell'identificatore* di colonna [ , tipo di dati*dell'identificatore di colonna*]...)  
  
> [!IMPORTANT]  
>  Come *tipo di dati* in *un'istruzione create-table-statement*, le applicazioni devono utilizzare un tipo di dati dalla colonna TYPE_NAME del set di risultati restituito da **SQLGetTypeInfo**.  
  
 *delete-statement-ricercato* ::  
  
 DELETE FROM *nome tabella* [WHERE *search-condition*]  
  
 *drop-table-statement* ::  
  
 NOME *tabella di base* DROP TABLE  
  
 *insert-statement* ::  
  
 INSERT INTO *nome tabella* [( *identificatore di colonna* [, *identificatore di colonna*]...)]      VALORI (*insert-value*[, *insert-value*]... )  
  
 *select-statement* ::=  
  
 SELECT [ALL &#124; DISTINCT] *elenco a discesa*  
  
 FROM *tabella-reference-list*  
  
 *[CONDIZIONE-ricerca*WHERE ]  
  
 [*order-by-clause*]  
  
 *istruzione* :: : *create-table-statement*  
  
 &#124; *delete-statement-searched*  
  
 &#124; *drop-table-statement*  
  
 &#124; *insert-statement*  
  
 &#124; *istruzione select*  
  
 &#124; *update-statement-searched*  
  
 *update-statement-ricercato*  
  
 UPDATE *nome tabella*  
  
 IDENTIFICATORe *di colonna* SET:*espressione* &#124; NULL  
  
 [, *identificatore di colonna* :*espressione* &#124; NULL]...  
  
 *[CONDIZIONE-ricerca*WHERE ]  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Elementi usati nelle istruzioni SQL](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Supporto dei tipi di datiData Type Support](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Tipi di dati parametro](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Marcatori di parametro](../../../odbc/reference/appendixes/parameter-markers.md)
