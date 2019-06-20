---
title: Panoramica di ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b064436dae6cb2f3d5f37fa02ab57a1e4a3f015
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63272934"
---
# <a name="odbc-overview"></a>Panoramica di ODBC
Open Database Connectivity (ODBC) è una diffuso API application programming interface () per l'accesso al database. Si basa sulle specifiche a livello di chiamata Interface (CLI) di Open Group e ISO/IEC per API di database e Usa Structured Query Language (SQL) come lingua del database l'accesso.  
  
 ODBC è progettato per massimo *interoperabilità* -, ovvero la possibilità di una singola applicazione di accedere ai sistemi di gestione di diversi database (DBMS) con lo stesso codice sorgente. Le applicazioni del database chiamano funzioni nell'interfaccia di ODBC, che vengono implementate nei moduli specifici del database denominati *driver*. L'uso dei driver consente di isolare le applicazioni dalle chiamate specifiche del database nello stesso modo che i driver della stampante isolare i programmi di elaborazione di testi da comandi specifici della stampante. Poiché i driver vengono caricati in fase di esecuzione, un utente deve solo aggiungere un nuovo driver per accedere a un nuovo DBMS; non è necessario ricompilare o ricollegare all'applicazione.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Perché è stato creato ODBC?](../../odbc/reference/why-was-odbc-created.md)  
  
-   [Che cos'è ODBC?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC e l'interfaccia della riga di comando standard](../../odbc/reference/odbc-and-the-standard-cli.md)
