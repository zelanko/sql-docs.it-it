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
ms.openlocfilehash: 945ebced0703c109ac64c374e31d2e76b556e7ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67944830"
---
# <a name="odbc-overview"></a>Panoramica di ODBC
Open Database Connectivity (ODBC) è un'Application Programming Interface (API) ampiamente accettata per l'accesso al database. Si basa sulle specifiche CLI (Call-Level Interface) di Open Group e ISO/IEC per le API di database e USA Structured Query Language (SQL) come linguaggio di accesso al database.  
  
 ODBC è progettato per garantire la massima *interoperabilità* , ovvero la capacità di una singola applicazione di accedere a diversi sistemi di gestione di database (DBMS) con lo stesso codice sorgente. Le applicazioni di database chiamano funzioni nell'interfaccia ODBC, implementate in moduli specifici del database denominati *driver*. L'utilizzo di driver consente di isolare le applicazioni da chiamate specifiche del database nello stesso modo in cui i driver della stampante isolano i programmi di elaborazione di Word da comandi specifici della stampante. Poiché i driver vengono caricati in fase di esecuzione, un utente deve solo aggiungere un nuovo driver per accedere a un nuovo sistema DBMS. non è necessario ricompilare o ricollegare l'applicazione.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Motivi per la creazione di ODBC](../../odbc/reference/why-was-odbc-created.md)  
  
-   [Informazioni su ODBC](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC e l'interfaccia della riga di comando standard](../../odbc/reference/odbc-and-the-standard-cli.md)
