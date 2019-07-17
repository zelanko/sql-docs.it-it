---
title: Funzioni di catalogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 232d2e9b7e9eb695a40058075ea511392e464a32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064404"
---
# <a name="catalog-functions"></a>Funzioni di catalogo
Tutti i database presentano una struttura che descrive la modalità con cui i dati verranno archiviati nel database. Ad esempio, un database semplice ordini di vendita può avere la struttura illustrata nella figura seguente, in cui le colonne ID vengono utilizzate per collegare le tabelle.  
  
 ![Viene illustrata la struttura di un database semplice](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 Questa struttura, insieme ad altre informazioni, ad esempio i privilegi, viene archiviata in un set di tabelle di sistema denominato del database *catalog* che è noto anche come una *dizionario dei dati*.  
  
 Un'applicazione può individuare questa struttura tramite le chiamate per il *funzioni di catalogo*. Le funzioni di catalogo restituiscono informazioni in set di risultati e sono in genere implementato tramite **seleziona** istruzioni con le tabelle nel catalogo. Un'applicazione potrebbe ad esempio richiedere un set di risultati contenente informazioni su tutte le tabelle del sistema o tutte le colonne di una particolare tabella.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Utilizzi dei dati del catalogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [Funzioni di catalogo in ODBC](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
