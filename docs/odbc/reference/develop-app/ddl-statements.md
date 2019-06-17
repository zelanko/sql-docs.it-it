---
title: Istruzioni DDL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9100405c91387faa66b714a94b8259167ae31899
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267642"
---
# <a name="ddl-statements"></a>Istruzioni DDL
Istruzioni Data Definition Language (DDL) variano notevolmente tra DBMS. SQL ODBC definisce le istruzioni per le operazioni più comuni di definizione dei dati: creazione ed eliminazione di tabelle, indici e viste. modifica di tabelle; e concedere e revocare tali privilegi. Tutte le altre istruzioni DDL sono specifiche dell'origine dati. Pertanto, applicazioni interoperative non possono eseguire alcune operazioni di definizione dei dati. In genere, ciò non costituisce un problema, perché queste operazioni tendono a essere molto specifici del DBMS e più a sinistra per il software di amministrazione di database proprietario fornito con la maggior parte dei DBMS o il programma di installazione fornita con il driver.  
  
 Un altro problema nella definizione dei dati è tale tipo di dati i nomi di variano notevolmente tra DBMS. Anziché la definizione di nomi di tipi di dati standard e i driver per convertirli in nomi specifici del DBMS, forzando **SQLGetTypeInfo** fornisce un modo per le applicazioni individuare i nomi di tipi di dati specifici del DBMS. Applicazioni interoperative devono utilizzare questi nomi nelle istruzioni SQL per creare e modificare le tabelle; i nomi elencati nella [appendice c: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), e [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md), sono solo esempi.
