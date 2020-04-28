---
title: SQLPrimaryKeys (driver ODBC Visual FoxPro) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83631d22bd07017c4eba8f6af171443ab8c76d9c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301546"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello 2  
  
 Restituisce i nomi delle colonne che costituiscono la chiave primaria per una tabella. Il comportamento dell'implementazione del driver ODBC Visual FoxPro di **SQLPrimaryKeys** è il seguente:  
  
-   Ignora gli argomenti *szTableOwner* e *cbTableOwner* .  
  
-   Funziona solo per le origini dati che sono [database](../../odbc/microsoft/visual-foxpro-terminology.md). Il driver restituisce l'errore "il driver non supporta questa funzione" se l'origine dati è una directory di [tabelle gratuite](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Per ulteriori informazioni, vedere [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) in *ODBC Programmer ' s Reference*.
