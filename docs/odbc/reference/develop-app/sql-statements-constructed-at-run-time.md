---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0573851ee93bda4aa33e8645148cf2ee66200bee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149129"
---
# <a name="sql-statements-constructed-at-run-time"></a>Istruzioni SQL costruite in fase di esecuzione
Le applicazioni che eseguono l'analisi ad hoc comunemente compilare istruzioni SQL in fase di esecuzione. Ad esempio, un foglio di calcolo potrebbe consentire a un utente di selezionare le colonne da cui recuperare i dati:  
  
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
  
 Un'altra classe di applicazioni che in genere crea istruzioni SQL in fase di esecuzione sono ambienti di sviluppo dell'applicazione. Tuttavia, le istruzioni che creano sono impostate come hardcoded nell'applicazione in corso di sviluppo, in cui possono in genere essere ottimizzati e testati.  
  
 Le applicazioni che creare istruzioni SQL in fase di esecuzione possono fornire una notevole flessibilità per l'utente. Come si può notare nell'esempio precedente, che non supporta ancora le operazioni comuni come la **in cui** clausole **ORDER BY** clausole o join, costruzione di istruzioni SQL in fase di esecuzione è notevolmente più complessa rispetto alle istruzioni di impostare come hardcoded. Inoltre, test di tali applicazioni è problematico, perché è possibile costruire un numero arbitrario di istruzioni SQL.  
  
 Un potenziale svantaggio della costruzione di istruzioni SQL in fase di esecuzione è che richiede molto più tempo per costruire un'istruzione di usare un'istruzione a livello di codice. Fortunatamente, questo raramente rappresenta un problema. Tali applicazioni tendono a essere a elevato utilizzo di interfaccia utente e l'ora l'applicazione trascorre la costruzione di istruzioni SQL è generalmente di dimensioni ridotte rispetto all'ora l'utente impiega immettendo i criteri.
