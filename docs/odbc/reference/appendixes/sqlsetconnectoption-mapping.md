---
title: 'Mapping di SQLSetConnectOption : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 757b50c7e18133e02b4cf6addaa327b2053f5439
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287471"
---
# <a name="sqlsetconnectoption-mapping"></a>Mapping di SQLSetConnectOption
Quando un ODBC 2. *x* chiama **SQLSetConnectOption** tramite un driver *.x* ODBC 3, la chiamata a  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 come segue:  
  
-   Se *fOption* indica un attributo di connessione definito da ODBC che richiede una stringa, Gestione Driver chiama  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   Se *fOption* indica un attributo di connessione definito da ODBC che restituisce un valore integer a 32 bit, Gestione Driver chiama  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   Se *fOption* indica un attributo di connessione definito dal driver, Gestione Driver chiama  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 Nei tre casi precedenti, l'argomento *ConnectionHandle* è impostato sul valore in *hdbc*, l'argomento *Attribute* è impostato sul valore in *fOption*e l'argomento *ValuePtr* è impostato sullo stesso valore di *vParam*.  
  
 Poiché Gestione Driver non sa se l'attributo di connessione definito dal driver richiede una stringa o un valore integer a 32 bit, deve passare un valore valido per il *BufferLength* argomento di **SQLSetConnectAttr**. Se il driver ha definito una semantica speciale per gli attributi di connessione definiti dal driver e deve essere chiamato utilizzando **SQLSetConnectOption**, deve supportare **SQLSetConnectOption**.  
  
 Se un ODBC 2. *x* applicazione chiama **SQLSetConnectOption** per impostare un'opzione di istruzione specifica del driver in un driver ODBC 3 *.x* e l'opzione è stata definita in un ODBC 2. *x* versione del driver, una nuova costante manifesto deve essere definita per l'opzione nel driver ODBC 3 *.x.* Se la costante del manifesto precedente viene utilizzata nella chiamata a **SQLSetConnectOption**, Gestione Driver chiamerà **SQLSetConnectAttr** con il **StringLength** argomento impostato su 0.  
  
 Per un driver *.x* ODBC 3, Gestione Driver non controlla più se *fOption* è tra SQL_CONN_OPT_MIN e SQL_CONN_OPT_MAX o è maggiore di SQL_CONNECT_OPT_DRVR_START.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>Impostazione delle opzioni di istruzione a livello di connessioneSetting Statement Options on the Connection Level  
 In ODBC 2. *x*, un'applicazione può chiamare **SQLSetConnectOption** per impostare un'opzione di istruzione. Al termine, il driver stabilisce l'opzione di istruzione come valore predefinito per tutte le istruzioni allocate successivamente per la connessione. È definito dal driver se il driver imposta l'opzione di istruzione per tutte le istruzioni esistenti associate alla connessione specificata.  
  
 Questa funzionalità è stata deprecata in ODBC 3 *.x*. I driver ODBC 3 *.x* richiedono solo l'impostazione ODBC 2. attributi dell'istruzione *x* a livello di connessione se desiderano utilizzare ODBC 2. *x* applicazioni che eseguono questa operazione. Le applicazioni *.x* ODBC 3 non devono mai impostare gli attributi dell'istruzione a livello di connessione. Gli attributi dell'istruzione ODBC 3 *.x* non possono essere impostati a livello di connessione, ad eccezione degli attributi SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, che sono entrambi attributi di connessione e attributi dell'istruzione e possono essere impostati a livello di connessione o di istruzione.
