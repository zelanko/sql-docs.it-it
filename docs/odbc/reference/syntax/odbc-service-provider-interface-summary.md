---
title: Riepilogo dell'interfaccia del provider di servizi ODBC Documenti Microsoft
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
ms.openlocfilehash: b2f7e459cc7b89106bf1b7ebcd49c699d43da9f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298898"
---
# <a name="odbc-service-provider-interface-summary"></a>Riepilogo dell'interfaccia del provider di servizi ODBC
Nella tabella seguente vengono descritte le funzioni di interfaccia del provider di servizi ODBC. Per ulteriori informazioni sulla sintassi e la semantica per ogni funzione, vedere riferimento all'interfaccia del provider di [servizi ODBC (SPI).](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)  
  
|Nome della funzione|Scopo|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Uguale a [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), ma imposta l'attributo nel token di informazioni di connessione anziché sull'handle di connessione.|  
|[SQLSetDriverConnectInfo (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|Imposta la stringa di connessione nel token delle informazioni di connessione per la chiamata [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) di un'applicazione.|  
|[SQLSetConnectInfo (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Imposta l'origine dati, l'ID utente e la password nel token di informazioni di connessione per la chiamata [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) di un'applicazione.|  
|[SQLGetPoolID (IDSQLGetPoolID)](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Recupera l'ID del pool.|  
|[SQLRateConnection (connessione SQLRateConnection)](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Determina se un driver può riutilizzare una connessione esistente nel pool di connessioni.|  
|[SQLPoolConnect (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Creare una nuova connessione se non è possibile riutilizzare alcuna connessione nel pool.|  
|[SQLCleanupConnectionPoolID (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Informa un driver che è stato sfornato un ID pool.|
