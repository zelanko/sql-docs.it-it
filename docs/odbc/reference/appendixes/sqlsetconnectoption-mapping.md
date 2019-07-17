---
title: Mapping di SQLSetConnectOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b512a795c3b9e2d1c6aa1c7c9e92fbc42a8c7862
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125587"
---
# <a name="sqlsetconnectoption-mapping"></a>Mapping di SQLSetConnectOption
Quando un'applicazione ODBC 2. *x* applicazione chiama **SQLSetConnectOption** tramite un'applicazione ODBC 3*x* driver, la chiamata a  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 verrà generato come indicato di seguito:  
  
-   Se *fOption* indica un attributo di connessione definite da ODBC che richiede una stringa, le chiamate di gestione Driver  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   Se *fOption* indica un attributo di connessione definite da ODBC che restituisce un valore integer a 32 bit, le chiamate di gestione Driver  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   Se *fOption* indica un attributo di connessione definiti dal driver, le chiamate di gestione Driver  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 Nei tre casi precedenti, il *ConnectionHandle* argomento è impostato sul valore *hdbc*, il *attributo* argomento è impostato sul valore in *fOption* e il *ValuePtr* argomento è impostato sullo stesso valore come *vParam*.  
  
 Poiché gestione Driver non sa se l'attributo di connessione definiti dal driver necessita di una stringa o un valore integer a 32 bit, deve passare un valore valido per il *BufferLength* argomento di **SQLSetConnectAttr**. Se il driver è definita la semantica speciale per definito dal driver connettere gli attributi e deve essere chiamato utilizzando **SQLSetConnectOption**, deve supportare **SQLSetConnectOption**.  
  
 Se un ODBC 2. *x* applicazione chiama **SQLSetConnectOption** per impostare un'opzione di istruzione specifici del driver in un'applicazione ODBC 3*x* driver e l'opzione è stata definita in un'API ODBC 2. *x* versione del driver, una nuova costante manifesto deve essere definito per l'opzione in ODBC 3*x* driver. Se la costante manifesto precedente viene usata nella chiamata a **SQLSetConnectOption**, il Driver Manager chiamerà **SQLSetConnectAttr** con il **StringLength** argomento impostato su 0.  
  
 Per un'applicazione ODBC 3 *. x* driver, gestione Driver non controlla se *fOption* compresa tra SQL_CONN_OPT_MIN e SQL_CONN_OPT_MAX, oppure è maggiore di SQL_CONNECT_OPT_DRVR_START.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>Impostazione di opzioni di istruzione per il livello di connessione  
 In ODBC 2. *x*, un'applicazione potrebbe chiamare **SQLSetConnectOption** per impostare un'opzione di istruzione. Al termine, il driver stabilisce l'opzione dell'istruzione per impostazione predefinita per le istruzioni in un secondo momento allocate per la connessione. Si è definito dal driver se il driver imposta l'opzione dell'istruzione per le istruzioni esistenti associate alla connessione specificata.  
  
 Questa funzionalità è stata deprecata in ODBC 3*x*. ODBC 3 *. x* i driver necessitano supportano solo l'impostazione di ODBC 2. *x* attributi di istruzione a livello di connessione se vogliono lavorare con l'API ODBC 2. *x* le applicazioni che eseguono questa operazione. ODBC 3*x* applicazioni non devono mai impostato gli attributi di istruzione a livello di connessione. ODBC 3*x* gli attributi di istruzione non possono essere impostati a livello di connessione, fatta eccezione per gli attributi SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, che sono entrambi gli attributi di connessione e gli attributi di istruzione e può essere impostare a livello di connessione o il livello di istruzione.
