---
title: SQLGetStmtOption (Driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898789"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: A livello di uno  
  
 Restituisce l'impostazione corrente di un'opzione di istruzione.  
  
|*fOption*|Valori di codice restituiti|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|valore intero a 32 bit che rappresenta il segnalibro per il numero di record corrente|  
|SQL_ROW_NUMBER|intero a 32 bit che specifica la posizione della riga corrente entro il risultato impostato|  
|SQL_TRANSLATE_DLL|Errore: "Non è in grado di driver"|  
  
 Il Driver ODBC Visual FoxPro è disponibile nessuna conversione DLL.  
  
 Per altre informazioni, vedere [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) nel *riferimento per programmatori ODBC*.
