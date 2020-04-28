---
title: Tipi di dati supportati (driver ODBC per Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: 21d5f8d9-a3aa-4aa4-bc37-ff8bc90c0870
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 313254a3a117984d666d7c7be7e506386ae34e3b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301116"
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>Tipi di dati supportati (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Il driver ODBC per Oracle supporta tutti i tipi di dati Oracle 7,3; Tuttavia, non supporta alcuno dei nuovi tipi di dati Oracle8 elencati di seguito.  
  
|Tipo di dati|Oracle 7,3|Oracle8|  
|---------------|----------------|-------------|  
|BFILE|n/d|Non supportato|  
|BLOB|n/d|Non supportato|  
|CHAR|Supportato|Supportato|  
|CLOB|n/d|Non supportato|  
|DATE|Supportato|Supportato|  
|FLOAT|Supportato|Supportato|  
|INTEGER|Supportato|Supportato|  
|LONG|Supportato|Supportato|  
|LONG RAW|Supportato|Supportato|  
|NCHAR|n/d|Non supportato|  
|NCLOB|n/d|Non supportato|  
|NUMBER|Supportato|Supportato|  
|NVARCHAR2|n/d|Non supportato|  
|RAW|Supportato|Supportato|  
|VARCHAR2|Supportato|Supportato|  
|MLSLABEL|Non supportato.|Non supportato.|  
  
> [!NOTE]  
>  Per ulteriori informazioni sulle dimensioni consentite della colonna VARCHAR, vedere la pagina relativa alle [dimensioni delle colonne varchar](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) in questa guida.
