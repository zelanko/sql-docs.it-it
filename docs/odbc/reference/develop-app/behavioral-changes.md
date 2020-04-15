---
title: Cambiamenti comportamentali Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e4a433531d90eb0f89d9a5e446464b13fd02526
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283441"
---
# <a name="behavioral-changes"></a>Modifiche del comportamento
Le modifiche comportamentali sono quelle modifiche per le quali la *sintassi* dell'interfaccia rimane invariata, ma la *semantica* è cambiata. Per queste modifiche, funzionalità utilizzata in ODBC 2. *x* si comporta in modo diverso rispetto alla stessa funzionalità di ODBC 3. *x*.  
  
 Se un'applicazione presenta ODBC 2. *x* o ODBC 3. *il* comportamento x è determinato dall'attributo di ambiente SQL_ATTR_ODBC_VERSION. Questo valore a 32 bit è impostato su SQL_OV_ODBC2 per presentare ODBC 2. *x* e SQL_OV_ODBC3 per esibire ODBC 3. *comportamento x.*  
  
 L'attributo di ambiente SQL_ATTR_ODBC_VERSION viene impostato da una chiamata a **SQLSetEnvAttr**. Dopo che un'applicazione chiama **SQLAllocHandle** per allocare un handle di ambiente, è necessario chiamare**SQLSetEnvAttr** immediatamente per impostare il comportamento che presenta. Di conseguenza, esiste un nuovo stato dell'ambiente per descrivere l'handle di ambiente in uno stato allocato, ma senza versione. Per ulteriori informazioni, vedere [Appendice B: tabelle](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)di transizione dello stato ODBC .  
  
 Un'applicazione indica il comportamento che presenta con il SQL_ATTR_ODBC_VERSIONattributo di ambiente, ma l'attributo non ha alcun effetto sulla connessione dell'applicazione con un ODBC 2. *x* o ODBC 3. *driver x.* Un ODBC 3. *x* applicazione può connettersi a un ODBC 2. *x* o 3. *x* driver, indipendentemente dall'impostazione dell'attributo environment.  
  
 ODBC 3. *X* le applicazioni non devono mai chiamare **SQLAllocEnv**. Di conseguenza, se Gestione Driver riceve una chiamata a **SQLAllocEnv**, riconosce l'applicazione come ODBC 2. *applicazione x.*  
  
 L'attributo SQL_ATTR_ODBC_VERSION influisce su tre diversi aspetti di un ODBC 3. comportamento del driver *x:*  
  
-   SQLSTATE  
  
-   Tipi di dati per data, ora e timestamp  
  
-   L'argomento *CatalogName* in **SQLTables** accetta i criteri di ricerca in ODBC 3. *x*, ma non in ODBC 2. *x (in* questo modo  
  
 L'impostazione dell'attributo di ambiente SQL_ATTR_ODBC_VERSION non influisce su **SQLSetParam** o **SQLBindParam**. **SQLColAttribute** non è interessato da questo bit. Anche se **SQLColAttribute** restituisce gli attributi interessati dalla versione di ODBC (tipo di data, precisione, scala e lunghezza), il comportamento previsto è determinato dal valore dell'argomento *FieldIdentifier.* Quando *FieldIdentifier* è uguale a SQL_DESC_TYPE, **SQLColAttribute** restituisce il ODBC 3. *x* codici per data, ora e timestamp; quando *FieldIdentifier* è uguale a SQL_COLUMN_TYPE, **SQLColAttribute** restituisce il ODBC 2. *x* per data, ora e timestamp.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Mapping di SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Modifiche ai tipi di dati datetime](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
