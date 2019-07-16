---
title: SQLSpecialColumns (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b690cceecb6c9980f5d84e96bccb1b02f014c026
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093093"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: Livello 1  
  
 Recupera il set di colonne ottimale che identifica in modo univoco una riga nella tabella.  
  
 Il Driver ODBC Visual FoxPro restituisce le colonne che costituiscono la chiave primaria sulla tabella FoxPro. (Vedere [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md).) Se viene chiamato con *fColType* impostato su SQL_ROWVER, viene restituita alcuna colonna. **SQLSpecialColumns** funziona solo per le origini dati che vengono [database](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Per altre informazioni, vedere [SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) nel *riferimento per programmatori ODBC*.
