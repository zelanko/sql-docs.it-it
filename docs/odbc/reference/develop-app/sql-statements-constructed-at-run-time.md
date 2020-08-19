---
description: Istruzioni SQL costruite in fase di esecuzione
title: Istruzioni SQL costruite in fase di esecuzione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fff9f7a4e579ce4e1d1177b8f5fa67f7d13a4fdc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424553"
---
# <a name="sql-statements-constructed-at-run-time"></a>Istruzioni SQL costruite in fase di esecuzione
Le applicazioni che eseguono l'analisi ad hoc compilano comunemente istruzioni SQL in fase di esecuzione. Un foglio di calcolo, ad esempio, può consentire a un utente di selezionare le colonne da cui recuperare i dati:  
  
```  
// SQL_Statements_Constructed_at_Run_Time.cpp  
#include <windows.h>  
#include <stdio.h>  
#include <sqltypes.h>  
  
int main() {  
   SQLCHAR *Statement = 0, *TableName = 0;  
   SQLCHAR **TableNamesArray, **ColumnNamesArray = 0;  
   BOOL *ColumnSelectedArray = 0;  
   BOOL  CommaNeeded;  
   SQLSMALLINT i = 0, NumColumns = 0;  
  
   // Use SQLTables to build a list of tables (TableNamesArray[]). Let the  
   // user select a table and store the selected table in TableName.  
  
   // Use SQLColumns to build a list of the columns in the selected table  
   // (ColumnNamesArray). Set NumColumns to the number of columns in the  
   // table. Let the user select one or more columns and flag these columns  
   // in ColumnSelectedArray[].  
  
   // Build a SELECT statement from the selected columns.  
   CommaNeeded = FALSE;  
   Statement = (SQLCHAR*)malloc(8);  
   strcpy_s((char*)Statement, 8, "SELECT ");  
  
   for (i = 0 ; i = NumColumns ; i++) {  
      if (ColumnSelectedArray[i]) {  
         if (CommaNeeded)  
            strcat_s((char*)Statement, sizeof(Statement), ",");  
         else  
            CommaNeeded = TRUE;  
         strcat_s((char*)Statement, sizeof(Statement), (char*)ColumnNamesArray[i]);  
      }  
   }  
  
   strcat_s((char*)Statement, 15, " FROM ");  
   // strcat_s((char*)Statement, 100, (char*)TableName);  
  
   // Execute the statement . It will be executed once, do not prepare it.  
   // SQLExecDirect(hstmt, Statement, SQL_NTS);  
}  
```  
  
 Un'altra classe di applicazioni che in genere costruisce istruzioni SQL in fase di esecuzione sono gli ambienti di sviluppo dell'applicazione. Tuttavia, le istruzioni che costruiscono sono hardcoded nell'applicazione in cui sono compilate, dove possono essere in genere ottimizzate e testate.  
  
 Le applicazioni che costruiscono istruzioni SQL in fase di esecuzione possono offrire un'enorme flessibilità all'utente. Come si può notare dall'esempio precedente, che non supportava anche operazioni comuni come clausole **where** , clausole **Order by** o join, la costruzione di istruzioni SQL in fase di esecuzione è molto più complessa rispetto alle istruzioni di codifica hardcoded. Inoltre, il test di tali applicazioni è problematico perché può costruire un numero arbitrario di istruzioni SQL.  
  
 Un potenziale svantaggio della creazione di istruzioni SQL in fase di esecuzione è il fatto che richiede molto più tempo per costruire un'istruzione rispetto all'uso di un'istruzione hardcoded. Fortunatamente, questo è raramente un problema. Tali applicazioni tendono a essere a elevato utilizzo di interfaccia utente e il tempo impiegato dall'applicazione per la costruzione di istruzioni SQL è generalmente ridotto rispetto al tempo impiegato dall'utente per l'immissione dei criteri.
