---
title: Driver di Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ca9b70ee6a96759e496b831f7c12dc3ee78419b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087876"
---
# <a name="unicode-drivers"></a>Driver di Unicode
Se un driver deve essere un driver di Unicode o un driver ANSI dipende interamente la natura dell'origine dati. Se l'origine dati supporta i dati Unicode, il driver deve essere un driver di Unicode. Se l'origine dati supporta solo i dati di ANSI, il driver deve rimanere un driver ANSI.  
  
 È necessario esportare un driver di Unicode **SQLConnectW** venga riconosciuta come un driver di Unicode da Gestione Driver.  
  
 Un driver di Unicode è necessario accettare le funzioni Unicode (con suffisso *W*) e archiviare i dati Unicode. È possibile utilizzare anche funzioni ANSI, ma non è necessario. (Gestione Driver non supera una chiamata di funzione ANSI con la *oggetto* suffisso per il driver, ma converte a ANSI chiamata senza il suffisso e quindi passa alla funzione, del driver.)  
  
 Un driver di Unicode deve essere in grado di restituire set di risultati in un valore Unicode o ANSI, a seconda dell'associazione dell'applicazione. Se un'applicazione si associa a SQL_C_CHAR, il driver di Unicode deve convertire dati SQL_WCHAR SQL_CHAR. Gestione driver assocerà SQL_C_WCHAR SQL_C_CHAR per i driver ANSI ma nessun mapping per i driver di Unicode non.  
  
> [!NOTE]  
>  Quando si determina il tipo di driver, Driver Manager chiamerà **SQLSetConnectAttr** e impostare l'attributo SQL_ATTR_ANSI_APP al momento della connessione. Se l'applicazione usa le API ANSI, SQL_ATTR_ANSI_APP verrà automaticamente impostato SQL_AA_TRUE e se Usa Unicode, verrà impostato sul valore SQL_AA_FALSE. Questo attributo viene usato in modo che il driver può presentare un comportamento diverso in base al tipo di applicazione. L'attributo non può essere impostato direttamente dall'applicazione e non è supportata dal **SQLGetConnectAttr**. Se un driver presenta lo stesso comportamento per applicazioni ANSI e Unicode, deve restituire SQL_ERROR per questo attributo. Se il driver restituisce SQL_SUCCESS, gestione Driver separa le connessioni agli standard ANSI e Unicode quando viene usato il pool di connessioni.
