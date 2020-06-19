---
title: MSSQLSERVER_1458 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6a62738b8d4205e269e51d45c98cfd114c3451fe
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969581"
---
# <a name="mssqlserver_1458"></a>MSSQLSERVER_1458
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1458|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBM_FAILREDO_ON_PRIMARY|  
|Testo del messaggio|La copia principale del database '%.*ls' ha rilevato l'errore % d, con stato% d e gravità% d. Il mirroring del database è stato sospeso. Risolvere il problema e riprendere il mirroring.|  
  
## <a name="explanation"></a>Spiegazione  
 Il messaggio indica che il database principale ha rilevato un errore che ha causato la sospensione del mirroring del database.  
  
## <a name="user-action"></a>Azione dell'utente  
 Nella maggior parte dei casi per la risoluzione di questo errore non è richiesto l'intervento dell'utente. Se il problema persiste, è in genere sufficiente riavviare l'istanza del database o del server per correggerlo. Per ulteriori informazioni, ricercare nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di ogni partner l'errore associato che ha preceduto la visualizzazione del messaggio.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
