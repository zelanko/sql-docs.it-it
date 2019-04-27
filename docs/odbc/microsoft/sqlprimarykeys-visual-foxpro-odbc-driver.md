---
title: SQLPrimaryKeys (Driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3eeafa338fea31741609e6f9a9b32a4128ebd87d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62636330"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: Livello 2  
  
 Restituisce i nomi delle colonne che costituiscono la chiave primaria per una tabella. L'implementazione di Driver ODBC Visual FoxPro della **SQLPrimaryKeys** si comporta come segue:  
  
-   Ignora la *szTableOwner* e *cbTableOwner* argomenti.  
  
-   Funziona solo per le origini dati che sono [database](../../odbc/microsoft/visual-foxpro-terminology.md). Il driver restituisce l'errore "Driver non supporta questa funzione" se l'origine dati è una directory dei [libero tabelle](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Per altre informazioni, vedere [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) nel *riferimento per programmatori ODBC*.
