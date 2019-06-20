---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSAbort::Abort (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ad1310112b3cd6ac536a55a82757ae99433372d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62511515"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
  Annulla il set di righe corrente oltre a qualsiasi comando eseguito in batch associato al comando corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Note  
 Se il comando interrotto è in una stored procedure, l'esecuzione della stored procedure (e di qualsiasi procedura che ha chiamato la procedura) verrà terminata insieme al batch di comandi che contiene la chiamata alla stored procedure. Se nel server è in corso il trasferimento di un set di risultati al client, questo processo verrà arrestato. Se il client non desidera utilizzare un set di risultati, la chiamata a **ISSAbort::Abort** prima di rilasciare il set di righe accelererà il rilascio del set di righe, ma se è presente una transazione aperta e XACT_ABORT è ON, verrà eseguito il rollback della transazione quando viene chiamato **ISSAbort::Abort**  
  
 Dopo aver **issabort:: Abort** restituisce S_OK, associato **IMultipleResults** interfaccia entra in uno stato inutilizzabile e restituisce DB_E_CANCELED a tutte le chiamate al metodo (ad eccezione dei metodi definiti per il **IUnknown** interface) fino a quando non viene rilasciato. Se si ottiene un'interfaccia **IRowset** da **IMultipleResults** prima di una chiamata a **Abort**, anche questa interfaccia passa in uno stato inutilizzabile e restituisce DB_E_CANCELED a tutte le chiamate ai metodi, ad eccezione dei metodi definiti dall'interfaccia **IUnknown** e da **IRowset::ReleaseRows**, fino a quando non viene rilasciata in seguito a una chiamata riuscita a **ISSAbort::Abort**.  
  
> [!NOTE]  
>  A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], se lo stato XACT_ABORT del server è ON, l'esecuzione di **ISSAbort::Abort** terminerà qualsiasi transazione implicita o esplicita e ne eseguirà il rollback durante la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la transazione corrente non viene interrotta.  
  
## <a name="arguments"></a>Argomenti  
 Nessuna.  
  
## <a name="return-code-values"></a>Valori restituiti  
 S_OK  
 Il metodo **ISSAbort::Abort** restituisce S_OK se il batch è stato annullato e DB_E_CANTCANCEL in caso contrario. Se il batch è già stato annullato, viene restituito DB_E_CANCELED.  
  
 DB_E_CANCELED  
 Il batch è già stato annullato.  
  
 DB_E_CANTCANCEL  
 Il batch non è stato annullato.  
  
 E_FAIL  
 Si è verificato un errore specifico del provider; Per informazioni dettagliate, usare il [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) interfaccia.  
  
 E_UNEXPECTED  
 La chiamata al metodo non era prevista. Lo stato dell'oggetto, ad esempio, è in dubbio in quanto **ISSAbort::Abort** è già stato chiamato.  
  
 E_OUTOFMEMORY  
 Errore di memoria insufficiente.  
  
## <a name="see-also"></a>Vedere anche  
 [ISSAbort &#40;OLE DB&#41;](../../database-engine/dev-guide/issabort-ole-db.md)  
  
  
