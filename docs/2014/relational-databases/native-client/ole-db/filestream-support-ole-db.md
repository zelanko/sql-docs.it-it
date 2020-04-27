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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62668934"
---
# <a name="filestream-support-ole-db"></a>Supporto FILESTREAM (OLE DB)
  A partire [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e Native Client 10,0, OLE DB supporta la funzionalità FILESTREAM avanzata. Per ulteriori informazioni su questa funzionalità, vedere [supporto FILESTREAM](../features/filestream-support.md). Per gli esempi, vedere [FILESTREAM e OLE DB](../../native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Per inviare e ricevere valori `varbinary(max)` maggiori di 2 GB, un'applicazione utilizza `DBTYPE_IUNKNOWN` in associazioni di parametri e di risultati. Per i parametri il provider deve chiamare IUnknown::QueryInterface per ISequentialStream e per i risultati che restituiscono ISequentialStream.  
  
 Per OLE DB il controllo relativo ai valori ISequentialStream diventa meno rigido. Quando *wType* è `DBTYPE_IUNKNOWN` nello struct `DBBINDING` , il controllo `DBPART_LENGTH` della lunghezza può essere disabilitato omettendo da *dwPart* o impostando la lunghezza dei dati (in corrispondenza dell'offset *obLength* nel buffer di dati) su ~ 0. In questo caso, il provider non controllerà la lunghezza del valore e richiederà e restituirà tutti i dati disponibili tramite il flusso. Questa modifica verrà applicata a tutti i tipi LOB (Large Object) e XML, ma solo in caso di connessione a server [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva. In questo modo, gli sviluppatori disporranno di maggiore flessibilità, mantenendo la coerenza e la compatibilità con le versioni precedenti per applicazioni esistenti e server legacy.  
  
 Questa modifica ha effetto su tutte le interfacce che trasferiscono dati, principalmente IRowset::GetData, ICommand::Execute e IRowsetFastLoad::InsertRow.  
  
## <a name="see-also"></a>Vedi anche  
 [Programmazione in SQL Server Native Client](../sql-server-native-client-programming.md)  
  
  
