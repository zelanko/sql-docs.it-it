---
description: Supporto FILESTREAM (OLE DB)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8dd62a70c60ff1242aa4ea8b81c85e9ae6046ea1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428073"
---
# <a name="filestream-support-ole-db"></a>Supporto FILESTREAM (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  A partire da [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10,0, OLE DB supporta la funzionalità FILESTREAM avanzata. Per ulteriori informazioni su questa funzionalità, vedere [supporto FILESTREAM](../../../relational-databases/native-client/features/filestream-support.md). Per gli esempi, vedere [FILESTREAM e OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Per inviare e ricevere valori **varbinary(max)** maggiori di 2 GB, un'applicazione usa **DBTYPE_IUNKNOWN** in associazioni di parametri e di risultati. Per i parametri il provider deve chiamare IUnknown::QueryInterface per ISequentialStream e per i risultati che restituiscono ISequentialStream.  
  
 Per OLE DB il controllo relativo ai valori ISequentialStream diventa meno rigido. Se *wType* è **DBTYPE_IUNKNOWN** nello struct **DBBINDING**, il controllo della lunghezza può essere disabilitato omettendo **DBPART_LENGTH** in *dwPart* o impostando la lunghezza dei dati (in corrispondenza dell'offset *obLength* nel buffer dei dati) su ~0. In questo caso, il provider non controllerà la lunghezza del valore e richiederà e restituirà tutti i dati disponibili tramite il flusso. Questa modifica verrà applicata a tutti i tipi LOB (Large Object) e XML, ma solo in caso di connessione a server [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva. In questo modo, gli sviluppatori disporranno di maggiore flessibilità, mantenendo la coerenza e la compatibilità con le versioni precedenti per applicazioni esistenti e server legacy.  
  
 Questa modifica ha effetto su tutte le interfacce che trasferiscono dati, principalmente IRowset::GetData, ICommand::Execute e IRowsetFastLoad::InsertRow.  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione in SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
