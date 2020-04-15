---
title: Cenni preliminari su ODBC - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a0515a882cd7d1c97a60e9262942bd7c397b0b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298291"
---
# <a name="odbc-overview"></a>Panoramica di ODBC
Open Database Connectivity (ODBC) è un'API (Application Programming Interface) ampiamente accettata per l'accesso al database. Si basa sulle specifiche CLI (Call-Level Interface) di Open Group e ISO/IEC per le API di database e utilizza SQL (Structured Query Language) come linguaggio di accesso al database.  
  
 ODBC è progettato per la massima *interoperabilità,* ovvero la capacità di una singola applicazione di accedere a sistemi di gestione di database diversi (DBS) con lo stesso codice sorgente. Le applicazioni di database chiamano le funzioni nell'interfaccia ODBC, implementate in moduli specifici del database *denominati driver*. L'uso dei driver isola le applicazioni dalle chiamate specifiche del database nello stesso modo in cui i driver della stampante isolano i programmi di elaborazione testi dai comandi specifici della stampante. Poiché i driver vengono caricati in fase di esecuzione, un utente deve solo aggiungere un nuovo driver per accedere a un nuovo DBMS; non è necessario ricompilare o ricollegare l'applicazione.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Perché è stato creato ODBC?](../../odbc/reference/why-was-odbc-created.md)  
  
-   [Che cos'è ODBC?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC e l'interfaccia della riga di comando standard](../../odbc/reference/odbc-and-the-standard-cli.md)
