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
ms.openlocfilehash: fd4f3499dcf24435c594d3f01adce97f979f817d
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553856"
---
# <a name="mssqlserver_1458"></a>MSSQLSERVER_1458
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
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
  
  
