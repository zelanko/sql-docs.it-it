---
title: Istruzioni SQL costruite in fase di esecuzione . Documenti Microsoft
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
ms.openlocfilehash: 795335be2a2a3aab1be6dac26bf6d213161fe42e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301972"
---
# <a name="sql-statements-constructed-at-run-time"></a>Istruzioni SQL costruite in fase di esecuzione
Le applicazioni che eseguono analisi ad hoc in genere compilano istruzioni SQL in fase di esecuzione. Ad esempio, un foglio di calcolo potrebbe consentire all'utente di selezionare le colonne da cui recuperare i dati:  
  
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
  
 Un'altra classe di applicazioni che in genere costruisce istruzioni SQL in fase di esecuzione sono gli ambienti di sviluppo di applicazioni. Tuttavia, le istruzioni che costruiscono sono hardcoded nell'applicazione che stanno compilando, dove in genere possono essere ottimizzate e testate.  
  
 Le applicazioni che costruiscono istruzioni SQL in fase di esecuzione possono fornire un'enorme flessibilità all'utente. Come si può vedere dall'esempio precedente, che non supportava nemmeno operazioni comuni come clausole **WHERE,** clausole **ORDER BY** o join, la costruzione di istruzioni SQL in fase di esecuzione è molto più complessa delle istruzioni hardcoded. Inoltre, il test di tali applicazioni è problematico perché possono costruire un numero arbitrario di istruzioni SQL.  
  
 Un potenziale svantaggio della costruzione di istruzioni SQL in fase di esecuzione è che la costruzione di un'istruzione richiede molto più tempo rispetto all'utilizzo di un'istruzione hardcoded. Fortunatamente, questo è raramente un problema. Tali applicazioni tendono a essere un utilizzo intensivo dell'interfaccia utente e il tempo che l'applicazione trascorre per la costruzione di istruzioni SQL è in genere ridotto rispetto al tempo che l'utente trascorre immettendo criteri.
