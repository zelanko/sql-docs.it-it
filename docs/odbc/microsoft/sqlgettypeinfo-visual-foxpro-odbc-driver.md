---
description: SQLGetTypeInfo (driver ODBC Visual FoxPro)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e24f506f1134e9191e370971795a23bbbb3bd380
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500177"
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
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|Memo (binario)|  
|SQL_LONGVARCHAR|Memo|  
|SQL_NUMERIC|Numeric *, Currency, float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|Non supportato. Non è presente alcun tipo di *tempo* Visual FoxPro.|  
|SQL_TIMESTAMP|Datetime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|Memo (binario) *, generale|  
|SQL_VARCHAR|Carattere|  
  
 * Tipo predefinito  
  
 Per ulteriori informazioni sui tipi di dati Visual FoxPro, vedere [Create Table](../../odbc/microsoft/create-table-sql-command.md). Per ulteriori informazioni su questa funzione, vedere [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) in *ODBC Programmer ' s Reference*.
