---
description: SQLGetStmtOption (driver ODBC Visual FoxPro)
title: SQLGetStmtOption (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e57456ca05e39c12b83da80cd19c34f482c3d8df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340087"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello 1  
  
 Restituisce l'impostazione corrente di un'opzione dell'istruzione.  
  
|*FOption*|Restituisce|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|valore intero a 32 bit che rappresenta il segnalibro per il numero di record corrente|  
|SQL_ROW_NUMBER|intero a 32 bit che specifica la posizione della riga corrente all'interno del set di risultati|  
|SQL_TRANSLATE_DLL|Errore: "driver non in grado di supportare"|  
  
 Il driver ODBC Visual FoxPro non contiene dll di traduzione.  
  
 Per ulteriori informazioni, vedere [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) in *ODBC Programmer ' s Reference*.
