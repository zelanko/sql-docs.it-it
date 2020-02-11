---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5521fb11cad064cf487d38562f4146fd32587993
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898789"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello 1  
  
 Restituisce l'impostazione corrente di un'opzione dell'istruzione.  
  
|*FOption*|Valori di codice restituiti|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|valore intero a 32 bit che rappresenta il segnalibro per il numero di record corrente|  
|SQL_ROW_NUMBER|intero a 32 bit che specifica la posizione della riga corrente all'interno del set di risultati|  
|SQL_TRANSLATE_DLL|Errore: "driver non in grado di supportare"|  
  
 Il driver ODBC Visual FoxPro non contiene dll di traduzione.  
  
 Per ulteriori informazioni, vedere [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) in *ODBC Programmer ' s Reference*.
