---
title: Gli attributi di connessione | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09b29277d74383abff1510ca7394aecad036fc7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036445"
---
# <a name="connection-attributes"></a>Attributi di connessione
Gli attributi di connessione sono illustrate le caratteristiche della connessione. Poiché ad esempio le transazioni si verificano al livello della connessione, il livello di isolamento delle transazioni è un attributo di connessione. Analogamente, il timeout di accesso o il numero di secondi di attesa durante il tentativo di connessione prima del timeout, è un attributo di connessione.  
  
 Gli attributi di connessione sono impostati con **SQLSetConnectAttr** e le relative impostazioni correnti recuperati con **SQLGetConnectAttr**. Se **SQLSetConnectAttr** viene chiamato prima che il driver viene caricato, il Driver Manager archivia gli attributi nella relativa struttura di connessione e li imposta nel driver come parte del processo di connessione. Non è necessario che un'applicazione impostare eventuali attributi di connessione. tutti gli attributi di connessione hanno impostazioni predefinite, alcune delle quali sono specifici del driver.  
  
 Un attributo di connessione può essere impostato prima o dopo la connessione, o entrambi, a seconda dell'attributo e il driver. Il timeout di accesso (SQL_ATTR_LOGIN_TIMEOUT) si applica al processo di connessione ed è efficace solo se è impostato prima della connessione. Gli attributi che specificano se usare la libreria di cursori ODBC (SQL_ATTR_ODBC_CURSORS) e le dimensioni del pacchetto di rete (SQL_ATTR_PACKET_SIZE) devono essere impostati prima della connessione, poiché la libreria di cursori ODBC si trova tra la gestione di Driver e il driver e di conseguenza deve essere caricato prima del driver.  
  
 Gli attributi per specificare se un'origine dati è di sola lettura o lettura / scrittura (SQL_ATTR_ACCESS_MODE) e il catalogo corrente (SQL_ATTR_CURRENT_CATALOG) possono essere impostati prima o dopo la connessione, a seconda del driver. Tuttavia, applicazioni interoperative impostarli prima della connessione in quanto alcuni driver non supportano la modifica di questi dopo la connessione.  
  
 Alcuni attributi di connessione prevedono un valore predefinito prima che venga effettuata la connessione, mentre altre no. Quelli che si sono SQL_ATTR_ACCESS_MODE SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE e SQL_ATTR_TRACEFILE.  
  
 Gli attributi di connessione di traduzione (SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION) devono essere impostati dopo la connessione.  
  
 Tutti gli altri attributi di connessione possono essere impostate in qualsiasi momento. Per altre informazioni, vedere la [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descrizione della funzione. (Gli attributi di connessione nelze nastavit il livello di ambiente da una chiamata a **SQLSetEnvAttr**.)
