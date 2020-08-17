---
description: SQLGetTypeInfo (driver dBASE)
title: SQLGetTypeInfo (driver dBASE) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c94bca8dbc8413f6a3b8fdffed61f9ecd15f78e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339967"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo (driver dBASE)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver dBASE. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il nome del tipo (TYPE_NAME) restituito nella tabella prodotta da **SQLGetTypeInfo** sarà il nome usato più di frequente dall'origine dati.  
  
 SQL_ALL_EXCEPT_LIKE verrà restituito nella colonna RICERCAbile per i tipi di dati byte, Counter, Double, Single, Long e short. Per ottenere la funzionalità LIKE, è possibile convertire il valore in un carattere usando le funzioni di conversione canoniche ODBC, quindi eseguire il confronto.
