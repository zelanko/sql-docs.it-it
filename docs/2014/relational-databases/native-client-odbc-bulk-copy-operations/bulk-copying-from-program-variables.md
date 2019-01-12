---
title: Copia bulk da variabili di programma | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], program variables
- bcp_bind function
- mapping data types [ODBC]
- SQL Server Native Client ODBC driver, bulk copy
- data types [ODBC], bulk copying
- ODBC, bulk copy operations
- program variables [ODBC]
ms.assetid: e4284a1b-7534-4b34-8488-b8d05ed67b8c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5473d741f5144338c99627e1057c51ce116093d6
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130291"
---
# <a name="bulk-copying-from-program-variables"></a>Copia bulk da variabili di programma
  È possibile eseguire una copia bulk direttamente dalle variabili di programma. Dopo aver allocato le variabili per contenere i dati di una riga e chiamare [bcp_init](../native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) per avviare la copia bulk, chiamare [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) per ogni colonna specificare il percorso e il formato della variabile di programma da associare con la colonna. Completare ogni variabile con i dati, quindi chiamare [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) per inviare una riga di dati al server. Ripetere il processo di compilazione di variabili e la chiamata **bcp_sendrow** fino a quando tutte le righe sono state inviate al server, quindi chiamare [bcp_done](../native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) per specificare che l'operazione è stata completata.  
  
 Il **bcp_bind**_pData_ parametro contiene l'indirizzo della variabile da associare alla colonna. I dati di ogni colonna possono essere archiviati in due modi:  
  
-   Allocando una variabile in modo da contenere i dati.  
  
-   Allocando una variabile indicatore seguita immediatamente dalla variabile dati.  
  
 La variabile indicatore indica la lunghezza dei dati per le colonne a lunghezza variabile e indica inoltre i valori NULL se la colonna ammette valori NULL. Se solo una variabile di dati viene usata, quindi l'indirizzo di questa variabile viene archiviato nel **bcp_bind**_pData_ parametro. Se viene utilizzata una variabile indicatore, l'indirizzo di questa variabile verrà archiviato nel **bcp_bind**_pData_ parametro. Funzioni di copia bulk calcolano il percorso della variabile dati aggiungendo le **bcp_bind**_cbIndicator_ e *pData* parametri.  
  
 **bcp_bind** supporta tre metodi per la gestione di dati a lunghezza variabile:  
  
-   Uso *cbData* con solo una variabile di dati. Inserire la lunghezza dei dati in *cbData*. Ogni volta che la lunghezza dei dati BULK copiato le modifiche, chiamare [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)reimpostare *cbData*. Se viene utilizzato uno degli altri due metodi, specificare SQL_VARLEN_DATA per *cbData*. Se tutti i valori dei dati forniti per una colonna sono NULL, specificare SQL_NULL_DATA per *cbData*.  
  
-   Utilizzare variabili indicatore. Non appena un nuovo valore dei dati viene spostato nella variabile dati, archiviare la lunghezza del valore nella variabile indicatore. Se viene utilizzato uno degli altri due metodi, specificare 0 per *cbIndicator*.  
  
-   Utilizzare i puntatori ai caratteri di terminazione. Carica il **bcp_bind**_pTerm_ parametro con l'indirizzo dello schema di bit che termina i dati. Se viene utilizzato uno degli altri due metodi, specificare NULL per *pTerm*.  
  
 Tutte e tre questi metodi sono utilizzabili in uguale **bcp_bind** chiamare, nel qual caso viene utilizzata la specifica che comporta la quantità minima di dati da copiare.  
  
 Il **bcp_bind**_tipo_ gli identificatori di tipo dati di parametro utilizzi DB-Library, non identificatori di tipo dei dati ODBC. Gli identificatori di tipo di dati DB-Library vengono definiti in SQLNCLI. h per l'uso con ODBC **bcp_bind** (funzione).  
  
 Le funzioni di copia bulk non supportano tutti i tipi di dati C ODBC. Ad esempio, le funzioni di copia bulk non supportano la struttura ODBC SQL_C_TYPE_TIMESTAMP, prestare [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) oppure [SQLGetData](../native-client-odbc-api/sqlgetdata.md) per convertire i dati ODBC SQL_TYPE_TIMESTAMP in una variabile SQL_C_CHAR. Se poi si usa **bcp_bind** con un *tipo* parametro di SQLCHARACTER per associare la variabile a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** colonna, funzioni di copia bulk convertono i clausola di escape di timestamp nella variabile carattere nel formato datetime appropriato.  
  
 Nella tabella seguente vengono elencati i tipi di dati consigliati da utilizzare nel mapping da un tipo di dati SQL ODBC a un tipo di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Tipo di dati SQL ODBC|Tipo di dati C ODBC|bcp_bind *tipo* parametro|Tipo di dati di SQL Server|  
|-----------------------|----------------------|--------------------------------|--------------------------|  
|SQL_CHAR|SQL_C_CHAR|SQLCHARACTER|**character**<br /><br /> **char**|  
|SQL_VARCHAR|SQL_C_CHAR|SQLCHARACTER|**varchar**<br /><br /> **variabili di carattere**<br /><br /> **char varying**<br /><br /> **sysname**|  
|SQL_LONGVARCHAR|SQL_C_CHAR|SQLCHARACTER|**text**|  
|SQL_WCHAR|SQL_C_WCHAR|SQLNCHAR|**nchar**|  
|SQL_WVARCHAR|SQL_C_WCHAR|SQLNVARCHAR|**nvarchar**|  
|SQL_WLONGVARCHAR|SQL_C_WCHAR|SQLNTEXT|**ntext**|  
|SQL_DECIMAL|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **DEC**<br /><br /> **money**<br /><br /> **smallmoney**|  
|SQL_NUMERIC|SQL_C_NUMERIC|SQLNUMERICN|**numeric**|  
|SQL_BIT|SQL_C_BIT|SQLBIT|**bit**|  
|SQL_TINYINT (con segno)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_TINYINT (senza segno)|SQL_C_UTINYINT|SQLINT1|**tinyint**|  
|SQL_SMALL_INT (con segno)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_SMALL_INT (senza segno)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER (con segno)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER (senza segno)|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **DEC**|  
|SQL_BIGINT (con segno e senza segno)|SQL_C_CHAR|SQLCHARACTER|**bigint**|  
|SQL_REAL|SQL_C_FLOAT|SQLFLT4|**real**|  
|SQL_FLOAT|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_DOUBLE|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_BINARY|SQL_C_BINARY|SQLBINARY|**binary**<br /><br /> **timestamp**|  
|SQL_VARBINARY|SQL_C_BINARY|SQLBINARY|**varbinary**<br /><br /> **Binary varying**|  
|SQL_LONGVARBINARY|SQL_C_BINARY|SQLBINARY|**image**|  
|SQL_TYPE_DATE|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIME|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIMESTAMP|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_GUID|SQL_C_GUID|SQLUNIQUEID|**uniqueidentifier**|  
|SQL_INTERVAL_|SQL_C_CHAR|SQLCHARACTER|**char**|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sono firmati **tinyint**senza segno **smallint**, o senza segno **int** i tipi di dati. Per evitare la perdita di valori dei dati quando si esegue la migrazione di questi tipi di dati, creare la tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con il tipo di dati integer successivo più grande. Per impedire agli utenti di aggiungere in un secondo momento valori non compresi nell'intervallo consentito dal tipo di dati originale, applicare una regola alla colonna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per limitare i valori consentiti all'intervallo supportato dal tipo di dati originale:  
  
```  
CREATE TABLE Sample_Ints(STinyIntCol   SMALLINT,  
USmallIntCol INT)  
GO  
CREATE RULE STinyInt_Rule  
AS   
@range >= -128 AND @range <= 127  
GO  
CREATE RULE USmallInt_Rule  
AS   
@range >= 0 AND @range <= 65535  
GO  
sp_bindrule STinyInt_Rule, 'Sample_Ints.STinyIntCol'  
GO  
sp_bindrule USmallInt_Rule, 'Sample_Ints.USmallIntCol'  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta direttamente i tipi di dati intervallo. Tuttavia, un'applicazione può archiviare le sequenze di escape dell'intervallo come stringhe di caratteri in una colonna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di tipo carattere. Tali valori potranno essere letti dall'applicazione per un utilizzo futuro ma non potranno essere utilizzati nelle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 Le funzioni di copia bulk possono essere utilizzate per caricare rapidamente i dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] letti da un'origine dati ODBC. Usare [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) per associare le colonne del set di risultati a variabili di programma, quindi usare **bcp_bind** per associare le stesse variabili di programma a un'operazione di copia bulk. La chiamata [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md) oppure **SQLFetch** viene quindi recuperata una riga di dati dall'origine dati ODBC nelle variabili di programma e chiamare il metodo [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) copia bulk dei dati dalle variabili di programma a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Un'applicazione può usare la [bcp_colptr](../native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md) funzionare ogni volta che è necessario modificare l'indirizzo della variabile dati specificata originariamente nel **bcp_bind** _pData_ parametro. Un'applicazione può usare il [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) funzionare ogni volta che è necessario modificare la lunghezza dei dati specificata in origine la **bcp_bind**_cbData_ parametro.  
  
 Non è possibile leggere i dati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nelle variabili di programma utilizzando la copia bulk. Non esiste una funzione simile a "bcp_readrow". È possibile solo inviare i dati dall'applicazione al server.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di operazioni di copia Bulk &#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  
