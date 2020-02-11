---
title: Funzionalità da controllare | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], writing interoperable applications
ms.assetid: 0fb1693b-11c3-43b1-bb16-c3323b7b2d45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f48a3c7568a9db8b599f6d5a1997607fb16e6020
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069877"
---
# <a name="features-to-watch-for"></a>Funzionalità da controllare
Questa sezione descrive una serie di funzionalità che gli sviluppatori di applicazioni spesso accettano per scontate. In realtà, queste funzionalità variano notevolmente in termini di supporto e modalità di supporto tra DBMS. è probabile che non si verifichino errori di codice per questi problemi nelle applicazioni interoperative.  
  
 In questa sezione non sono elencate tutte le funzionalità che gli sviluppatori di applicazioni devono prendere in considerazione. Per informazioni, vedere le descrizioni delle funzioni [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)e [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) , [Appendice C: grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)e le sezioni di questo manuale che illustrano ciascuna funzionalità.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Numero di versione](../../../odbc/reference/develop-app/version-number.md)  
  
-   [Istruzioni e connessioni attive multiple](../../../odbc/reference/develop-app/multiple-active-statements-and-connections.md)  
  
-   [Supporto delle transazioni in DBMS](../../../odbc/reference/develop-app/transaction-support-in-dbmss.md)  
  
-   [Commit e comportamento di rollback](../../../odbc/reference/develop-app/commit-and-rollback-behavior.md)  
  
-   [Istruzioni NOT NULL in CREATE TABLE](../../../odbc/reference/develop-app/not-null-in-create-table-statements.md)  
  
-   [Tipi di dati supportati](../../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)  
  
-   [Grammatica SQL ODBC](../../../odbc/reference/develop-app/odbc-sql-grammar.md)  
  
-   [Elaborazione batch](../../../odbc/reference/develop-app/batch-processing.md)
