---
title: Connessione con SQLBrowseConnect | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4d738d394bb3c507f6aa08f736016b51ac4fefb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294661"
---
# <a name="connecting-with-sqlbrowseconnect"></a>Connessione con SQLBrowseConnect
**SQLBrowseConnect**, ad esempio **SQLDriverConnect**, usa una stringa di connessione. Tuttavia, usando **SQLBrowseConnect**, un'applicazione può costruire una stringa di connessione completa in fase di esecuzione. In questo modo, l'applicazione può eseguire due operazioni:  
  
-   Creare finestre di dialogo personalizzate per richiedere queste informazioni, mantenendo al contempo il controllo sull'aspetto.  
  
-   Esplorare il sistema per individuare origini dati che possano essere utilizzate da un driver specifico, possibilmente in diversi passaggi. L'utente, ad esempio, potrebbe esplorare innanzitutto la rete per individuare i server e, dopo averne scelto uno, esplorare il server per individuare i database accessibili dal driver.  
  
 L'applicazione chiama **SQLBrowseConnect** e passa una stringa di connessione, nota come *stringa di connessione della richiesta browse,* che specifica un driver o un'origine dati. Il driver restituisce una stringa di connessione, nota come *stringa di connessione del risultato browse,* che contiene parole chiave, valori possibili (se la parola chiave accetta un set discreto di valori) e nomi descrittivi. L'applicazione compila una finestra di dialogo con i nomi descrittivi e chiede all'utente i valori. Compila quindi una nuova stringa di connessione di richiesta browse da questi valori e la restituisce al driver con un'altra chiamata a **SQLBrowseConnect**.  
  
 Poiché le stringhe di connessione vengono passate in avanti e indietro, il driver può fornire diversi livelli di esplorazione restituendo una nuova stringa di connessione quando l'applicazione restituisce quello precedente. Ad esempio, la prima volta che un'applicazione chiama **SQLBrowseConnect**, il driver potrebbe restituire parole chiave per richiedere all'utente un nome di server. Quando l'applicazione restituisce il nome del server, il driver potrebbe restituire parole chiave per richiedere all'utente un database. Il processo di esplorazione verrà completato dopo che l'applicazione ha restituito il nome del database.  
  
 Ogni volta che **SQLBrowseConnect** restituisce una nuova stringa di connessione del risultato browse, restituisce SQL_NEED_DATA come codice restituito. Indica all'applicazione che il processo di connessione non è completo. Fino a quando **SQLBrowseConnect** non restituisce SQL_SUCCESS, la connessione è in uno stato di dati necessario e non può essere usata per altri scopi, ad esempio per impostare un attributo di connessione. L'applicazione può terminare il processo di esplorazione della connessione chiamando **Disconnect**.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Esempio di esplorazione di SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
