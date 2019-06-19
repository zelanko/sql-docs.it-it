---
title: Il recupero di una singola riga con IRow | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: faf887ab5e03d2d0ca8702dc9bd35d0ba094ece4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183672"
---
# <a name="fetching-a-single-row-with-irow"></a>Recupero di una sola riga utilizzando IRow
  Il **IRow** implementazione nell'interfaccia di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider è stato semplificato per migliorare le prestazioni. **IRow** consente l'accesso diretto alle colonne di un singolo oggetto riga. Se si prevede che il risultato dell'esecuzione di un comando produca esattamente una riga, **IRow** recupererà le colonne della riga in questione. Se il set di risultati include più righe, **IRow** esporrà solo la prima.  
  
 L'implementazione dell'interfaccia **IRow** non consente la navigazione all'interno della riga. Ogni colonna nella riga avviene solo una volta con una sola eccezione: Una colonna è accessibile una sola volta per trovarne le dimensioni e un'altra per recuperare i dati.  
  
> [!NOTE]  
>  **IRow::Open** supporta solo i tipi DBGUID_STREAM e DBGUID_NULL di oggetti da aprire.  
  
 Per ottenere un oggetto riga utilizzando il metodo **ICommand::Execute**, è necessario passare IID_IRow. L'interfaccia **IMultipleResults** deve essere utilizzata per gestire più set di risultati. **IMultipleResults** supporta **IRow** e **IRowset**. **IRowset** viene utilizzata per le operazioni bulk.  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Uso di IRow::GetColumns](using-irow-getcolumns.md)  
  
-   [Recupero di dati BLOB tramite IRow](../../database-engine/dev-guide/fetching-blob-data-using-irow.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Set di righe](rowsets.md)  
  
  
