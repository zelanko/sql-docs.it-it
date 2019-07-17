---
title: SQLAllocConnect (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 70d48b12-def5-475c-b8e1-654a55fdfe0f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2889ef8e5c6f3a0db4e133ddf0bdd51fda338b40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063287"
---
# <a name="sqlallocconnect-visual-foxpro-odbc-driver"></a>SQLAllocConnect (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: A livello centrale  
  
 Alloca memoria per un handle di connessione *hdbc*, all'interno dell'ambiente identificato dal *henv*. Gestione Driver elabora questa chiamata e il driver chiama **SQLAllocConnect** ogni volta che [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md), **SQLBrowseConnect**, o [SQLDriverConnect ](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) viene chiamato.  
  
 Per altre informazioni, vedere [SQLAllocConnect](../../odbc/reference/syntax/sqlallocconnect-function.md) nel *riferimento per programmatori ODBC*.
