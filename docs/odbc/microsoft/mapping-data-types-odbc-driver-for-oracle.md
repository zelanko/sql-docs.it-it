---
title: Mapping dei tipi di dati (Driver ODBC per Oracle) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 47646fd6fdf1e8fd16165af1bcfc5e741c6e610f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080732"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>Mapping dei tipi di dati (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Il Server Oracle supporta un set di tipi di dati. Il Driver ODBC per Oracle esegue il mapping di questi tipi di dati per i tipi di dati SQL ODBC appropriati. Nella tabella seguente sono elencati i tipi di dati Oracle Server 7.3 e dei tipi di dati ODBC SQL corrispondenti.  
  
 Il Driver ODBC per Oracle supporta Oracle 7.3 e alcuni tipi di dati Oracle8. Per altre informazioni sui tipi di dati Oracle8 supportati, vedere [Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md).  
  
|Tipo di dati di Oracle Server|Tipo di dati SQL ODBC|  
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
>  Per altre informazioni sulle dimensioni consentita della colonna VARCHAR, vedere [dimensioni della colonna VARCHAR](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) in questa Guida.
