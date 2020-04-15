---
title: Maniglie di connessione Documenti Microsoft
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
ms.openlocfilehash: d5b03e0733e35984350d2a218b885dc148ca8f8f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299021"
---
# <a name="connection-handles"></a>Handle di connessione
Una *connessione* è costituita da un driver e da un'origine dati. Un handle di connessione identifica ogni connessione. L'handle di connessione definisce non solo il driver da utilizzare, ma l'origine dati da utilizzare con tale driver. All'interno di un segmento di codice che implementa ODBC (Gestione Driver o un driver), l'handle di connessione identifica una struttura che contiene informazioni di connessione, ad esempio:  
  
-   Lo stato della connessione  
  
-   La diagnostica a livello di connessione corrente  
  
-   Gli handle delle dichiarazioni e dei descrittori attualmente allocati sulla connessione  
  
-   Le impostazioni correnti di ogni attributo di connessione  
  
 ODBC non impedisce più connessioni simultanee, se il driver le supporta. Pertanto, in un particolare ambiente ODBC, più handle di connessione potrebbero puntare a una varietà di driver e origini dati, allo stesso driver e una varietà di origini dati o anche a più connessioni allo stesso driver e origine dati. Alcuni driver limitano il numero di connessioni attive supportate; l'opzione SQL_MAX_DRIVER_CONNECTIONS in **SQLGetInfo** specifica il numero di connessioni attive supportate da un driver specifico.  
  
 Gli handle di connessione vengono utilizzati principalmente per la connessione all'origine dati (**SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**), la disconnessione dall'origine dati (**SQLDisconnect**), il recupero di informazioni sul driver e sull'origine dati (**SQLGetInfo**), il recupero della diagnostica (**SQLGetDiagField** e **SQLGetDiagRec**) e l'esecuzione di transazioni (**SQLEndTran**). Vengono inoltre utilizzati durante l'impostazione e il recupero degli attributi di connessione (**SQLSetConnectAttr** e **SQLGetConnectAttr**) e per ottenere il formato nativo di un'istruzione SQL (**SQLNativeSql**).  
  
 Gli handle di connessione vengono allocati con **SQLAllocHandle** e liberati con **SQLFreeHandle**.
