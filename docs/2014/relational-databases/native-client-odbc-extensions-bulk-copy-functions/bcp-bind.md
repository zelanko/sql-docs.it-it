---
title: bcp_bind | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_bind
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 711c82bb627ca9ad1620cf1e11fdbc9dfa5f4351
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63140564"
---
# <a name="bcpbind"></a>bcp_bind
  Vengono associati dati provenienti da una variabile di programma a una colonna di tabella per eseguire la copia bulk in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_bind (  
HDBC   
hdbc  
,   
LPCBYTE   
pData  
,  
INT   
cbIndicator  
,  
DBINT   
cbData  
,  
LPCBYTE   
pTerm  
,  
INT   
cbTerm  
,  
INT   
eDataType  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
 *pData*  
 Puntatore ai dati copiati. Se *eDataType* è SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR o SQLIMAGE, *pData* può essere NULL. Un valore NULL *pData* indica che i valori di dati long verranno inviati al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in blocchi mediante [bcp_moretext](bcp-moretext.md). L'utente deve solo impostare *pData* su NULL se la colonna che corrisponde al campo associato dell'utente è una colonna BLOB in caso contrario **bcp_bind** avrà esito negativo.  
  
 Se presenti nei dati, gli indicatori vengono visualizzati in memoria direttamente prima dei dati. Il *pData* parametro fa riferimento alla variabile indicatore in questo caso e la larghezza dell'indicatore, il *cbIndicator* parametro, viene utilizzato correttamente da copia di massa di dati di indirizzo dell'utente.  
  
 *cbIndicator*  
 Lunghezza, espressa in byte, di un indicatore di lunghezza o Null per i dati della colonna. Valori di lunghezza di indicatore validi sono 0 (nel caso in cui non venga utilizzato un indicatore), 1, 2, 4 o 8. Gli indicatori vengono visualizzati in memoria direttamente prima di qualsiasi dato. La definizione del tipo di struttura seguente, ad esempio, potrebbe essere utilizzata per inserire valori integer in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la copia bulk:  
  
```  
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 Nel caso di esempio, il *pData* parametro verrà impostato per l'indirizzo di un'istanza della struttura, l'indirizzo dei BCPBOUNDINT dichiarata *iIndicator* membro della struttura. Il *cbIndicator* parametro verrà impostato per la dimensione di un numero intero (sizeof(int)) e la *cbData* nuovo parametro viene impostato sulla dimensione di un intero (sizeof(int)). Per la copia bulk il valore di una riga nel server che contiene un valore NULL per la colonna associata, il valore dell'istanza *iIndicator* membro deve essere impostato su SQL_NULL_DATA.  
  
 *cbData*  
 Numero di byte dei dati nella variabile di programma che non include la lunghezza di un carattere di terminazione o di un indicatore di lunghezza o Null.  
  
 L'impostazione *cbData* su SQL_NULL_DATA indica che tutte le righe copiate nel server contengono un valore NULL per la colonna.  
  
 L'impostazione *cbData* su SQL_VARLEN_DATA indica che il sistema userà un carattere di terminazione di stringa o altro metodo, per determinare la lunghezza dei dati copiati.  
  
 Per tipi di dati a lunghezza fissa, ad esempio numeri interi, il tipo di dati indica la lunghezza dei dati al sistema. Pertanto, per tipi di dati a lunghezza fissa *cbData* può essere SQL_VARLEN_DATA o la lunghezza dei dati.  
  
 Per la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caratteri e tipi di dati binari *cbData* può essere SQL_VARLEN_DATA, SQL_NULL_DATA, un valore positivo o 0. Se *cbData* è SQL_VARLEN_DATA, il sistema utilizza un indicatore di lunghezza o null (se presente) o una sequenza di caratteri di terminazione per determinare la lunghezza dei dati. Se vengono forniti entrambi, il sistema utilizza quello che comporta la copia del minori numero di dati. Se *cbData* è SQL_VARLEN_DATA, il tipo di dati della colonna è una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carattere o binario e né un indicatore di lunghezza né una sequenza di caratteri di terminazione è specificata, il sistema restituisce un messaggio di errore.  
  
 Se *cbData* è 0 o un valore positivo, il sistema utilizza *cbData* come la lunghezza dei dati. Tuttavia, se, oltre a un numero positivo *cbData* valore, viene fornita una sequenza di lunghezza indicatore o terminazione, il sistema determina la lunghezza dei dati utilizzando il metodo che determina la quantità minima di dati da copiare.  
  
 Il *cbData* il valore del parametro rappresenta il numero di byte di dati. Se i dati di carattere sono rappresentati da caratteri "wide" Unicode, quindi un valore positivo *cbData* il valore del parametro rappresenta il numero di caratteri moltiplicato per la dimensione in byte di ogni carattere.  
  
 *pTerm*  
 Puntatore al modello di byte, se presente, che contrassegna la fine di questa variabile di programma. Le stringhe ANSI e MBCS C, ad esempio, presentano generalmente un carattere di terminazione di 1 byte (\0).  
  
 Se non c'è nessun carattere di terminazione per la variabile, impostare *pTerm* su NULL.  
  
 È possibile utilizzare una stringa vuota ("") per definire il carattere di terminazione Null C come carattere di terminazione della variabile di programma. Poiché la stringa con terminazione null costituisce un singolo byte (il terminatore stesso), impostare *cbTerm* su 1. Ad esempio, per indicare che la stringa in *szName* è con terminazione null e che il carattere di terminazione deve essere utilizzato per indicare la lunghezza:  
  
```  
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```  
  
 Un modulo nonterminated di questo esempio potrebbe indicare che copiare da 15 caratteri il *szName* variabile alla seconda colonna della tabella associata:  
  
```  
bcp_bind(hdbc, szName, 0, 15,   
   NULL, 0, SQLCHARACTER, 2)  
```  
  
 L'API della copia bulk esegue la conversione dei caratteri da Unicode a MBCS in base alle necessità. Verificare che la stringa di byte del carattere di terminazione e la lunghezza della stringa di byte siano impostate correttamente. Ad esempio, per indicare che la stringa nel *szName* è una stringa di caratteri wide Unicode terminata per il valore di carattere di terminazione null di Unicode:  
  
```  
bcp_bind(hdbc, szName, 0,   
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 Se il limite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la colonna è a caratteri "wide", in cui viene eseguita alcuna conversione [bcp_sendrow](bcp-sendrow.md). Se la colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un tipo di carattere MBCS, la conversione da carattere wide a carattere multibyte viene eseguita quando i dati vengono inviati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *cbTerm*  
 Numero dei byte presenti nel carattere di terminazione per la variabile di programma, se presente. Se non è presente alcun carattere di terminazione per la variabile, impostare *cbTerm* su 0.  
  
 *eDataType*  
 Tipo di dati C della variabile di programma. I dati della variabile di programma vengono convertiti nel tipo della colonna di database. Se questo parametro è 0, non viene eseguita alcuna conversione.  
  
 Il *eDataType* parametro viene enumerato in base il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] token dei tipi di dati in SQLNCLI. h, i non enumeratori dei tipi di dati C ODBC. È ad esempio possibile specificare un numero intero a due byte, SQL_C_SHORT di tipo ODBC, utilizzando il tipo specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLINT2.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ha introdotto il supporto per i token tipo dati SQLXML e SQLUDT nel *`eDataType`* parametro.  
  
 *idxServerCol*  
 Posizione ordinale della colonna nella tabella di database in cui vengono copiati i dati. La prima colonna di una tabella è la colonna 1. La posizione ordinale di una colonna viene indicata da [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Note  
 Uso **bcp_bind** di un modo veloce ed efficiente per copiare dati da una variabile di programma in una tabella in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Chiamare [bcp_init](bcp-init.md) prima di chiamare questa o qualsiasi altra funzione di copia bulk. La chiamata **bcp_init** imposta il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella di destinazione per la copia bulk. Quando si chiama **bcp_init** per l'uso con **bcp_bind** e [bcp_sendrow](bcp-sendrow.md), il **bcp_init** _szDataFile_parametro, che indica il file di dati è impostato su NULL. il **bcp_init**_eDirection_ parametro è impostato su DB_IN.  
  
 Rendere un oggetto separato **bcp_bind** chiamato per ogni colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella in cui si desidera copiare. Dopo la necessaria **bcp_bind** chiamate sono state apportate, quindi chiamare **bcp_sendrow** per inviare una riga di dati da variabili di programma a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La riassociazione della colonna non è supportata.  
  
 Ogni volta che si desidera [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire il commit delle righe già ricevute, chiamare [bcp_batch](bcp-batch.md). Ad esempio, chiamare **bcp_batch** una volta per ogni 1000 righe inserite o in un altro intervallo.  
  
 Quando non sono presenti altre righe da inserire, chiamare [bcp_done](bcp-done.md). In caso contrario, viene generato un errore.  
  
 Controllare le impostazioni dei parametri specificate con [bcp_control](bcp-control.md), non hanno effetto sui **bcp_bind** trasferimenti di righe.  
  
 Se *pData* per una colonna è impostata su NULL perché il relativo valore verrà fornito dalle chiamate a [bcp_moretext](bcp-moretext.md), eventuali colonne successive in cui *eDataType* impostato su SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR o SQLIMAGE deve essere associate con *pData* impostato su NULL e i relativi valori devono anche essere forniti dalle chiamate a `bcp_moretext`.  
  
 Per i nuovi tipi di valori di grandi dimensioni, ad esempio `varchar(max)`, `varbinary(max)`, o `nvarchar(max)`, è possibile utilizzare SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY e SQLNCHAR come indicatori di tipo nel *eDataType* parametro.  
  
 Se *cbTerm* è diverso da 0, qualsiasi valore (1, 2, 4 o 8) non è valido per il prefisso (*cbIndicator*). In questo caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client verrà Cerca il carattere di terminazione, calcolare la lunghezza dei dati per il carattere di terminazione (*i*) e impostare il *cbData* al valore più piccolo di i e il valore di prefisso.  
  
 Se *cbTerm* è 0 e *cbIndicator* (il prefisso) non è 0, *cbIndicator* deve essere 8. Al prefisso a 8 byte possono essere assegnati i valori seguenti:  
  
-   0xFFFFFFFFFFFFFFFF indica un valore Null per il campo  
  
-   0xFFFFFFFFFFFFFFFE viene trattato come valore di prefisso speciale utilizzato per inviare dati in blocchi al server in modo efficace. Il formato dei dati con questo prefisso speciale è:  
  
-   < SPECIAL_PREFIX > \<0 o più BLOCCHI di dati >< ZERO_CHUNK > dove:  
  
-   SPECIAL_PREFIX è 0xFFFFFFFFFFFFFFFE  
  
-   DATA_CHUNK è un prefisso a 4 byte che contiene la lunghezza del blocco, seguita dai dati effettivi la cui lunghezza viene specificata nel prefisso a 4 byte.  
  
-   ZERO_CHUNK è un valore a 4 byte che contiene tutti zeri (00000000) che indicano la fine dei dati.  
  
-   Qualsiasi altra lunghezza a 8 byte valida viene trattata come una lunghezza dei dati normale.  
  
 La chiamata [bcp_columns](bcp-columns.md) quando si usa **bcp_bind** provoca un errore.  
  
## <a name="bcpbind-support-for-enhanced-date-and-time-features"></a>Supporto di bcp_bind per le caratteristiche avanzate di data e ora  
 Per informazioni sui tipi utilizzati con il *eDataType* parametro per i tipi di data/ora, vedere [modifiche di copia di massa per i tipi di tempo ed Enhanced Data &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Per altre informazioni, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="example"></a>Esempio  
  
```  
#include sql.h  
#include sqlext.h  
#include odbcss.h  
// Variables like henv not specified.  
HDBC      hdbc;  
char         szCompanyName[MAXNAME];  
DBINT      idCompany;  
DBINT      nRowsProcessed;  
DBBOOL      bMoreData;  
char*      pTerm = "\t\t";  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source; return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bcp.   
if (bcp_init(hdbc, "comdb..accounts_info", NULL, NULL  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.   
if (bcp_bind(hdbc, (LPCBYTE) &idCompany, 0, sizeof(DBINT), NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_bind(hdbc, (LPCBYTE) szCompanyName, 0, SQL_VARLEN_DATA,  
   (LPCBYTE) pTerm, strnlen(pTerm, sizeof(pTerm)), SQLCHARACTER, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
while (TRUE)  
   {  
   // Retrieve and process program data.   
   if ((bMoreData = getdata(&idCompany, szCompanyName)) == TRUE)  
      {  
      // Send the data.   
      if (bcp_sendrow(hdbc) == FAIL)  
         {  
         // Raise error and return.  
         return;  
         }  
      }  
   else  
      {  
      // Break out of loop.  
      break;  
      }  
   }  
  
// Terminate the bulk copy operation.  
if ((nRowsProcessed = bcp_done(hdbc)) == -1)  
   {  
   printf_s("Bulk-copy unsuccessful.\n");  
   return;  
   }  
  
printf_s("%ld rows copied.\n", nRowsProcessed);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
