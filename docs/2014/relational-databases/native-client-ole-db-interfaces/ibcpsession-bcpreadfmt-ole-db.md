---
title: 'Ibcpsession:: Bcpreadfmt (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPReadFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPReadFmt method
ms.assetid: e2a12050-94e4-48a3-8a48-b780d646f116
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a82cd2b9261b8f8c26e4e37636423cc27603fcc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192418"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
  Legge le informazioni sul formato per ogni colonna dal file di formato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT BCPReadFmt(   
const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Note  
 Il metodo **BCPReadFmt** viene usato per la lettura di dati da un file di formato che specifica il formato dei dati nel file di dati. Questo metodo è in grado di rilevare la versione corretta del file di formato. Può rilevare automaticamente se il file è in formato xml o testo stile antico e comportarsi di conseguenza. Le versioni di file di formato supportate dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BCP del provider OLE DB Native Client sono versione 6.0 o versione successiva.  
  
 Dopo la lettura dei valori del formato, il metodo **BCPReadFmt** effettua le chiamate appropriate ai metodi [IBCPSession::BCPColumns](ibcpsession-bcpcolumns-ole-db.md) e [IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md). L'utente può evitare di analizzare un file di formato ed effettuare queste chiamate.  
  
 Per salvare un file di formato, chiamare il metodo [IBCPSession::BCPWriteFmt](ibcpsession-bcpwritefmt-ole-db.md). Le chiamate al metodo **BCPReadFmt** possono fare riferimento ai formati salvati. In alternativa, l'utilità per la copia bulk (**bcp**) può salvare i formati di dati definiti dall'utente in file ai quali può fare riferimento il metodo **BCPReadFmt**.  
  
 Il `BCP_OPTION_DELAYREADFMT` pari al *eOption* parametro [ibcpsession:: Bcpcontrol](ibcpsession-bcpcontrol-ole-db.md) modifica il comportamento di ibcpsession:: Bcpreadfmt.  
  
## <a name="arguments"></a>Argomenti  
 *pwszFormatFile*[in]  
 Percorso e nome del file contenente i valori di formato per il file di dati.  
  
## <a name="return-code-values"></a>Valori restituiti  
 S_OK  
 Il metodo è riuscito.  
  
 E_FAIL  
 Si è verificato un errore specifico del provider. Per informazioni dettagliate, usare l'interfaccia [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md).  
  
 E_OUTOFMEMORY  
 Errore di memoria insufficiente.  
  
 E_UNEXPECTED  
 La chiamata al metodo non era prevista. Non è stato ad esempio chiamato il metodo [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) prima della chiamata a questo metodo.  
  
## <a name="see-also"></a>Vedere anche  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Esecuzione di operazioni di copia bulk](../native-client/features/performing-bulk-copy-operations.md)  
  
  
