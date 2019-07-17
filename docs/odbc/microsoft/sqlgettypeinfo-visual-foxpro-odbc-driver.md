---
title: SQLGetTypeInfo (Driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898623"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: Livello 1  
  
 Restituisce informazioni sui tipi di dati supportati da un'origine dati. Il driver restituisce le informazioni in un set di risultati SQL. La tabella seguente elenca i tipi di dati ODBC e il tipo di dati Visual FoxPro corrispondente.  
  
|Tipo ODBC|Tipo di oggetto visivo FoxPro|  
|---------------|------------------------|  
|SQL_BIGINT|Non supportati. È disponibile alcun tipo di Visual FoxPro a 64 bit.|  
|SQL_BIT|Logico|  
|SQL_CHAR|Carattere|  
|SQL_DATE|Date|  
|SQL_DECIMAL|Numeric|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|Memo (binario)|  
|SQL_LONGVARCHAR|Memo|  
|SQL_NUMERIC|Numerico *, valuta, Float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|Non supportati. Non vi è alcun Visual FoxPro *ora* tipo.|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|Memo (binario) *, generale|  
|SQL_VARCHAR|Carattere|  
  
 \* Tipo di predefinito  
  
 Per altre informazioni sui tipi di dati Visual FoxPro, vedere [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md). Per altre informazioni su questa funzione, vedere [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) nel *riferimento per programmatori ODBC*.
