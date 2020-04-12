---
title: Recuperare i dati numerici con SQL_NUMERIC_STRUCT Documenti Microsoft
description: L'utilizzo di C/Cè tramite ODBC consente di recuperare il tipo di dati numerico di SQL Server utilizzando SQL_NUMERIC_STRUCT, correlati a i SQL_C_NUMERIC.
editor: ''
ms.prod: sql
ms.technology: connectivity
ms.devlang: cpp
ms.topic: conceptual
ms.custom: ''
ms.date: 07/14/2017
ms.author: genemi
author: MightyPen
ms.openlocfilehash: ec2b68b918cbc79a245fe639108e94165be729c8
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219100"
---
# <a name="retrieve-numeric-data-with-sql_numeric_struct"></a>Recuperare dati numerici con SQL\_NUMERIC\_STRUCT

In questo articolo viene descritto come recuperare dati numerici dal driver ODBC di SQL Server in una struttura numerica. Viene inoltre descritto come ottenere i valori corretti utilizzando valori di precisione e scala specifici.

Questo tipo di dati consente alle applicazioni di gestire direttamente i dati numerici. Intorno all'anno 2003, ODBC 3.0 ha introdotto un nuovo tipo di dati ODBC C, identificato da **SQL\_C\_NUMERIC**. Questo tipo di dati è ancora rilevante a partire dal 2017.

Il buffer C utilizzato ha la definizione di tipo **SQL\_NUMERIC\_STRUCT**. Questa struttura include campi per l'archiviazione della precisione, della scala, del segno e del valore dei dati numerici. Il valore stesso viene archiviato come intero scalato con il byte meno significativo che inizia nella posizione più a sinistra. 

L'articolo [Tipi di](c-data-types.md) dati C fornisce ulteriori\_\_informazioni sul formato e sull'utilizzo di SQL NUMERIC STRUCT. In genere [l'Appendice D](appendix-d-data-types.md) di ODBC 3.0 Programmer's Reference illustra i tipi di dati.


## <a name="sql_numeric_struct-overview"></a>Panoramica di SQL\_NUMERIC\_STRUCT


Lo\_STRUCT\_NUMERICo SQL viene definito nel file di intestazione sqltypes.h come segue:


```c
#define SQL_MAX_NUMERIC_LEN    16
typedef struct tagSQL_NUMERIC_STRUCT
{
   SQLCHAR    precision;
   SQLSCHAR   scale;
   SQLCHAR    sign;   /* 1 if positive, 0 if negative */
   SQLCHAR    val[SQL_MAX_NUMERIC_LEN];
} SQL_NUMERIC_STRUCT;
```

            
I campi di precisione e scala della struttura numerica non vengono mai utilizzati per l'input da un'applicazione, solo per l'output dal driver all'applicazione.

Il driver utilizza la precisione predefinita (definito dal driver) e la scala predefinita (0) ogni volta che si restituiscono dati all'applicazione. A meno che l'applicazione non specifichi i valori per la precisione e la scala, il driver assume il valore predefinito e tronca la parte decimale dei dati numerici.

## <a name="sql_numeric_struct-code-sample"></a>Esempio\_\_di codice SQL NUMERIC STRUCT

Questo esempio di codice mostra come:This code sample shows you how to:

- Impostare la precisione.
- Impostare la scala.
- Recuperare i valori corretti. 

> [!Note]
> QUALSIASI UTILIZZO DA PARTE DELL'UTENTE DEL CODICE FORNITO IN QUESTO ARTICOLO È A PROPRIO RISCHIO E PERICOLO. 
>
> Microsoft fornisce questi esempi di codice "così com'è" senza garanzia di alcun tipo, espressa o implicita, inclusa, a non solo, le garanzie implicite di merchantability e/o idoneità per uno scopo particolare.

```c
#include <stdio.h>
#include <string.h>
#include <conio.h>
#include <stdlib.h>
#include <ctype.h>
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

#define MAXDSN       25
#define MAXUID       25
#define MAXAUTHSTR   25
#define MAXBUFLEN   255

SQLHENV     henv   = SQL_NULL_HENV;
SQLHDBC     hdbc1  = SQL_NULL_HDBC;     
SQLHSTMT    hstmt1 = SQL_NULL_HSTMT;
SQLHDESC    hdesc  = NULL;


SQL_NUMERIC_STRUCT NumStr;

int main()
{
   RETCODE retcode;

//Change the values below as appropriate to make a successful connection.
//szDSN: DataSourceName, szUID=userid, szAuthStr: password

UCHAR szDSN[MAXDSN+1] = "sql33",szUID[MAXUID+1]="sa", szAuthStr[MAXAUTHSTR+1] = "";
SQLINTEGER strlen1;
SQLINTEGER a;
int i,sign =1;
long myvalue, divisor;
float final_val;
   
// Allocate the Environment handle. Set the Env attribute, allocate the
//connection handle, connect to the database and allocate the statement //handle.

retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);
retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION,(SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);
retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);
retcode = SQLConnect(hdbc1, szDSN,SQL_NTS,szUID,SQL_NTS,szAuthStr,SQL_NTS);
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);

// Execute the select statement. Here it is assumed that numeric_test
//table is created using the following statements:

// Create table numeric_test (col1 numeric(5,3))
//insert into numeric_test values (25.212)

retcode = SQLExecDirect(hstmt1,(UCHAR *)"select * from numeric_test",SQL_NTS);

// Use SQLBindCol to bind the NumStr to the column that is being retrieved.

retcode = SQLBindCol(hstmt1,1,SQL_C_NUMERIC,&NumStr,19,&strlen1);

// Get the application row descriptor for the statement handle using
//SQLGetStmtAttr.

retcode = SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_ROW_DESC,&hdesc, 0, NULL);

// You can either use SQLSetDescRec or SQLSetDescField when using
// SQLBindCol. However, if you prefer to call SQLGetData, you have to
// call SQLSetDescField instead of SQLSetDescRec. For more information on
// descriptors, please refer to the ODBC 3.0 Programmers reference or
// your Online documentation.

//Used when using SQLSetDescRec
//a=b=sizeof(NumStr);

// Set the datatype, precision and scale fields of the descriptor for the 
//numeric column. Otherwise the default precision (driver defined) and 
//scale (0) are returned.

// In this case, the table contains only one column, hence the second 
//parameter contains one. Zero applies to bookmark columns. Please check 
//the programmers guide for more information.

//retcode=SQLSetDescRec(hdesc,1,SQL_NUMERIC,NULL,sizeof(NumStr),5,3,&NumStr,&a,&b);

retcode = SQLSetDescField (hdesc,1,SQL_DESC_TYPE,(VOID*)SQL_C_NUMERIC,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_PRECISION,(VOID*) 5,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_SCALE,(VOID*) 3,0);
    
// Initialize the val array in the numeric structure.

memset(NumStr.val,0,16);
   
// Call SQLFetch to fetch the first record.

while((retcode =SQLFetch(hstmt1)) != SQL_NO_DATA)
  {
// Notice that the TargetType (3rd Parameter) is SQL_ARD_TYPE, which  
//forces the driver to use the Application Row Descriptor with the 
//specified scale and precision.

   retcode = SQLGetData(hstmt1, 1, SQL_ARD_TYPE, &NumStr, 19, &a); 

// Check for null indicator.

   if ( SQL_NULL_DATA == a )
   {
   printf( "The final value: NULL\n" );
   continue;
   }

// Call to convert the little endian mode data into numeric data.

   myvalue = strtohextoval();

// The returned value in the above code is scaled to the value specified
//in the scale field of the numeric structure. For example 25.212 would
//be returned as 25212. The scale in this case is 3 hence the integer 
//value needs to be divided by 1000.

   divisor = 1;
   if(NumStr.scale > 0)
     {
    for (i=0;i< NumStr.scale; i++)   
         divisor = divisor * 10;
     }
   final_val =  (float) myvalue /(float) divisor;

// Examine the sign value returned in the sign field for the numeric
//structure.
//NOTE: The ODBC 3.0 spec required drivers to return the sign as 
//1 for positive numbers and 2 for negative number. This was changed in the
//ODBC 3.5 spec to return 0 for negative instead of 2.

      if(!NumStr.sign) sign = -1;
      else sign  =1;

   final_val *= sign;
   printf("The final value: %f\n",final_val);
    }

   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA_FOUND);

   /* clean up */ 
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);
   SQLDisconnect(hdbc1);
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
   return(0);
}
```


### <a name="interim-results"></a>Risultati intermedi:


```console
//  C  ==> 12 * 1    =     12
//  7  ==> 07 * 16   =    112
//  2  ==> 02 * 256  =    512
//  6  ==> 06 * 4096 =  24576
===============================
                 Sum =  25212
```


Nella struttura numerica, il campo val è una matrice di caratteri di 16 elementi. Ad esempio, 25.212 viene scalato a 25212 e la scala è 3.For example, 25.212 is scalad to 25212 and the scale is 3. In formato esadecimale questo numero sarebbe 627C.

Il driver restituisce i seguenti elementi:

- Il carattere equivalente di 7C, che è ' (pipe) nel primo elemento della matrice di caratteri.
- L'equivalente di 62, che è 'b' nel secondo elemento.
- Il resto degli elementi della matrice contiene zeri, pertanto il buffer contiene ''b'0''.

Ora la sfida consiste nel costruire l'intero scalato da questa matrice di stringhe. Ogni carattere nella stringa corrisponde a due cifre esadecimali, ad esempio la cifra meno significativa (LSD) e la cifra più significativa (MSD). Il valore intero scalato può essere generato moltiplicando ogni cifra (LSD & MSD) con un multiplo di 16, a partire da 1.

Codice che implementa la conversione dalla modalità little endian all'intero ridimensionato. Spetta allo sviluppatore dell'applicazione implementare questa funzionalità. L'esempio di codice seguente è solo uno dei molti modi possibili.


```c
long strtohextoval()
{
    long val=0,value=0;
    int i=1,last=1,current;
    int a=0,b=0;

        for(i=0;i<=15;i++)
        {
         current = (int) NumStr.val[i];
         a= current % 16; //Obtain LSD
         b= current / 16; //Obtain MSD
            
         value += last* a;   
         last = last * 16;   
         value += last* b;
         last = last * 16;   
        }
     return value;
}
```


### <a name="applies-to-versions"></a>Si applica alle versioni


Le informazioni precedenti\_su\_SQL NUMERIC STRUCT si applicano alle seguenti versioni del prodotto:

- Driver Microsoft ODBC per Microsoft SQL Server 3.7
- Componenti di Microsoft Data Access 2.1
- Componenti di Microsoft Data Access 2.5
- Componenti di Microsoft Data Access 2.6
- Componenti di Microsoft Data Access 2.7


## <a name="sql_c_numeric-overview"></a>Panoramica di SQL\_C\_NUMERIC


Nel programma di esempio seguente\_viene\_illustrato l'utilizzo di SQL C NUMERIC, inserendo 123.45 in una tabella. Nella tabella, la colonna è definita come numerico o decimale, con precisione 5 e con scala 2.

Il driver ODBC utilizzato per eseguire questo programma deve supportare la funzionalità ODBC 3.0.


```c
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

void main() {

   SQLHENV    henv  = NULL;
   SQLHDBC    hdbc  = NULL;
   SQLHSTMT   hstmt = NULL;

   SQL_NUMERIC_STRUCT   NumStr;
   SQLINTEGER           cbNumStr = sizeof (NumStr);

   SQLAllocHandle(SQL_HANDLE_ENV, NULL, &henv);

   /* Set the ODBC behavior version. */ 
   SQLSetEnvAttr(henv,
         SQL_ATTR_ODBC_VERSION,
         (SQLPOINTER) SQL_OV_ODBC3,
         SQL_IS_INTEGER);

   SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);

   /* Substitute your own connection information */ 
   SQLConnect(hdbc,
      (SQLCHAR *) "MyDSN", 5,
      (SQLCHAR *) "UserID", 6,
      (SQLCHAR *) "Password", 8);

   SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);

   /*
      Set up the SQL_NUMERIC_STRUCT, NumStr, to hold "123.45".

      First, we need to scale 123.45 to an integer: 12345
      One way to switch the bytes is to convert 12345 to Hex:  0x3039
      Since the least significant byte will be stored starting from the
      leftmost byte, "0x3039" will be stored as "0x3930".

      The precision and scale fields are not used for input to the driver,
      only for output from the driver. The precision and scale will be set
      in the application parameter descriptor later.
   */ 

   NumStr.sign = 1;   /* 1 if positive, 2 if negative */ 

   memset (NumStr.val, 0, 16);
   NumStr.val [0] = 0x39;
   NumStr.val [1] = 0x30;

   /* SQLBindParameter needs to be called before SQLSetDescField */ 
   SQLBindParameter(hstmt,
          1,
          SQL_PARAM_INPUT,
          SQL_C_NUMERIC,
          SQL_NUMERIC,
          5,
          2,
          &NumStr,
          0,
          (SQLINTEGER *) &cbNumStr);

   /* Modify the fields in the implicit application parameter descriptor */ 
   SQLHDESC   hdesc = NULL;

   SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);
   SQLSetDescField(hdesc, 1, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_PRECISION, (SQLPOINTER) 5, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_SCALE, (SQLPOINTER) 2, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_DATA_PTR, (SQLPOINTER) &NumStr, 0);

   SQLExecDirect(hstmt,
         (SQLCHAR *) "INSERT INTO table (numeric_column) VALUES (?)",
         SQL_NTS);

   SQLFreeHandle(SQL_HANDLE_STMT, hstmt);

   SQLDisconnect (hdbc);

   SQLFreeHandle(SQL_HANDLE_DBC, hdbc);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
}
```


<!--
GeneMi historical notes, 2017/July/12. Per Jason.C

https://go.microsoft.com/fwlink/?LinkId=147596

https://support.microsoft.com/help/222831

https://web.archive.org/web/20140319133434/http:/support.microsoft.com:80/kb/222831

https://web.archive.org/web/20080505073901/http:/support.microsoft.com:80/kb/181254

https://docs.microsoft.com/sql/odbc/reference/appendixes/c-data-types
-->

