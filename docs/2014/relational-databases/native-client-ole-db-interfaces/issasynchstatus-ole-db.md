---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSAsynchStatus (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aeb6c6c789bfe1ca2af5616fb0a1ef9785700224
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127765"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
  **ISSAsynchStatus** espone il supporto per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operazioni asincrone. Si tratta di un'interfaccia facoltativa eredita dall'interfaccia OLE DB principale **IDBAsynchStatus**. Oltre ai metodi **Abort** e **GetStatus** ereditati da **IDBAsynchStatus**, **ISSAsynchStatus** fornisce un nuovo metodo, utilizzato per attendere il completamento dell'operazione asincrona o il verificarsi di un timeout.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort &#40;OLE DB&#41;](issasynchstatus-abort-ole-db.md)|Annulla un'operazione di esecuzione asincrona.|  
|[ISSAsynchStatus::GetStatus &#40;OLE DB&#41;](issasynchstatus-getstatus-ole-db.md)|Restituisce lo stato di un'operazione in esecuzione in modo asincrono.|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](issasynchstatus-waitforasynchcompletion-ole-db.md)|Resta in attesa fino al completamento dell'operazione di esecuzione asincrona o fino al verificarsi di un timeout.|  
  
## <a name="remarks"></a>Note  
 L'implementazione **ISSAsynchStatus** del metodo **ISSAsynchStatus::GetStatus** coincide con quella del metodo **IDBAsynchStatus::GetStatus**, ad eccezione del fatto che se l'inizializzazione di un'origine dati viene interrotta, viene restituito E_UNEXPECTED anziché DB_E_CANCELED (benché **ISSAsynchStatus::WaitForAsynchCompletion** restituisca DB_E_CANCELED). Ciò è dovuto al fatto che l'oggetto origine dati non viene lasciato nello stato consueto in seguito a un'operazione di interruzione, in modo da consentire ulteriori tentativi di operazioni di inizializzazione.  
  
 I metodi seguenti supportano l'utilizzo dell'esecuzione asincrona in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>Vedere anche  
 [Le interfacce &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [Esecuzione di operazioni asincrone](../native-client/features/performing-asynchronous-operations.md)  
  
  
