---
title: Proprietà SQLGetDescField . Documenti Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetDescField function
ms.assetid: 3e59a37a-28ee-4c91-8968-7fe3b966739d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 341a9fe5c5919093853b0c62c7148515380a0551
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299579"
---
# <a name="sqlgetdescfield"></a>SQLGetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client espone i campi descrittore specifici del driver per il descrittore di riga di implementazione (IRD) solo. All'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] IRD, i campi descrittore sono referenziati tramite gli attributi di colonna specifici del driver. Per informazioni su un elenco completo dei campi descrittori specifici del driver disponibili, vedere [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md).  
  
 I campi di descrizione che contengono stringhe dell'identificatore di colonna sono spesso stringhe di lunghezza zero. Tutti i valori dei campi di descrizione specifici di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono di sola lettura.  
  
 Analogamente agli attributi recuperati con SQLColAttribute, i campi del descrittore che segnalano gli attributi a livello di riga (ad esempio SQL_CA_SS_COMPUTE_ID) vengono segnalati per tutte le colonne nel set di risultati.  
  
## <a name="sqlgetdescfield-and-table-valued-parameters"></a>SQLGetDescField e parametri con valori di tabella  
 SQLGetDescField può essere utilizzato per ottenere valori per gli attributi estesi dei parametri con valori di tabella e delle colonne di parametri con valori di tabella. Per ulteriori informazioni sui parametri con valori di tabella, vedere Parametri con valori di [tabella &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgetdescfield-support-for-enhanced-date-and-time-features"></a>Supporto di SQLGetDescField per le caratteristiche avanzate di data e ora  
 Per informazioni sui campi descrittore disponibili con i nuovi tipi di data/ora, vedere [Metadati dei](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)parametri e dei risultati .  
  
 Per ulteriori informazioni, vedere [Miglioramenti di data e ora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
 A [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]partire da , SQLGetDescField può restituire **SQL_C_SS_TIME2** (per i tipi **di ora)** o **SQL_C_SS_TIMESTAMPOFFSET** (per **datetimeoffset**) anziché **SQL_C_BINARY**, se l'applicazione utilizza ODBC 3.8.  
  
## <a name="sqlgetdescfield-support-for-large-clr-udts"></a>Supporto di SQLGetDescField per tipi definiti dall'utente CLR di grandi dimensioni  
 **SQLGetDescField** supporta tipi CLR definiti dall'utente di grandi dimensioni.SQLGetDescField supports large CLR user-defined types (UDTs). Per ulteriori informazioni, vedere [Tipi CLR di grandi dimensioni definiti dall'utente &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlgetdescfield-support-for-sparse-columns"></a>Supporto di SQLGetDescField per colonne di tipo sparse  
 SQLGetDescField può essere utilizzato per eseguire una query sul nuovo campo IRD SQL_CA_SS_IS_COLUMN_SET per determinare se una colonna è una **colonna column_set.**  
  
 Per ulteriori informazioni, vedere [Supporto delle colonne di tipo sparse &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="example"></a>Esempio  
  
```  
typedef struct tagCOMPUTEBYLIST  
    {  
    SQLSMALLINT nBys;  
    SQLSMALLINT aByList[1];  
    } COMPUTEBYLIST;  
typedef COMPUTEBYLIST* PCOMPUTEBYLIST;   
  
SQLHDESC    hIRD;   
SQLINTEGER  cbIRD;   
SQLINTEGER  nSet = 0;   
  
// . . .  
// Execute a statement that contains a COMPUTE clause,  
//  then get the descriptor handle of the IRD and  
//  get some IRD values.  
  
SQLGetStmtAttr(g_hStmt, SQL_ATTR_IMP_ROW_DESC,  
    (SQLPOINTER) &hIRD, sizeof(SQLHDESC), &cbIRD);  
  
// For statement-wide column attributes, any  
//  descriptor record will do. You know that 1 exists,  
//  so use it.  
SQLGetDescField(hIRD, 1, SQL_CA_SS_NUM_COMPUTES,  
    (SQLPOINTER) &nComputes, SQL_IS_INTEGER, &cbIRD);  
  
if (nSet == 0)  
    {  
    SQLINTEGER      nOrderID;  
  
    printf_s("Normal result set.\n");  
  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        SQLGetDescField(hIRD, nCol+1,  
            SQL_CA_SS_COLUMN_ORDER,  
            (SQLPOINTER) &nOrderID, SQL_IS_INTEGER,  
            &cbIRD);  
  
        if (nOrderID != 0)  
            {  
            printf_s("Col in ORDER BY, pos: %ld",  
                nOrderID);  
            }  
            printf_s("\n");  
        }  
  
    printf_s("\n");  
    }  
else  
    {  
    PCOMPUTEBYLIST  pByList;  
    SQLSMALLINT     nBy;  
    SQLINTEGER      nColID;  
  
    printf_s("Computed result set number: %lu\n",  
        nSet);  
  
    SQLGetDescField(hIRD, 1, SQL_CA_SS_COMPUTE_BYLIST,  
        (SQLPOINTER) &pByList, SQL_IS_INTEGER,  
        &cbIRD);  
  
    if (pByList != NULL)  
        {  
        printf_s("Clause ordered by columns: ");  
        for (nBy = 0; nBy < pByList->nBys; )  
            {  
            printf_s("%u", pByList->aByList[nBy]);  
            nBy++;  
  
            if (nBy == pByList->nBys)  
                {  
                printf_s("\n");  
                }  
            else  
                {  
                printf_s(", ");  
                }  
            }  
        }  
    else  
        {  
        printf_s("Compute clause set not ordered.\n");  
        }  
  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        SQLGetDescField(hIRD, nCol+1,  
            SQL_CA_SS_COLUMN_ID, (SQLPOINTER) &nColID,  
            SQL_IS_INTEGER, &cbIRD);  
        printf_s("ColumnID: %lu, nColID);  
        }  
    printf_s("\n");  
    }  
  
if (SQLMoreResults(g_hStmt) == SQL_SUCCESS)  
    {  
    // Determine the result set indicator.  
    SQLGetDescField(hIRD, 1, SQL_CA_SS_COMPUTE_ID,  
        (SQLPOINTER) &nSet, SQL_IS_INTEGER, &cbIRD);  
    }  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLGetDescFieldSQLGetDescField Function](https://go.microsoft.com/fwlink/?LinkId=59351)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
