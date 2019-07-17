---
title: Modifiche del comportamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fc9f8dcc3782204c8bf1c9add1200e451edcf127
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103870"
---
# <a name="behavioral-changes"></a>Modifiche del comportamento
Modifiche del comportamento sono le modifiche per il quale il *sintassi* dell'interfaccia rimane invariato, ma la *semantica* sono stati modificati. Per queste modifiche, la funzionalità usata in ODBC 2. *x* si comporta in modo diverso rispetto alla stessa funzionalità in ODBC 3. *x*.  
  
 Indica se un'applicazione presenta ODBC 2. *x* comportamento o ODBC 3. *x* comportamento è determinato dall'attributo SQL_ATTR_ODBC_VERSION ambiente. Questo valore a 32 bit è impostato su SQL_OV_ODBC2 può presentare ODBC 2. *x* comportamento e SQL_OV_ODBC3 può presentare ODBC 3. *x* comportamento.  
  
 L'attributo di ambiente SQL_ATTR_ODBC_VERSION è impostato da una chiamata a **SQLSetEnvAttr**. Dopo che un'applicazione chiama **SQLAllocHandle** per allocare un handle di ambiente, è necessario chiamare**SQLSetEnvAttr** immediatamente per impostare il comportamento presenta. (Di conseguenza, vi è un nuovo stato dell'ambiente per descrivere l'handle di ambiente in un allocata, ma versionless, lo stato). Per altre informazioni, vedere [appendice b: Tabelle della transizione di stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Un'applicazione indica quale problema presenta con l'attributo di ambiente SQL_ATTR_ODBC_VERSION, ma l'attributo non ha alcun effetto sulla connessione dell'applicazione con un'API ODBC 2. *x* o ODBC 3. *x* driver. Un database ODBC 3. *x* applicazione può connettersi a una delle due un ODBC 2. *x* o 3. *x* driver, indipendentemente da quali l'impostazione dell'attributo environment.  
  
 ODBC 3. *x* le applicazioni non devono mai chiamare **SQLAllocEnv**. Di conseguenza, se Gestione Driver riceve una chiamata a **SQLAllocEnv**, che riconosce l'applicazione come un'API ODBC 2. *x* dell'applicazione.  
  
 L'attributo SQL_ATTR_ODBC_VERSION influisce su tre diversi aspetti di un'applicazione ODBC 3. *x* comportamento del driver:  
  
-   SQLSTATE  
  
-   Tipi di dati per data, ora e timestamp  
  
-   Il *CatalogName* nell'argomento **SQLTables** accetta i criteri di ricerca in ODBC 3. *x*, ma non in ODBC 2. *x*  
  
 L'impostazione dell'attributo environment SQL_ATTR_ODBC_VERSION non interessa **SQLSetParam** oppure **SQLBindParam**. **SQLColAttribute** non è influenzato da tale bit. Sebbene **SQLColAttribute** restituisce gli attributi che sono interessati dalla versione di ODBC (tipo di dati, precisione, scala e lunghezza), il comportamento previsto è determinato dal valore della *FieldIdentifier*argomento. Quando *FieldIdentifier* è uguale a, SQL_DESC_TYPE **SQLColAttribute** restituisce ODBC 3. *x* codici per date, time e timestamp; quando si *FieldIdentifier* è uguale a, SQL_COLUMN_TYPE **SQLColAttribute** restituisce ODBC 2. *x* codici per date, time e timestamp.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Mapping di SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Modifiche ai tipi di dati datetime](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
