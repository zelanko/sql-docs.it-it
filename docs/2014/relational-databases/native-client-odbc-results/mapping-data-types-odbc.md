---
title: Mapping dei tipi di dati (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcca4bc6161526d1bd78e55bc9452f2d7d9d69d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200012"
---
# <a name="mapping-data-types-odbc"></a>Mapping dei tipi di dati (ODBC)
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue il mapping del driver ODBC di Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati SQL ai tipi di dati SQL ODBC. Nelle sezioni seguenti vengono illustrati i tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL e i tipi di dati SQL ODBC con i quali eseguono il mapping. Vengono inoltre illustrati i tipi di dati SQL ODBC e i tipi di dati C ODBC corrispondenti, nonché le conversioni supportate e quelle predefinite.  
  
> [!NOTE]  
>  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** tipo di dati corrisponde al tipo di dati SQL_BINARY o SQL_VARBINARY ODBC perché i valori nelle **timestamp** colonne non sono **datetime** valori, ma **binari (8)** oppure **varbinary (8)** valori che indicano la sequenza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attività sulla riga. Se il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client rileva un valore SQL_C_WCHAR (Unicode) che corrisponde a un numero dispari di byte, il byte dispari finale viene troncato.  
  
## <a name="dealing-with-sqlvariant-data-type-in-odbc"></a>Gestione del tipo di dati sql_variant in ODBC  
 Il **sql_variant** può contenere uno dei tipi di dati nella colonna tipo di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ad eccezione di oggetti di grandi dimensioni (LOB), ad esempio **testo**, **ntext**, e  **immagine**. Ad esempio, la colonna può contenere **smallint** i valori per alcune righe **float** valori per le altre righe, e **char/nchar** valori nella parte restante.  
  
 Il **sql_variant** tipo di dati è simile al **Variant** il tipo di dati in Microsoft Visual Basic??.  
  
### <a name="retrieving-data-from-the-server"></a>Recupero di dati dal server  
 ODBC non è un concetto dei tipi variant, limitando l'uso del **sql_variant** tipo di dati con un driver ODBC in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se viene specificata l'associazione, il **sql_variant** tipo di dati deve essere associato a uno dei tipi di dati ODBC documentati. **SQL_CA_SS_VARIANT_TYPE**, un nuovo attributo specifico per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client, restituisce il tipo di dati di un'istanza nel **sql_variant** colonna all'utente.  
  
 Se viene specificata alcuna associazione, il [SQLGetData](../native-client-odbc-api/sqlgetdata.md) funzione può essere utilizzata per determinare il tipo di dati di un'istanza nel **sql_variant** colonna.  
  
 Per recuperare **sql_variant** dati seguono questa procedura.  
  
1.  Chiamare **SQLFetch** per posizionarsi sulla riga recuperata.  
  
2.  Chiamare **SQLGetData**, specificando SQL_C_BINARY per il tipo e 0 per la lunghezza dei dati. In tal modo il driver di leggere il **sql_variant** intestazione. L'intestazione fornisce il tipo di dati di tale istanza nel **sql_variant** colonna. **SQLGetData** restituisce le dimensioni (in byte) del valore.  
  
3.  Chiamare [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md) specificando **SQL_CA_SS_VARIANT_TYPE** come valore di attributo. Questa funzione restituirà il tipo di dati C dell'istanza di **sql_variant** colonna al client.  
  
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
  
 Se l'utente crea l'associazione utilizzando [SQLBindCol](../native-client-odbc-api/sqlbindcol.md), il driver legge i metadati e i dati. Il driver converte quindi i dati nel tipo ODBC appropriato specificato nell'associazione.  
  
### <a name="sending-data-to-the-server"></a>Invio dei dati al server  
 **SQL_SS_VARIANT**, un nuovo tipo di dati specifici per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client, viene usato per i dati inviati a un **sql_variant** colonna. Quando si inviano dati al server utilizzando i parametri (ad esempio, INSERT INTO TableName VALUES (?,?)), [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) viene usato per specificare le informazioni sui parametri, incluso il tipo C e i corrispondenti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client convertirà il tipo di dati C in uno degli appropriati **sql_variant** sottotipi.  
  
## <a name="see-also"></a>Vedere anche  
 [L'elaborazione dei risultati &#40;ODBC&#41;](processing-results-odbc.md)  
  
  
