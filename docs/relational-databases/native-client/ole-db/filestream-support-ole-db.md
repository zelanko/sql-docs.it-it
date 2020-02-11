---
title: Supporto FILESTREAM (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ff05424d9b8726f21c8c4aa2facd42b87961cc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73760872"
---
# <a name="filestream-support-ole-db"></a>Supporto FILESTREAM (OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  A partire [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e Native Client 10,0, OLE DB supporta la funzionalità FILESTREAM avanzata. Per ulteriori informazioni su questa funzionalità, vedere [supporto FILESTREAM](../../../relational-databases/native-client/features/filestream-support.md). Per esempi, vedere [FileStream e OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Per inviare e ricevere valori **varbinary (max)** maggiori di 2 GB, un'applicazione utilizza **DBTYPE_IUNKNOWN** nelle associazioni di parametri e risultati. Per i parametri, il provider deve chiamare IUnknown:: QueryInterface per ISequentialStream e per i risultati che restituiscono ISequentialStream.  
  
 Per OLE DB, il controllo relativo ai valori ISequentialStream verrà rilassato. Quando *wType* è **DBTYPE_IUNKNOWN** nello struct **DBBINDING** , il controllo della lunghezza può essere disabilitato omettendo **DBPART_LENGTH** da *dwPart* o impostando la lunghezza dei dati (in corrispondenza dell'offset *obLength* nel buffer di dati) su ~ 0. In questo caso, il provider non controllerà la lunghezza del valore e richiederà e restituirà tutti i dati disponibili tramite il flusso. Questa modifica verrà applicata a tutti i tipi LOB (Large Object) e XML, ma solo in caso di connessione a server [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva. In questo modo, gli sviluppatori disporranno di maggiore flessibilità, mantenendo la coerenza e la compatibilità con le versioni precedenti per applicazioni esistenti e server legacy.  
  
 Questa modifica ha effetto su tutte le interfacce che trasferiscono i dati, principalmente IRowset:: GetData, ICommand:: Execute e IRowsetFastLoad:: InsertRow.  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione in SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
