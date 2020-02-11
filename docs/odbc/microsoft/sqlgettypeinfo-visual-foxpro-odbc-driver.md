---
title: SQLGetTypeInfo (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5f25e20b-a4ef-42da-aeb6-00e0510fb1cc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f29be5e03a6cc9c1c91809db2b8ec7c686e90f11
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898623"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello 1  
  
 Restituisce informazioni sui tipi di dati supportati da un'origine dati. Il driver restituisce le informazioni in un set di risultati SQL. Nella tabella seguente sono elencati i tipi di dati ODBC e il tipo di dati Visual FoxPro corrispondente.  
  
|Tipo ODBC|Tipo Visual FoxPro|  
|---------------|------------------------|  
|SQL_BIGINT|Non supportato. Non esiste alcun tipo Visual FoxPro a 64 bit.|  
|SQL_BIT|Logico|  
|SQL_CHAR|Carattere|  
|SQL_DATE|Data|  
|SQL_DECIMAL|Numeric|  
|SQL_DOUBLE|DOUBLE|  
|SQL_FLOAT|DOUBLE|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|Memo (binario)|  
|SQL_LONGVARCHAR|Memo|  
|SQL_NUMERIC|Numeric *, Currency, float|  
|SQL_REAL|DOUBLE|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|Non supportato. Non è presente alcun tipo di *tempo* Visual FoxPro.|  
|SQL_TIMESTAMP|Datetime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|Memo (binario) *, generale|  
|SQL_VARCHAR|Carattere|  
  
 * Tipo predefinito  
  
 Per ulteriori informazioni sui tipi di dati Visual FoxPro, vedere [Create Table](../../odbc/microsoft/create-table-sql-command.md). Per ulteriori informazioni su questa funzione, vedere [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) in *ODBC Programmer ' s Reference*.
