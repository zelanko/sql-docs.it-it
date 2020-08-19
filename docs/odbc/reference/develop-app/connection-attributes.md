---
description: Attributi di connessione
title: Attributi di connessione | Microsoft Docs
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
ms.openlocfilehash: a7db2fb6361f114f4864436116f5b0f2f5651e79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424803"
---
# <a name="connection-attributes"></a>Attributi di connessione
Gli attributi di connessione sono caratteristiche della connessione. Poiché ad esempio le transazioni si verificano al livello della connessione, il livello di isolamento delle transazioni è un attributo di connessione. Analogamente, il timeout di accesso o il numero di secondi di attesa durante il tentativo di connessione prima del timeout, è un attributo di connessione.  
  
 Gli attributi di connessione vengono impostati con **SQLSetConnectAttr** e le impostazioni correnti recuperate con **SQLGetConnectAttr**. Se **SQLSetConnectAttr** viene chiamato prima del caricamento del driver, gestione driver archivia gli attributi nella relativa struttura di connessione e li imposta nel driver come parte del processo di connessione. Non è necessario che un'applicazione imposti attributi di connessione; per tutti gli attributi di connessione sono disponibili impostazioni predefinite, alcune delle quali sono specifiche del driver.  
  
 Un attributo di connessione può essere impostato prima o dopo la connessione oppure, a seconda dell'attributo e del driver. Il timeout di accesso (SQL_ATTR_LOGIN_TIMEOUT) si applica al processo di connessione ed è efficace solo se impostato prima della connessione. Gli attributi che specificano se utilizzare la libreria di cursori ODBC (SQL_ATTR_ODBC_CURSORS) e le dimensioni del pacchetto di rete (SQL_ATTR_PACKET_SIZE) devono essere impostati prima della connessione, perché la libreria di cursori ODBC risiede tra Gestione driver e il driver e pertanto deve essere caricata prima del driver.  
  
 Gli attributi per specificare se un'origine dati è di sola lettura o di lettura/scrittura (SQL_ATTR_ACCESS_MODE) ed è possibile impostare il catalogo corrente (SQL_ATTR_CURRENT_CATALOG) prima o dopo la connessione, a seconda del driver. Tuttavia, le applicazioni interoperative le impostano prima della connessione perché alcuni driver non supportano la modifica di questi elementi dopo la connessione.  
  
 Alcuni attributi di connessione hanno un valore predefinito prima della connessione, mentre altri no. Ovvero SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE e SQL_ATTR_TRACEFILE.  
  
 È necessario impostare gli attributi di connessione di conversione (SQL_ATTR_TRANSLATE_DLL e SQL_ATTR_TRANSLATE_OPTION) dopo la connessione.  
  
 Tutti gli altri attributi di connessione possono essere impostati in qualsiasi momento. Per ulteriori informazioni, vedere la descrizione della funzione [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) . Non è possibile impostare gli attributi di connessione a livello di ambiente mediante una chiamata a **SQLSetEnvAttr**.
