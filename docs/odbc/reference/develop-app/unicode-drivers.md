---
title: Driver Unicode | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aabdd899d78c1141716725d57e343dc002dc96ad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284353"
---
# <a name="unicode-drivers"></a>Driver di Unicode
Se un driver deve essere un driver Unicode o un driver ANSI dipende interamente dalla natura dell'origine dati. Se l'origine dati supporta dati Unicode, il driver deve essere un driver Unicode. Se l'origine dati supporta solo dati ANSI, il driver deve rimanere un driver ANSI.  
  
 Un driver Unicode deve esportare **SQLConnectW** per essere riconosciuto come driver Unicode da Gestione driver.  
  
 Un driver Unicode deve accettare funzioni Unicode, con suffisso *W*, e archiviare dati Unicode. Può anche accettare funzioni ANSI, ma non è necessario per. (Gestione driver non passa una chiamata di funzione ANSI con *il suffisso a del driver* , ma la converte in una chiamata di funzione ANSI senza il suffisso e quindi la passa al driver).  
  
 Un driver Unicode deve essere in grado di restituire set di risultati in formato Unicode o ANSI, a seconda dell'associazione dell'applicazione. Se un'applicazione viene associata a SQL_C_CHAR, è necessario che il driver Unicode converta SQL_WCHAR dati in SQL_CHAR. Gestione driver eseguirà il mapping SQL_C_WCHAR SQL_C_CHAR per i driver ANSI, ma non esegue alcun mapping per i driver Unicode.  
  
> [!NOTE]  
>  Quando si determina il tipo di driver, gestione driver chiamerà **SQLSetConnectAttr** e imposterà l'attributo SQL_ATTR_ANSI_APP al momento della connessione. Se l'applicazione usa le API ANSI, SQL_ATTR_ANSI_APP sarà impostata su SQL_AA_TRUE e se usa Unicode, verrà impostata su un valore di SQL_AA_FALSE. Questo attributo viene utilizzato in modo che il driver possa presentare un comportamento diverso in base al tipo di applicazione. L'attributo non può essere impostato direttamente dall'applicazione e non è supportato da **SQLGetConnectAttr**. Se un driver presenta lo stesso comportamento per le applicazioni ANSI e Unicode, deve restituire SQL_ERROR per questo attributo. Se il driver restituisce SQL_SUCCESS, gestione driver separirà le connessioni ANSI e Unicode quando verrà utilizzato il pool di connessioni.
