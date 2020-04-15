---
title: Connessione con SQLBrowseConnect Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294661"
---
# <a name="connecting-with-sqlbrowseconnect"></a>Connessione con SQLBrowseConnect
**SQLBrowseConnect**, come **SQLDriverConnect**, utilizza una stringa di connessione. Tuttavia, utilizzando **SQLBrowseConnect**, un'applicazione può costruire una stringa di connessione completa in fase di esecuzione. In questo modo, l'applicazione può eseguire due operazioni:  
  
-   Creare le proprie finestre di dialogo per richiedere queste informazioni, mantenendo così il controllo sull'aspetto.  
  
-   Esplorare il sistema per individuare origini dati che possano essere utilizzate da un driver specifico, possibilmente in diversi passaggi. L'utente, ad esempio, potrebbe esplorare innanzitutto la rete per individuare i server e, dopo averne scelto uno, esplorare il server per individuare i database accessibili dal driver.  
  
 L'applicazione chiama **SQLBrowseConnect** e passa una stringa di connessione, nota come stringa di *connessione richiesta Sfoglia,* che specifica un driver o un'origine dati. Il driver restituisce una stringa di connessione, nota come stringa di *connessione risultato Sfoglia,* che contiene parole chiave, valori possibili (se la parola chiave accetta un set discreto di valori) e nomi descrittivi. L'applicazione compila una finestra di dialogo con i nomi descrittivi e richiede all'utente i valori. Viene quindi compilata una nuova stringa di connessione richiesta sfoglia da questi valori e restituisce questo al driver con un'altra chiamata a **SQLBrowseConnect**.  
  
 Poiché le stringhe di connessione vengono passate avanti e indietro, il driver può fornire diversi livelli di esplorazione restituendo una nuova stringa di connessione quando l'applicazione restituisce quella precedente. Ad esempio, la prima volta che un'applicazione chiama **SQLBrowseConnect**, il driver potrebbe restituire parole chiave per richiedere all'utente un nome server. Quando l'applicazione restituisce il nome del server, il driver potrebbe restituire parole chiave per richiedere all'utente di un database. Il processo di esplorazione sarà completo dopo che l'applicazione ha restituito il nome del database.  
  
 Ogni volta che **SQLBrowseConnect** restituisce una nuova stringa di connessione risultato Sfoglia, restituisce SQL_NEED_DATA come codice restituito. Ciò indica all'applicazione che il processo di connessione non è completo. Fino a quando **SQLBrowseConnect** non restituisce SQL_SUCCESS, la connessione è in uno stato di dati necessari e non può essere utilizzata per altri scopi, ad esempio per impostare un attributo di connessione. L'applicazione può terminare il processo di esplorazione della connessione chiamando **SQLDisconnect**.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Esempio di esplorazione di SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
