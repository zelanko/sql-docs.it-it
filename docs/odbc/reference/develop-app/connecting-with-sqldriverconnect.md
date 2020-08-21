---
title: Connessione con SQLDriverConnect | Microsoft Docs
description: SQLDriverConnect fornisce funzionalità aggiuntive per la connessione tramite SQLConnect, incluse le opzioni per richiedere all'utente ulteriori informazioni.
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78186e903405aa1b59cfac185e62646dbda6e77a
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2020
ms.locfileid: "88746171"
---
# <a name="connecting-with-sqldriverconnect"></a>Connessione con SQLDriverConnect

**SQLDriverConnect** viene utilizzato per connettersi a un'origine dati utilizzando una stringa di connessione. **SQLDriverConnect** viene usato al posto di **SQLConnect** per gli scenari seguenti:  
  
- Stabilire una connessione utilizzando una stringa di connessione che contiene il nome dell'origine dati, uno o più ID utente, una o più password e altre informazioni richieste dall'origine dati.  
  
- Stabilire una connessione utilizzando una stringa di connessione parziale o senza informazioni aggiuntive. in tal caso, gestione driver e il driver possono richiedere all'utente le informazioni di connessione.  
  
- Stabilire una connessione a un'origine dati non definita nelle informazioni di sistema. Se l'applicazione fornisce una stringa di connessione parziale, il driver può richiedere all'utente le informazioni di connessione.  
  
- Stabilire una connessione a un'origine dati utilizzando una stringa di connessione costruita dalle informazioni contenute in un file con estensione DSN.  
  
Dopo che è stata stabilita una connessione, **SQLDriverConnect** restituisce la stringa di connessione completata. L'applicazione può usare questa stringa per le richieste di connessione successive.

In questa sezione vengono trattati gli argomenti seguenti.  
  
- [Informazioni di connessione specifiche del driver](driver-specific-connection-information.md)  
  
- [Chiedere all'utente informazioni di connessione](prompting-the-user-for-connection-information.md)  
  
- [Connessione tramite origini dati dei file](connecting-using-file-data-sources.md)  
  
- [Connessione diretta ai driver](connecting-directly-to-drivers.md)
