---
description: Riepilogo dell'interfaccia del provider di servizi ODBC
title: Riepilogo dell'interfaccia del provider di servizi ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00d15d33fba1e697eebbe6a640c4f8a4d8eadea7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487344"
---
# <a name="odbc-service-provider-interface-summary"></a>Riepilogo dell'interfaccia del provider di servizi ODBC
Nella tabella seguente vengono descritte le funzioni di interfaccia del provider di servizi ODBC. Per ulteriori informazioni sulla sintassi e la semantica per ogni funzione, vedere [riferimento a ODBC Service Provider Interface (SPI)](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md).  
  
|Nome della funzione|Scopo|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Uguale a [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), ma imposta l'attributo sul token delle informazioni di connessione anziché sull'handle di connessione.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|Imposta la stringa di connessione nel token delle informazioni di connessione per la chiamata [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) di un'applicazione.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Imposta l'origine dati, l'ID utente e la password nel token di informazioni di connessione per la chiamata [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) di un'applicazione.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Recupera l'ID del pool.|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Determina se un driver può riutilizzare una connessione esistente nel pool di connessioni.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Crea una nuova connessione se non è possibile riutilizzare una connessione nel pool.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Informa un driver che è stato raggiunto il timeout di un ID pool.|
