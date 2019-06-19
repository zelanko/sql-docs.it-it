---
title: Ambiente, connessione e gli attributi di istruzione | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e77be71458eb10e97a82c925d34141a7bcaf1dc4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62943004"
---
# <a name="environment-connection-and-statement-attributes"></a>Attributi relativi ad ambiente, connessione e istruzioni
ODBC definisce una serie di attributi relative agli ambienti, le connessioni o istruzioni.  
  
 Gli attributi di ambiente interessano l'intero ambiente, ad esempio se il pool di connessioni è abilitato. Gli attributi di ambiente vengono impostati con **SQLSetEnvAttr** e recuperate con **SQLGetEnvAttr**.  
  
 Gli attributi di connessione influiscono su ogni connessione singolarmente, ad esempio come tempo deve attendere un driver durante il tentativo di connettersi a un'origine dati prima del timeout. Gli attributi di connessione sono impostati con **SQLSetConnectAttr** e recuperate con **SQLGetConnectAttr**. Per altre informazioni sugli attributi di connessione, vedere [attributi di connessione](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Gli attributi di istruzione interessano singolarmente, ogni istruzione, ad esempio se è necessario eseguire in modo asincrono un'istruzione. Gli attributi di istruzione sono impostati con **SQLSetStmtAttr** e recuperate con **SQLGetStmtAttr**. Alcuni attributi di istruzione sono gli attributi di sola lettura e non possono essere impostati. Ad esempio, l'attributo di istruzione SQL_ATTR_ROW_NUMBER, che viene usato per recuperare il numero di riga corrente nel cursore, è di sola lettura. Per altre informazioni sugli attributi di istruzione, vedere [attributi di istruzione](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Oltre agli attributi definiti da ODBC, è possibile definire un driver la propria connessione e gli attributi di istruzione. Gli attributi definiti dal driver devono essere registrati con Open Group per garantire che due fornitori di driver non assegnano lo stesso valore integer per attributi diversi, proprietari. Per altre informazioni, vedere [tipi di dati specifici del Driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e gli attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Per un elenco completo degli attributi, vedere [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), e [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md). La maggior parte degli attributi sono descritti anche nella descrizione della funzione ODBC che influiscano.
