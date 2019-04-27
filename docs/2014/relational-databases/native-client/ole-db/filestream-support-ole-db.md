---
title: Supporto FILESTREAM (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad6aa7b55906e68dba6615140ef2c6afcc3efaa5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62668934"
---
# <a name="filestream-support-ole-db"></a>Supporto FILESTREAM (OLE DB)
  A partire [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, OLE DB supporta la caratteristica FILESTREAM avanzata. Per altre informazioni su questa funzionalità, vedere [supporto FILESTREAM](../features/filestream-support.md). Per esempi, vedere [Filestream e OLE DB](../../native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Per inviare e ricevere valori `varbinary(max)` maggiori di 2 GB, un'applicazione utilizza `DBTYPE_IUNKNOWN` in associazioni di parametri e di risultati. Per i parametri il provider deve chiamare IUnknown:: QueryInterface per ISequentialStream e per ottenere risultati che restituiscono ISequentialStream.  
  
 Per OLE DB, viene aumentato il controllo correlato ai valori di ISequentialStream. Quando *wType* viene `DBTYPE_IUNKNOWN` nel `DBBINDING` struct, controllo della lunghezza può essere disabilitate omettendo `DBPART_LENGTH` da *dwPart* o impostando la lunghezza dei dati (in corrispondenza dell'offset *obLength* nel buffer di dati) a ~ 0. In questo caso, il provider non controllerà la lunghezza del valore e richiederà e restituirà tutti i dati disponibili tramite il flusso. Questa modifica verrà applicata a tutti i tipi LOB (Large Object) e XML, ma solo in caso di connessione a server [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva. In questo modo, gli sviluppatori disporranno di maggiore flessibilità, mantenendo la coerenza e la compatibilità con le versioni precedenti per applicazioni esistenti e server legacy.  
  
 Questa modifica interessa tutte le interfacce che trasferiscono dati, principalmente IRowset:: GetData ICommand:: Execute e IRowsetFastLoad:: InsertRow.  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione in SQL Server Native Client](../sql-server-native-client-programming.md)  
  
  
