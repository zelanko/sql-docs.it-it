---
title: Attributi dell'ambiente, della connessione e dell'istruzione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86cecaf0b82c7b6d15b3f37262507d2cff0c3c10
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300931"
---
# <a name="environment-connection-and-statement-attributes"></a>Attributi relativi ad ambiente, connessione e istruzioni
ODBC definisce un numero di attributi associati a ambienti, connessioni o istruzioni.  
  
 Gli attributi dell'ambiente hanno effetto sull'intero ambiente, ad esempio se il pool di connessioni è abilitato. Gli attributi di ambiente vengono impostati con **SQLSetEnvAttr** e recuperati con **SQLGetEnvAttr**.  
  
 Gli attributi di connessione interessano ogni singola connessione, ad esempio il tempo di attesa di un driver durante il tentativo di connessione a un'origine dati prima del timeout. Gli attributi di connessione vengono impostati con **SQLSetConnectAttr** e recuperati con **SQLGetConnectAttr**. Per ulteriori informazioni sugli attributi di connessione, vedere la pagina relativa agli [attributi di connessione](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Gli attributi di istruzione influiscono singolarmente su ogni istruzione, ad esempio se un'istruzione deve essere eseguita in modo asincrono. Gli attributi di istruzione vengono impostati con **SQLSetStmtAttr** e recuperati con **SQLGetStmtAttr**. Alcuni attributi di istruzione sono attributi di sola lettura e non possono essere impostati. Ad esempio, l'attributo SQL_ATTR_ROW_NUMBER Statement, utilizzato per recuperare il numero della riga corrente nel cursore, è di sola lettura. Per ulteriori informazioni sugli attributi dell'istruzione, vedere [attributi di istruzione](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Oltre agli attributi definiti da ODBC, un driver può definire la propria connessione e gli attributi dell'istruzione. Gli attributi definiti dal driver devono essere registrati con il gruppo aperto per garantire che due fornitori di driver non assegni lo stesso valore integer a attributi proprietari diversi. Per ulteriori informazioni, vedere [tipi di dati specifici del driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Per un elenco completo degli attributi, vedere [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)e [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md). La maggior parte degli attributi viene descritta anche nella descrizione della funzione ODBC che interessa.
