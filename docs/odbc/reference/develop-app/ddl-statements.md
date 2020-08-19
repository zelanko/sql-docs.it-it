---
description: Istruzioni DDL
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 395abe3eed64f37c000ecff6f0b68a6e0cb1d076
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424733"
---
# <a name="ddl-statements"></a>Istruzioni DDL
Le istruzioni DDL (Data Definition Language) variano notevolmente tra i sistemi DBMS. ODBC SQL definisce istruzioni per le operazioni più comuni di definizione dei dati: creazione ed eliminazione di tabelle, indici e viste; modifica di tabelle; e la concessione e la revoca dei privilegi. Tutte le altre istruzioni DDL sono specifiche dell'origine dati. Pertanto, le applicazioni interoperabili non possono eseguire alcune operazioni di definizione dei dati. In generale, questo non è un problema, perché tali operazioni tendono a essere specifiche del DBMS e sono più adatte al software di amministrazione del database proprietario fornito con la maggior parte dei DBMS o il programma di installazione fornito con il driver.  
  
 Un altro problema nella definizione dei dati è che i nomi dei tipi di dati variano notevolmente tra i DBMS. Anziché definire i nomi dei tipi di dati standard e forzare i driver a convertirli in nomi specifici di DBMS, **SQLGetTypeInfo** consente alle applicazioni di individuare i nomi dei tipi di dati specifici del sistema DBMS. Per creare e modificare le tabelle, le applicazioni interoperative devono usare questi nomi nelle istruzioni SQL. i nomi elencati nei tipi di dati [Appendice C: grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)e [Appendice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md)sono solo esempi.
