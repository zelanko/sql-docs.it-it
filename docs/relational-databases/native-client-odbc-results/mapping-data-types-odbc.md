---
title: Tipi di dati di mapping (ODBC) Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [ODBC]
- result sets [ODBC], data types
- ODBC data types, mapping
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], mapping
- sql_variant data type
- SQL Server Native Client ODBC driver, data types
ms.assetid: 4ba0924d-9fca-4c48-aced-0a8d817b3dde
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 92426c854758d07a9d62ec57510d202b870dd9f2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304629"
---
# <a name="mapping-data-types-odbc"></a>Mapping dei tipi di dati (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client esegue il mapping dei tipi di dati SQL ai tipi di dati SQL ODBC. Nelle sezioni seguenti vengono illustrati i tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL e i tipi di dati SQL ODBC con i quali eseguono il mapping. Vengono inoltre illustrati i tipi di dati SQL ODBC e i tipi di dati C ODBC corrispondenti, nonché le conversioni supportate e quelle predefinite.  
  
> [!NOTE]  
>  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo di dati **timestamp** esegue il mapping al tipo di dati ODBC SQL_BINARY o SQL_VARBINARY perché i valori nelle colonne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** non sono valori **datetime,** ma valori **binary(8)** o **varbinary(8)** che indicano la sequenza di attività sulla riga. Se il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client rileva un valore SQL_C_WCHAR (Unicode) che corrisponde a un numero dispari di byte, il byte dispari finale viene troncato.  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>Gestione del tipo di dati sql_variant in ODBC  
 La colonna **sql_variant** tipo di dati può [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenere qualsiasi tipo di dati in oggetti di grandi dimensioni (LOB), ad esempio **text**, **ntext**e **image**. Ad esempio, la colonna potrebbe contenere valori **piccoli** per alcune righe, valori **float** per altre righe e valori **char/nchar** nel resto.  
  
 Il **tipo di** dati sql_variant è simile al tipo di dati Variant in Microsoft Visual Basic.The type are similar to the **Variant** data type in Microsoft Visual Basic®.  
  
### <a name="retrieving-data-from-the-server"></a>Recupero di dati dal server  
 ODBC non dispone di un concetto di tipi variant, limitando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]l'utilizzo del tipo di dati **sql_variant** con un driver ODBC in . Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]viene specificata l'associazione , il **tipo di** dati sql_variant deve essere associato a uno dei tipi di dati ODBC documentati. **SQL_CA_SS_VARIANT_TYPE**, un nuovo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attributo specifico per il driver ODBC Native Client , restituisce all'utente il tipo di dati di un'istanza nella **colonna sql_variant.**  
  
 Se non viene specificata alcuna associazione, è possibile utilizzare la funzione [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) per determinare il tipo di dati di un'istanza nella colonna **sql_variant.**  
  
 Per recuperare **sql_variant** dati, attenersi alla seguente procedura.  
  
1.  Chiamare **SQLFetch** per posizionare la riga recuperata.  
  
2.  Chiamare **SQLGetData**, specificando SQL_C_BINARY per il tipo e 0 per la lunghezza dei dati. In questo modo il driver per leggere l'intestazione **sql_variant.** L'intestazione fornisce il tipo di dati di tale istanza nella colonna **sql_variant.** **SQLGetData** restituisce la dimensione (in byte) del valore.  
  
3.  Chiamare [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) specificando **SQL_CA_SS_VARIANT_TYPE** come valore dell'attributo. Questa funzione restituirà il tipo di dati C dell'istanza nella colonna **sql_variant** al client.  
  
 Di seguito viene riportato un segmento di codice nel quale vengono mostrate le operazioni precedenti.  
  
```  
while ((retcode = SQLFetch (hstmt))==SQL_SUCCESS)  
{  
    if (retcode != SQL_SUCCESS && retcode != SQL_SUCCESS_WITH_INFO)  
    {  
        SQLError (NULL, NULL, hstmt, NULL,   
                    &lNativeError,szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    retcode = SQLGetData (hstmt, 1, SQL_C_BINARY,   
                                pBuff,0,&Indicator);//Figure out the length  
    if (retcode != SQL_SUCCESS_WITH_INFO && retcode != SQL_SUCCESS)  
    {  
        SQLError (NULL, NULL, hstmt, NULL, &lNativeError,   
                    szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    printf_s ("Byte length : %d ",Indicator); //Print out the byte length  
  
    int iValue = 0;  
    retcode = SQLColAttribute (hstmt, 1, SQL_CA_SS_VARIANT_TYPE, NULL,   
                                        NULL,NULL,&iValue);  //Figure out the type  
    printf_s ("Sub type = %d ",iValue);//Print the type, the return is C_type of the column]  
  
// Set up a new binding or do the SQLGetData on that column with   
// the appropriate type  
}  
```  
  
 Se l'utente crea l'associazione utilizzando [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), il driver legge i metadati e i dati. Il driver converte quindi i dati nel tipo ODBC appropriato specificato nell'associazione.  
  
### <a name="sending-data-to-the-server"></a>Invio dei dati al server  
 **SQL_SS_VARIANT**, un nuovo tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di dati specifico per il driver ODBC Native Client, viene utilizzato per i dati inviati a una colonna **sql_variant.** Quando si inviano dati al server utilizzando parametri (ad esempio, INSERT INTO TableName VALUES (?,?)), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) viene utilizzato per specificare le informazioni sul parametro, tra cui il tipo C e il tipo corrispondente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client convertirà il tipo di dati C in uno dei sottotipi **di sql_variant** appropriati.  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborazione dei risultati &#40;&#41;ODBCProcessing Results &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
