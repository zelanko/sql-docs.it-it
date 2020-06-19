---
title: MSSQLSERVER_1462 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8b9146958577fce9ff7df223fd0d71a7b6c8b11c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969572"
---
# <a name="mssqlserver_1462"></a>MSSQLSERVER_1462
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1462|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBM_DISABLED_DUE_TO_FAILED_REDO|  
|Testo del messaggio|Mirroring del database disabilitato a causa di un'operazione di rollforward non riuscita. Impossibile riprendere.|  
  
## <a name="explanation"></a>Spiegazione  
 Il mirroring del database non è riuscito a eseguire un'operazione di rollforward di un record di log nel mirror.  
  
### <a name="possible-causes"></a>Possibili cause  
 La causa più probabile è che un'operazione di aggiunta file è stata completata nel database principale ma non è stata eseguita nel database mirror perché i nomi file o le strutture di directory del server principale e del server mirror sono diverse.  
  
## <a name="user-action"></a>Azione dell'utente  
 Esaminare il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per individuare la causa dell'errore. Provare a eliminare la causa del problema e a riprendere il mirroring nel database.  
  
## <a name="see-also"></a>Vedere anche  
 [Risolvere i problemi relativi alla configurazione del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
