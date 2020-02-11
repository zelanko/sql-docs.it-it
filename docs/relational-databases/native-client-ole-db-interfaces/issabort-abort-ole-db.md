---
title: 'Dissabot:: Abort (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d66d37da3ba2de7f12cefb8f806c44d5dd967003
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73763174"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Annulla il set di righe corrente oltre a qualsiasi comando eseguito in batch associato al comando corrente.  
  
L'interfaccia **ISSAbort** , esposta nel provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, fornisce il metodo **ISSAbort::Abort** che viene utilizzato per annullare il set di righe corrente oltre a qualsiasi comando eseguito in batch insieme al comando che ha inizialmente generato il set di righe e non ha ancora completato l'esecuzione.  
  
 **È un'** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaccia specifica del provider di Native Client disponibile usando **QueryInterface** sull'oggetto **IMultipleResults** restituito da **ICommand:: Execute** o **IOpenRowset:: OPENROWSET**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Osservazioni  
 Se il comando interrotto è in una stored procedure, l'esecuzione della stored procedure (e di qualsiasi procedura che ha chiamato la procedura) verrà terminata insieme al batch di comandi che contiene la chiamata alla stored procedure. Se nel server è in corso il trasferimento di un set di risultati al client, questo processo verrà arrestato. Se il client non desidera utilizzare un set di risultati, la chiamata a **ISSAbort::Abort** prima di rilasciare il set di righe accelererà il rilascio del set di righe, ma se è presente una transazione aperta e XACT_ABORT è ON, verrà eseguito il rollback della transazione quando viene chiamato **ISSAbort::Abort**  
  
 Dopo che il metodo IsDefined **:: Abort** restituisce S_OK, l'interfaccia **IMultipleResults** associata entra in uno stato inutilizzabile e restituisce DB_E_CANCELED a tutte le chiamate ai metodi, ad eccezione dei metodi definiti dall'interfaccia **IUnknown** , fino a quando non viene rilasciata. Se si ottiene un'interfaccia **IRowset** da **IMultipleResults** prima di una chiamata a **Abort**, anche questa interfaccia passa in uno stato inutilizzabile e restituisce DB_E_CANCELED a tutte le chiamate ai metodi, ad eccezione dei metodi definiti dall'interfaccia **IUnknown** e da **IRowset::ReleaseRows**, fino a quando non viene rilasciata in seguito a una chiamata riuscita a **ISSAbort::Abort**.  
  
> [!NOTE]  
>  A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], se lo stato XACT_ABORT del server è ON, l'esecuzione di **ISSAbort::Abort** terminerà qualsiasi transazione implicita o esplicita e ne eseguirà il rollback durante la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la transazione corrente non viene interrotta.  
  
## <a name="arguments"></a>Argomenti  
 No.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 S_OK  
 Il metodo **ISSAbort::Abort** restituisce S_OK se il batch è stato annullato e DB_E_CANTCANCEL in caso contrario. Se il batch è già stato annullato, viene restituito DB_E_CANCELED.  
  
 DB_E_CANCELED  
 Il batch è già stato annullato.  
  
 DB_E_CANTCANCEL  
 Il batch non è stato annullato.  
  
 E_FAIL  
 Si è verificato un errore specifico del provider. per informazioni dettagliate, usare l'interfaccia [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) .  
  
 E_UNEXPECTED  
 La chiamata al metodo non era prevista. Lo stato dell'oggetto, ad esempio, è in dubbio in quanto **ISSAbort::Abort** è già stato chiamato.  
  
 E_OUTOFMEMORY  
 Errore di memoria insufficiente.  
  
## <a name="see-also"></a>Vedere anche  
 [&#40;OLE DB&#41;](https://msdn.microsoft.com/library/7c4df482-4a83-4da0-802b-3637b507693a)  
  
  
