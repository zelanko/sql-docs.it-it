---
title: Mapping dei tipi di dati (driver ODBC per Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 432c21b70efcdd63ef36bfe3d26f8488ddb11d1d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302672"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>Mapping dei tipi di dati (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Il server Oracle supporta un set di tipi di dati. Il driver ODBC per Oracle esegue il mapping di questi tipi di dati ai tipi di dati SQL ODBC appropriati. Nella tabella seguente sono elencati i tipi di dati del server Oracle 7,3 e i tipi di dati SQL ODBC corrispondenti.  
  
 Il driver ODBC per Oracle supporta Oracle 7,3 e alcuni tipi di dati Oracle8. Per altre informazioni sui tipi di dati Oracle8 supportati, vedere [tipi di dati supportati](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md).  
  
|Tipo di dati del server Oracle|Tipo di dati SQL ODBC|  
|-----------------------------|------------------------|  
|CHAR|SQL_CHAR|  
|DATE|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_DECIMAL|  
|LONG|SQL_LONGVARCHAR|  
|LONG RAW|SQL_LONGVARBINARY|  
|NUMBER|SQL_DECIMAL|  
|RAW|SQL_VARBINARY|  
|VARCHAR2|SQL_VARCHAR|  
  
> [!NOTE]  
>  Per ulteriori informazioni sulle dimensioni consentite della colonna VARCHAR, vedere la pagina relativa alle [dimensioni delle colonne varchar](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) in questa guida.
