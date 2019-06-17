---
title: bcp_exec | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_exec
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_exec function
ms.assetid: b23ea2cc-8545-4873-b0c1-57e76b0a3a7b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d5ce458ea8f5874620ea0561eeea5c6ff8e56bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62689040"
---
# <a name="bcpexec"></a>bcp_exec
  Esegue una copia bulk completa di dati tra una tabella di database e un file utente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_exec (  
HDBC   
hdbc  
,  
LPDBINT   
pnRowsProcessed  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
 *pnRowsProcessed*  
 Puntatore a DBINT. Il **bcp_exec** funzione DBInt con il numero di righe copiate correttamente. Se *pnRowsProcessed* è NULL, viene ignorato dal **bcp_exec**.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED, SUCCEED_ASYNC o FAIL. Il **bcp_exec** funzione restituisce SUCCEED se vengono copiate tutte le righe. **bcp_exec** restituisce SUCCEED_ASYNC se un'operazione di copia bulk asincrona è ancora in attesa. **bcp_exec** restituisce FAIL se si verifica un errore completo o se il numero di righe che generano errori raggiunge il valore specificato per BCPMAXERRS tramite [bcp_control](bcp-control.md). Il valore predefinito BCPMAXERRS è 10. L'opzione BCPMAXERRS influisce solo sugli errori di sintassi rilevati dal provider durante la lettura delle righe dal file di dati, ma non delle righe inviate al server. Il server interrompe il batch quando rileva un errore con una riga. Verificare i *pnRowsProcessed* parametro per il numero di righe copiate correttamente.  
  
## <a name="remarks"></a>Note  
 Questa funzione Copia dati da un file utente a una tabella di database o viceversa, in base al valore di *eDirection* nel parametro [bcp_init](bcp-init.md).  
  
 Prima di chiamare **bcp_exec**, chiamare **bcp_init** con un nome di file utente valido. In caso contrario, viene generato un errore.  
  
 **bcp_exec** è l'unica funzione di copia che probabilmente continuerà a rimanere in attesa per un periodo di tempo in blocco. è anche l'unica funzione di copia bulk che supporta la modalità asincrona. Per impostare la modalità asincrona, utilizzare [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) per impostare SQL_ATTR_ASYNC_ENABLE su SQL_ASYNC_ENABLE_ON prima di chiamare **bcp_exec**. Per testare il completamento, chiamare **bcp_exec** con gli stessi parametri. Se la copia bulk non ha ancora completato, **bcp_exec** restituisce SUCCEED_ASYNC. Restituisce inoltre nel *pnRowsProcessed* un conteggio dello stato del numero di righe che sono stati inviati al server. Il commit delle righe inviate al server non viene eseguito fino a quando non viene raggiunta la fine di un batch.  
  
 Per informazioni su una sostanziale modifica inizio la copia di massa in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], vedere [esecuzione di operazioni di copia di massa &#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare **bcp_exec**:  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, _T("pubs..authors"), _T("authors.sav"), NULL, DB_OUT)  
   == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Now, execute the bulk copy.   
if (bcp_exec(hdbc, &nRowsProcessed) == FAIL)  
   {  
   if (nRowsProcessed == -1)  
      {  
      printf_s("No rows processed on bulk copy execution.\n");  
      }  
   else  
      {  
      printf_s("Incomplete bulk copy.   Only %ld row%s copied.\n",  
         nRowsProcessed, (nRowsProcessed == 1) ? "": "s");  
      }  
   return;  
   }  
  
printf_s("%ld rows processed.\n", nRowsProcessed);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
