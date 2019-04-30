---
title: ISQLServerErrorInfo::GetErrorInfo (OLE DB) | Documenti di Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetErrorInfo method
ms.assetid: 83265c9c-eaf9-41f0-9f73-b0ae0972f0d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9131c65236a0efffa19aab2bd10b1fd8e309653b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127782"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
  Restituisce un puntatore a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider SSERRORINFO struttura contenente la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dettagli errore.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
   HRESULT GetErrorInfo(  
SSERRORINFO**ppSSErrorInfo,  
OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>Argomenti  
 *ppSSErrorInfo*[out]  
 Puntatore a una struttura SSERRORINFO. Se il metodo non riesce o non sono disponibili informazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associate all'errore, il provider non alloca memoria e verifica che l'argomento *ppSSErrorInfo* sia un puntatore Null nell'output.  
  
 *ppErrorStrings*[out]  
 Puntatore a un puntatore stringa carattere Unicode. Se il metodo non riesce o non sono disponibili informazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associate a un errore, il provider non alloca memoria e verifica che l'argomento *ppErrorStrings* sia un puntatore Null nell'output. Liberando l'argomento *ppErrorStrings* con il metodo **IMalloc::Free**, vengono liberati i tre singoli membri della stringa della struttura SSERRORINFO restituita, in quanto la memoria è allocata in un blocco.  
  
## <a name="return-code-values"></a>Valori restituiti  
 S_OK  
 Il metodo è riuscito.  
  
 E_INVALIDARG  
 Entrambi i *ppSSErrorInfo* o *ppErrorStrings* argomento era NULL.  
  
 E_OUTOFMEMORY  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider non è riuscito ad allocare memoria sufficiente per completare la richiesta.  
  
## <a name="remarks"></a>Note  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider alloca memoria per le stringhe SSERRORINFO e OLECHAR restituite tramite i puntatori passati dal consumer. Il consumer deve deallocare questa memoria tramite il metodo **IMalloc::Free** quando l'accesso ai dati dell'errore non è più necessario.  
  
 La struttura SSERRORINFO viene definita nel modo seguente:  
  
```  
typedef struct tagSSErrorInfo  
   {  
   LPOLESTR pwszMessage;  
   LPOLESTR pwszServer;  
   LPOLESTR pwszProcedure;  
   LONG lNative;  
   BYTE bState;  
   BYTE bClass;  
   WORD wLineNumber;  
   }  
SSERRORINFO;  
```  
  
|Membro|Descrizione|  
|------------|-----------------|  
|*pwszMessage*|Messaggio di errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il messaggio viene restituito attraverso il metodo **IErrorInfo::GetDescription**.|  
|*pwszServer*|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si è verificato l'errore.|  
|*pwszProcedure*|Nome della stored procedure che genera l'errore se esso si è verificato all'interno della stessa, in caso contrario, una stringa vuota.|  
|*lNative*|Numero di errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il numero di errore è identico a quello restituito nel parametro *plNativeError* del metodo **ISQLErrorInfo::GetSQLInfo**.|  
|*bState*|Stato dell'errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*bClass*|Gravità dell'errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Quando applicabile, riga di una stored procedure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ha generato il messaggio di errore. Se non è coinvolta alcuna procedura, il valore predefinito è 1.|  
  
 I puntatori nella struttura fanno riferimento agli indirizzi nella stringa restituita nell'argomento *ppErrorStrings*.  
  
## <a name="see-also"></a>Vedere anche  
 [ISQLServerErrorInfo per la &#40;OLE DB&#41;](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)   
 [RAISERROR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
