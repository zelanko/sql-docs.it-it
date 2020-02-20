---
title: ISSAbort::Abort (OLE DB) | Microsoft Docs
description: ISSAbort::Abort (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 72ce7fa29adfb349fab8c9e60872740c94484108
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994391"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Annulla il set di righe corrente oltre a qualsiasi comando eseguito in batch associato al comando corrente.  
  
L'interfaccia **ISSAbort**, esposta nel driver OLE DB per SQL Server, fornisce il metodo **ISSAbort::Abort** che viene utilizzato per annullare il set di righe corrente oltre a qualsiasi comando eseguito in batch insieme al comando che ha inizialmente generato il set di righe e non ha ancora completato l'esecuzione.  
  
 **ISSAbort** è un'interfaccia specifica del driver OLE DB per SQL Server disponibile mediante **QueryInterface** sull'oggetto **IMultipleResults** restituito da **ICommand::Execute** o **IOpenRowset::OpenRowset**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Osservazioni  
 Se il comando interrotto è in una stored procedure, l'esecuzione della stored procedure (e di qualsiasi procedura che ha chiamato la procedura) verrà terminata insieme al batch di comandi che contiene la chiamata alla stored procedure. Se nel server è in corso il trasferimento di un set di risultati al client, questo processo verrà arrestato. Se il client non desidera utilizzare un set di risultati, la chiamata a **ISSAbort::Abort** prima di rilasciare il set di righe accelererà il rilascio del set di righe, ma se è presente una transazione aperta e XACT_ABORT è ON, verrà eseguito il rollback della transazione quando viene chiamato **ISSAbort::Abort**  
  
 Dopo che **ISSAbort::Abort** restituisce S_OK, l'interfaccia **IMultipleResults** associata passa in uno stato inutilizzabile e restituisce DB_E_CANCELED a tutte le chiamate ai metodi, ad eccezione dei metodi definiti dall'interfaccia **IUnknown**, fino a quando non viene rilasciata. Se si ottiene un'interfaccia **IRowset** da **IMultipleResults** prima di una chiamata a **Abort**, anche questa interfaccia passa in uno stato inutilizzabile e restituisce DB_E_CANCELED a tutte le chiamate ai metodi, ad eccezione dei metodi definiti dall'interfaccia **IUnknown** e da **IRowset::ReleaseRows**, fino a quando non viene rilasciata in seguito a una chiamata riuscita a **ISSAbort::Abort**.  
  
> [!NOTE]  
>  A partire da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], se lo stato XACT_ABORT del server è ON, l'esecuzione di **ISSAbort::Abort** terminerà qualsiasi transazione implicita o esplicita e ne eseguirà il rollback durante la connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la transazione corrente non viene interrotta.  
  
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
 Si è verificato un errore specifico del provider. Per informazioni dettagliate, usare l'interfaccia [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).  
  
 E_UNEXPECTED  
 La chiamata al metodo non era prevista. Lo stato dell'oggetto, ad esempio, è in dubbio in quanto **ISSAbort::Abort** è già stato chiamato.  
  
 E_OUTOFMEMORY  
 Errore di memoria insufficiente.  
  
  
