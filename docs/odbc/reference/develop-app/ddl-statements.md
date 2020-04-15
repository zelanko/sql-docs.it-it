---
title: Istruzioni DDL Documenti Microsoft
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
ms.openlocfilehash: cae06efe6dd11e651e8553fa5c1004c2fa145478
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302992"
---
# <a name="ddl-statements"></a>Istruzioni DDL
Le istruzioni DDL (Data Definition Language) variano enormemente tra i DBS. ODBC SQL definisce le istruzioni per le operazioni di definizione dei dati più comuni: creazione ed eliminazione di tabelle, indici e viste; modifica delle tabelle; concedere e revocare privilegi. Tutte le altre istruzioni DDL sono specifiche dell'origine dati. Pertanto, le applicazioni interoperabili non possono eseguire alcune operazioni di definizione dei dati. In generale, questo non è un problema, perché tali operazioni tendono ad essere altamente specifiche DBMS e sono meglio lasciare al software di amministrazione del database proprietario fornito con la maggior parte DBMS o il programma di installazione fornito con il driver.  
  
 Un altro problema nella definizione dei dati è che i nomi dei tipi di dati variano enormemente tra i DBS. Anziché definire i nomi dei tipi di dati standard e forzare i driver a convertirli in nomi specifici di DBMS, **SQLGetTypeInfo** consente alle applicazioni di individuare i nomi dei tipi di dati specifici di DBMS. Le applicazioni interoperabili devono utilizzare questi nomi nelle istruzioni SQL per creare e modificare le tabelle. i nomi [elencati nell'Appendice C: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)e [Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md)sono solo esempi .
