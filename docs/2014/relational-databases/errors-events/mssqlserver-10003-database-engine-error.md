---
title: MSSQLSERVER_10003 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10003 (Database Engine error)
ms.assetid: 9e2cb199-f077-4d88-8117-1b7550afc696
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7e5a3b7c5b639b5ded1ea7dfd357a93375781b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916539"
---
# <a name="mssqlserver10003"></a>MSSQLSERVER_10003
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10003|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|HR_E_OUTOFMEMORY|  
|Testo del messaggio|Memoria insufficiente per il provider.|  
  
## <a name="explanation"></a>Spiegazione  
 La condizione di memoria di sistema insufficiente ha causato l'esaurimento della memoria del provider OLE DB.  
  
## <a name="user-action"></a>Azione dell'utente  
 Riavviare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se l'operazione non è risolutiva, riavviare il computer. Se il problema persiste, raccogliere gli eventi di traccia OLE DB mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e fornire questi dati al Servizio Supporto Tecnico Clienti Microsoft per il provider OLE DB.  
  
## <a name="see-also"></a>Vedere anche  
 [Modelli e autorizzazioni di SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
