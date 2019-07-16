---
title: Origini dati di file | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d27f168640b25652ed0fd40154ebfb677ef9300
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068643"
---
# <a name="file-data-sources"></a>Origini dati di file
*Origini dati del file* vengono archiviati in un file e consentire le informazioni di connessione da usare più volte da un singolo utente o condiviso da più utenti. Quando viene usata un'origine dati file, gestione Driver stabilisce la connessione all'origine dati usando le informazioni in un file DSN. Questo file può essere modificato come qualsiasi altro file. Un'origine dati file non è un nome dell'origine dati, perché esegue un'origine dati di computer e non è registrato per qualsiasi utente o computer.  
  
 Un'origine dati file semplifica il processo di connessione, perché il file DSN contiene la stringa di connessione che in caso contrario, dovrà essere compilato per una chiamata per il **SQLDriverConnect** (funzione). Un altro vantaggio del file DSN è che si possono essere copiato in qualsiasi computer, in modo da origini dati identici possono essere usate da tutti i computer, purché abbiano il driver appropriato installato. Un'origine dati file può essere condivisa anche dalle applicazioni. Un'origine dati file condivisibile possa essere inserita in una rete e utilizzata contemporaneamente da più applicazioni.  
  
 Un file DSN può anche essere condivisibile. Un file DSN condivisibili risiede in un singolo computer e fa riferimento a un'origine di dati della macchina. Origini dati dei file condivisibili esistano principalmente per consentire la semplice conversione di origini dati dei computer alle origini dati dei file in modo che un'applicazione può essere progettata per funzionare esclusivamente con origini dati dei file. Quando Gestione Driver viene inviata le informazioni in un'origine dati file condivisibile, si connette se necessario, per l'origine dati di computer a cui punta il file DSN.  
  
 Per altre informazioni sulle origini dati dei file, vedere [ci si connette tramite File Zdroje dat](../../odbc/reference/develop-app/connecting-using-file-data-sources.md), o il [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) descrizione della funzione.
