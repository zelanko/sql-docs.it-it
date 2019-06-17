---
title: I livelli di isolamento (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a18986af71f652a833f413ee1fa62ca2fd44ba06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63215988"
---
# <a name="isolation-levels-ole-db"></a>Livelli di isolamento (OLE DB)
  I client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono controllare i livelli di isolamento delle transazioni per una connessione. Per controllare il livello di isolamento delle transazioni, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer di provider OLE DB Native Client utilizza:  
  
-   Proprietà DBPROPSET_SESSION dbprop_session_autocommitisolevels per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modalità autocommit predefinita del provider OLE DB Native Client.  
  
     Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinito di provider OLE DB Native Client per il livello è DBPROPVAL_TI_READCOMMITTED.  
  
-   Parametro *isoLevel* del metodo **ITransactionLocal::StartTransaction** per le transazioni locali di cui viene eseguito il commit manuale.  
  
-   Parametro *isoLevel* del metodo **ITransactionDispenser::BeginTransaction** per le transazioni distribuite coordinate da MS DTC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente accesso di sola lettura nel livello di isolamento di lettura dirty. Tutti gli altri livelli limitano la concorrenza applicando blocchi agli oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Poiché il client richiede livelli di concorrenza maggiori, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] applica restrizioni superiori all'accesso simultaneo ai dati. Per mantenere il massimo livello di accesso simultaneo ai dati, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB Native Client deve controllare in modo intelligenze le richieste per i livelli di concorrenza specifici.  
  
> [!NOTE]  
>  In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] è stato introdotto il livello di isolamento dello snapshot. Per altre informazioni, vedere [Uso dell'isolamento dello snapshot](../native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Transazioni](transactions.md)  
  
  
