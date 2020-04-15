---
title: SQLTables (driver dBASE) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLTables
- SQLTables function [ODBC], dBASE Driver
ms.assetid: 45938efb-b678-47d8-9345-644fa26ad679
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 242be06eafc7657f37f55ce266af471cbc72597f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306072"
---
# <a name="sqltables-dbase-driver"></a>SQLTables (driver dBASE)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver dBASE. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argomento|Commenti|  
|--------------|--------------|  
|*szTableOwner*|L'unico argomento valido per *szTableOwner* è NULL perché nessuno dei driver supporta i nomi dei proprietari. Con *szTableOwner* impostato su NULL, vengono restituite tutte le tabelle. NULL viene restituito nella colonna TABLE_OWNER.|  
|*SzTableQualifier (qualificatore di szTable)*|Nella colonna TABLE_QUALIFIER, **SQLTables** restituirà il percorso di una directory.|  
|*SzTableType (Tipo di SzTableType)*|Per i file dBASE, "TABLE" è l'unico tipo di tabella supportato.|
