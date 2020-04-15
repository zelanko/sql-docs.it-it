---
title: Attributi di connessione Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c295ce88eedf1d4cddc4173f5dea39c44b01f83d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299042"
---
# <a name="connection-attributes"></a>Attributi di connessione
Gli attributi di connessione sono caratteristiche della connessione. Poiché ad esempio le transazioni si verificano al livello della connessione, il livello di isolamento delle transazioni è un attributo di connessione. Analogamente, il timeout di accesso o il numero di secondi di attesa durante il tentativo di connessione prima del timeout, è un attributo di connessione.  
  
 Gli attributi di connessione vengono impostati con **SQLSetConnectAttr** e le relative impostazioni correnti recuperate con **SQLGetConnectAttr**. Se **SQLSetConnectAttr** viene chiamato prima del caricamento del driver, Gestione Driver archivia gli attributi nella relativa struttura di connessione e li imposta nel driver come parte del processo di connessione. Non è necessario che un'applicazione imposti attributi di connessione; tutti gli attributi di connessione hanno valori predefiniti, alcuni dei quali sono specifici del driver.  
  
 Un attributo di connessione può essere impostato prima o dopo la connessione o uno dei due, a seconda dell'attributo e del driver. Il timeout di accesso (SQL_ATTR_LOGIN_TIMEOUT) si applica al processo di connessione ed è valido solo se impostato prima della connessione. Gli attributi che specificano se utilizzare la libreria di cursori ODBC (SQL_ATTR_ODBC_CURSORS) e la dimensione del pacchetto di rete (SQL_ATTR_PACKET_SIZE) devono essere impostati prima della connessione, perché la libreria di cursori ODBC si trova tra Gestione Driver e il driver e pertanto deve essere caricato prima del driver.  
  
 Gli attributi per specificare se un'origine dati è di sola lettura o di lettura-scrittura (SQL_ATTR_ACCESS_MODE) e il catalogo corrente (SQL_ATTR_CURRENT_CATALOG) può essere impostato prima o dopo la connessione, a seconda del driver. Tuttavia, le applicazioni interoperabili le impostano prima della connessione perché alcuni driver non supportano la modifica di questi dopo la connessione.  
  
 Alcuni attributi di connessione hanno un valore predefinito prima che venga stabilita la connessione, mentre altri no. Quelli che lo fanno sono SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE e SQL_ATTR_TRACEFILE.  
  
 Gli attributi di connessione di traslazione (SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION) devono essere impostati dopo la connessione.  
  
 Tutti gli altri attributi di connessione possono essere impostati in qualsiasi momento. Per altre informazioni, vedere la descrizione della funzione [SQLSetConnectAttr.For](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) more information, see the SQLSetConnectAttr function description. Gli attributi di connessione non possono essere impostati a livello di ambiente da una chiamata a **SQLSetEnvAttr.**
