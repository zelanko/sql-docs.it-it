---
title: SqlGetStmtOption (driver ODBC di Visual FoxPro) Documenti Microsoft
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
ms.openlocfilehash: 2624783f7bd55903f5741c62190626e455a9096d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295141"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Completo  
  
 Conformità API ODBC: livello uno  
  
 Restituisce l'impostazione corrente di un'opzione di istruzione.  
  
|*Opzione FOption*|Valori di codice restituiti|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|Valore intero a 32 bit che è il segnalibro per il numero di record corrente|  
|SQL_ROW_NUMBER|Numero intero a 32 bit che specifica la posizione della riga corrente all'interno del set di risultati|  
|SQL_TRANSLATE_DLL|Errore: "Driver non in grado"|  
  
 Il driver ODBC di Visual FoxPro non dispone di DLL di conversione.  
  
 Per ulteriori informazioni, vedere [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) in *ODBC Programmer's Reference*.
