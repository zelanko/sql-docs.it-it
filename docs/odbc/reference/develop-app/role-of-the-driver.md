---
title: Ruolo del conducente Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304283"
---
# <a name="role-of-the-driver"></a>Ruolo del driver
Il driver verifica la presenza di tutti gli errori e gli avvisi non controllati da Gestione Driver e ordina i record di stato generati. (Un ODBC 2. *x* driver non ordina i record di stato.) Sono inclusi gli errori e gli avvisi nel troncamento dei dati, nella conversione dei dati, nella sintassi e in alcune transizioni di stato. Il driver potrebbe anche controllare gli errori e gli avvisi parzialmente controllati da Gestione Driver. Ad esempio, anche se Gestione Driver controlla se il valore di *Operazione* in **SQLSetPos** è valido, il driver deve verificare se è supportato.  
  
 Il driver esegue anche il mapping degli *errori nativi,* ovvero gli errori restituiti dall'origine dati, a SQLSTATEs. Ad esempio, il driver potrebbe eseguire il mapping di una serie di errori nativi diversi per la sintassi SQL non valida a SQLSTATE 42000 (errore di sintassi o violazione di accesso). Il driver restituisce il numero di errore nativo nel campo SQL_DIAG_NATIVE del record di stato. La documentazione del driver deve mostrare come gli errori e gli avvisi vengono mappati dall'origine dati agli argomenti in **SQLGetDiagRec** e **SQLGetDiagField**.
