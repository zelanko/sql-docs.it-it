---
title: La connessione con SQLBrowseConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04df089b97bf385925c87a98b3f89cdac3ef21e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083127"
---
# <a name="connecting-with-sqlbrowseconnect"></a>Connessione con SQLBrowseConnect
**SQLBrowseConnect**, ad esempio **SQLDriverConnect**, Usa una stringa di connessione. Tuttavia, utilizzando **SQLBrowseConnect**, un'applicazione può costruire una stringa di connessione completa in fase di esecuzione. In questo modo, l'applicazione può eseguire due operazioni:  
  
-   Compilare la propria finestre di dialogo per la richiesta di queste informazioni, mantenendo in tal modo controllo sulla relativa "aspetto."  
  
-   Esplorare il sistema per individuare origini dati che possano essere utilizzate da un driver specifico, possibilmente in diversi passaggi. L'utente, ad esempio, potrebbe esplorare innanzitutto la rete per individuare i server e, dopo averne scelto uno, esplorare il server per individuare i database accessibili dal driver.  
  
 L'applicazione chiama **SQLBrowseConnect** e passa una stringa di connessione, nota come il *Sfoglia stringa di connessione richiesta* che specifica un'origine dati o driver. Il driver restituisce una stringa di connessione, nota come il *esplorare stringa di connessione risultato* che contiene le parole chiave, i valori possibili (se la parola chiave accetta un set discreto di valori) e nomi descrittivi. L'applicazione crea una finestra di dialogo con i nomi descrittivi e richiede l'immissione di valori. Quindi compila una nuova stringa di connessione Sfoglia richieste da questi valori e restituisce l'oggetto per il driver con un'altra chiamata a **SQLBrowseConnect**.  
  
 Poiché le stringhe di connessione vengono passate avanti e indietro, il driver può fornire diversi livelli di esplorazione, restituendo una nuova stringa di connessione quando l'applicazione termina quella precedente. Ad esempio, la prima volta un'applicazione chiama **SQLBrowseConnect**, il driver può restituire le parole chiave per richiedere all'utente per un nome del server. Quando l'applicazione viene restituito il nome del server, il driver potrebbe restituire le parole chiave per richiedere all'utente per un database. Il processo di esplorazione sarebbe completato dopo l'applicazione ha restituito il nome del database.  
  
 Ogni volta che **SQLBrowseConnect** restituisce una stringa di connessione di risultato Sfoglia nuovo, viene restituito SQL_NEED_DATA come il codice restituito. In questo modo l'applicazione che il processo di connessione non è completato. Fino a quando **SQLBrowseConnect** restituisce SQL_SUCCESS, la connessione è in uno stato dei dati necessari e non può essere utilizzato per altri scopi, ad esempio per impostare un attributo di connessione. L'applicazione può terminare la connessione di esplorazione processo chiamando **SQLDisconnect**.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Esempio di esplorazione di SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
