---
title: IBCPSession::BCPColumns (OLE DB) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPColumns (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPColumns method
ms.assetid: c338abe8-9e30-4853-a7c6-b1a6c00095e1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7108760ebdb5e7e3e6367b801b07d4f8140a62d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238738"
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns (OLE DB)
  Imposta il numero di campi da associare alle colonne di una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT BCPColumns(   
DBCOUNTITEMnColumns);  
```  
  
## <a name="remarks"></a>Note  
 Chiama internamente [IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md) per impostare i valori predefiniti per i dati dei campi. Questi valori predefiniti vengono ottenuti dalle informazioni sulle colonne di SQL Server recuperate internamente dal provider quando si specifica il nome di tabella tramite [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md).  
  
> [!NOTE]  
>  È possibile chiamare questo metodo solo dopo avere chiamato **BCPInit** con un nome di file valido.  
  
 È consigliabile chiamare questo metodo solo se si intende utilizzare un formato di file utente diverso da quello predefinito. Per ulteriori informazioni su una descrizione del formato di file utente predefinito, vedere il metodo **BCPInit**.  
  
 Dopo avere chiamato il metodo **BCPColumns**, è necessario chiamare il metodo **BCPColFmt** per ogni colonna del file utente per definire in modo completo un formato di file personalizzato.  
  
## <a name="arguments"></a>Argomenti  
 *nColumns*[in]  
 Numero totale di campi nel file utente. Anche se si prepara la copia bulk dei dati dal file utente in una tabella di SQL Server e non si prevede di copiare tutti i campi del file utente, è comunque necessario impostare l'argomento *nColumns* sul numero totale di campi del file utente. I campi ignorati possono quindi essere specificati tramite **BCPColFmt**.  
  
## <a name="return-code-values"></a>Valori restituiti  
 S_OK  
 Il metodo è riuscito.  
  
 E_FAIL  
 Si è verificato un errore specifico del provider. Per informazioni dettagliate, usare l'interfaccia [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md).  
  
 E_UNEXPECTED  
 La chiamata al metodo non era prevista. Non è stato ad esempio chiamato il metodo **BCPInit** prima della chiamata a questo metodo. Si verifica inoltre quando questo metodo viene chiamato più volte per un'operazione di copia bulk.  
  
 E_OUTOFMEMORY  
 Errore di memoria insufficiente.  
  
## <a name="see-also"></a>Vedere anche  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Esecuzione di operazioni di copia bulk](../native-client/features/performing-bulk-copy-operations.md)  
  
  
