---
title: Handle di connessione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77fdb63f346ada40346544a53c3ff69db0a8a9a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280844"
---
# <a name="connection-handles"></a>Handle di connessione
Oggetto *connessione* è costituito da un driver e un'origine dati. Un handle di connessione identifica ogni connessione. L'handle di connessione definisce non solo il driver da usare, ma l'origine dati da utilizzare con tale driver. All'interno di un segmento di codice che implementa ODBC (gestione Driver o un driver), l'handle di connessione identifica una struttura che contiene informazioni di connessione, ad esempio il seguente:  
  
-   Lo stato della connessione  
  
-   La diagnostica a livello di connessione corrente  
  
-   Gli handle delle istruzioni e i descrittori allocati per la connessione  
  
-   Le impostazioni correnti di ogni attributo di connessione  
  
 ODBC non impedisce più connessioni simultanee, se il driver supportarle. Pertanto, in un ambiente ODBC specifico, più handle di connessione potrebbero fare riferimento a un'ampia gamma di driver e origini dati per lo stesso driver e una varietà di origini dati, o anche a più connessioni allo stesso driver e origine dati. Alcuni driver limitare il numero di connessioni attive che supportano; opzione il SQL_MAX_DRIVER_CONNECTIONS **SQLGetInfo** specifica il numero di connessioni attivo supporta un driver specifico.  
  
 Handle di connessione vengono utilizzati principalmente per la connessione all'origine dati (**SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect**), disconnessione dai dati origine (**SQLDisconnect**), recupero di informazioni relative all'origine dati e del driver (**SQLGetInfo**), il recupero di diagnostica (**SQLGetDiagField** e **SQLGetDiagRec**) e l'esecuzione di transazioni (**SQLEndTran**). Vengono usati anche quando l'impostazione e recupero di attributi di connessione (**SQLSetConnectAttr** e **SQLGetConnectAttr**) e quando si recupera il formato nativo di un'istruzione SQL (**SQLNativeSql** ).  
  
 Handle di connessione vengono allocati con **SQLAllocHandle** e liberati con **SQLFreeHandle**.
