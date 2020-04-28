---
title: Ruolo del driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c683d990aaa3fd6892369e734c06fd1c356bd0f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304283"
---
# <a name="role-of-the-driver"></a>Ruolo del driver
Il driver controlla la presenza di tutti gli errori e gli avvisi non controllati da Gestione driver e i record di stato degli ordini generati. (ODBC 2). il driver *x* non Ordina i record di stato. Sono inclusi gli errori e gli avvisi nel troncamento dei dati, la conversione dei dati, la sintassi e alcune transizioni di stato. Il driver potrebbe inoltre controllare gli errori e gli avvisi parzialmente controllati da Gestione driver. Ad esempio, anche se Gestione driver controlla se il valore dell' *operazione* in **SQLSetPos** è valido, il driver deve verificare se è supportato.  
  
 Il driver esegue anche il mapping degli *errori nativi* , ovvero gli errori restituiti dall'origine dati a sqlstates. Ad esempio, il driver potrebbe eseguire il mapping di un numero di errori nativi diversi per la sintassi SQL non valida per SQLSTATE 42000 (errore di sintassi o violazione di accesso). Il driver restituisce il numero di errore nativo nel campo SQL_DIAG_NATIVE del record di stato. La documentazione del driver dovrebbe mostrare come viene eseguito il mapping degli errori e degli avvisi dall'origine dati agli argomenti in **SQLGetDiagRec** e **SQLGetDiagField**.
