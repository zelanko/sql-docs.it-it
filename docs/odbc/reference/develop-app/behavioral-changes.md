---
title: Modifiche comportamentali | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103870"
---
# <a name="behavioral-changes"></a>Modifiche del comportamento
Le modifiche comportamentali sono le modifiche per le quali la *sintassi* dell'interfaccia resta invariata, ma la *semantica* è stata modificata. Per queste modifiche, funzionalità utilizzate in ODBC 2. *x* si comporta in modo diverso rispetto alla stessa funzionalità di ODBC 3. *x*.  
  
 Indica se un'applicazione presenta ODBC 2. comportamento *x* o ODBC 3. il comportamento *x* è determinato dall'attributo SQL_ATTR_ODBC_VERSION Environment. Questo valore a 32 bit è impostato su SQL_OV_ODBC2 per presentare ODBC 2. comportamento *x* e SQL_OV_ODBC3 per presentare ODBC 3. comportamento *x* .  
  
 L'attributo di ambiente SQL_ATTR_ODBC_VERSION viene impostato da una chiamata a **SQLSetEnvAttr**. Quando un'applicazione chiama **SQLAllocHandle** per allocare un handle di ambiente, deve chiamare immediatamente**SQLSetEnvAttr** per impostare il comportamento che espone. Di conseguenza, è disponibile un nuovo stato dell'ambiente per descrivere l'handle di ambiente in uno stato allocato, ma senza versioni,. Per ulteriori informazioni, vedere [Appendice B: tabelle di transizione dello stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Un'applicazione indica il comportamento che presenta con l'attributo di ambiente SQL_ATTR_ODBC_VERSION, ma l'attributo non ha alcun effetto sulla connessione dell'applicazione con ODBC 2. *x* o ODBC 3. driver *x* . ODBC 3. l'applicazione *x* può connettersi a un ODBC 2. *x* o 3. driver *x* , indipendentemente dall'impostazione dell'attributo Environment.  
  
 ODBC 3. le applicazioni *x* non devono mai chiamare **SQLAllocEnv**. Di conseguenza, se Gestione driver riceve una chiamata a **SQLAllocEnv**, l'applicazione viene riconosciuta come ODBC 2. applicazione *x* .  
  
 L'attributo SQL_ATTR_ODBC_VERSION influiscono su tre aspetti diversi di ODBC 3. comportamento del driver *x* :  
  
-   SQLSTATE  
  
-   Tipi di dati per data, ora e timestamp  
  
-   L'argomento *CatalogName* in **SQLTables** accetta i criteri di ricerca in ODBC 3. *x*, ma non in ODBC 2. *x*  
  
 L'impostazione dell'attributo SQL_ATTR_ODBC_VERSION Environment non influisce su **SQLSetParam** o **SQLBindParam**. Anche **SQLColAttribute** non è influenzato da questo bit. Sebbene **SQLColAttribute** restituisca attributi interessati dalla versione di ODBC (tipo di data, precisione, scala e lunghezza), il comportamento previsto è determinato dal valore dell'argomento *FieldIdentifier* . Quando *FieldIdentifier* è uguale a SQL_DESC_TYPE, **SQLColAttribute** restituisce ODBC 3. codici *x* per data, ora e timestamp; Quando *FieldIdentifier* è uguale a SQL_COLUMN_TYPE, **SQLColAttribute** restituisce ODBC 2. codici *x* per data, ora e timestamp.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Mapping di SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Modifiche ai tipi di dati datetime](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
