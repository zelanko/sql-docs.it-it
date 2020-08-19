---
description: Handle di connessione
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a4457fa72c40892e208057ac013d3da1e557a6d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424793"
---
# <a name="connection-handles"></a>Handle di connessione
Una *connessione* è costituita da un driver e da un'origine dati. Un handle di connessione identifica ogni connessione. L'handle di connessione definisce non solo il driver da usare ma l'origine dati da usare con tale driver. All'interno di un segmento di codice che implementa ODBC (Gestione driver o driver), l'handle di connessione identifica una struttura che contiene le informazioni di connessione, come le seguenti:  
  
-   Stato della connessione  
  
-   Diagnostica a livello di connessione corrente  
  
-   Handle di istruzioni e descrittori attualmente allocati nella connessione  
  
-   Impostazioni correnti di ogni attributo di connessione  
  
 ODBC non impedisce più connessioni simultanee, se supportate dal driver. In un particolare ambiente ODBC, quindi, più handle di connessione potrebbero puntare a un'ampia gamma di driver e origini dati, allo stesso driver e a una varietà di origini dati o anche a più connessioni allo stesso driver e all'origine dati. Alcuni driver limitano il numero di connessioni attive supportate; l'opzione SQL_MAX_DRIVER_CONNECTIONS in **SQLGetInfo** specifica il numero di connessioni attive supportate da un determinato driver.  
  
 Gli handle di connessione vengono utilizzati principalmente per la connessione all'origine dati (**SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**), la disconnessione dall'origine dati (**SQLConnect**), il recupero di informazioni sul driver e l'origine dati (**SQLGetInfo**), il recupero di diagnostica (**SQLGetDiagField** e **SQLGetDiagRec**) e l'esecuzione di transazioni (**SQLEndTran**). Vengono inoltre utilizzati durante l'impostazione e il recupero degli attributi di connessione (**SQLSetConnectAttr** e **SQLGetConnectAttr**) e quando si recupera il formato nativo di un'istruzione SQL (**SQLNativeSql**).  
  
 Gli handle di connessione vengono allocati con **SQLAllocHandle** e liberati con **SQLFreeHandle**.
