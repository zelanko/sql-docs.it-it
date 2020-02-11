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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 145170afee5ab791602695c662ce1e80e86cae7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915675"
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>Tipi di dati supportati (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Il driver ODBC per Oracle supporta tutti i tipi di dati Oracle 7,3; Tuttavia, non supporta alcuno dei nuovi tipi di dati Oracle8 elencati di seguito.  
  
|Tipo di dati|Oracle 7,3|Oracle8|  
|---------------|----------------|-------------|  
|BFILE|n/d|Non supportate|  
|BLOB|n/d|Non supportate|  
|CHAR|Supportato|Supportato|  
|CLOB|n/d|Non supportate|  
|DATE|Supportato|Supportato|  
|FLOAT|Supportato|Supportato|  
|INTEGER|Supportato|Supportato|  
|LONG|Supportato|Supportato|  
|LONG RAW|Supportato|Supportato|  
|NCHAR|n/d|Non supportate|  
|NCLOB|n/d|Non supportate|  
|NUMBER|Supportato|Supportato|  
|NVARCHAR2|n/d|Non supportate|  
|RAW|Supportato|Supportato|  
|VARCHAR2|Supportato|Supportato|  
|MLSLABEL|Non supportato.|Non supportato.|  
  
> [!NOTE]  
>  Per ulteriori informazioni sulle dimensioni consentite della colonna VARCHAR, vedere la pagina relativa alle [dimensioni delle colonne varchar](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) in questa guida.
