---
title: Creare ed eseguire tracce utilizzando stored procedure Transact-SQL
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 80347417-338d-4bea-8885-91fae5181cfe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3d1c5a85072bec1fc304156268680c201ad2245e
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095647"
---
# <a name="create-and-run-traces-using-transact-sql-stored-procedures"></a>Creare ed eseguire tracce utilizzando stored procedure Transact-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Il processo di traccia eseguito tramite Traccia SQL varia a seconda che la traccia venga creata ed eseguita utilizzando Microsoft [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] o le stored procedure di sistema.  
  
 In alternativa a [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], è possibile utilizzare le stored procedure di sistema [!INCLUDE[tsql](../../includes/tsql-md.md)] per creare ed eseguire le tracce. Il processo di traccia eseguito tramite le stored procedure di sistema include i passaggi seguenti:  
  
1.  Creare una traccia usando **sp_trace_create**.  
  
2.  Aggiungere gli eventi con **sp_trace_setevent**.  
  
3.  (Facoltativo) Impostare un filtro con **sp_trace_setfilter**.  
  
4.  Avviare la traccia con **sp_trace_setstatus**.  
  
5.  Arrestare la traccia con **sp_trace_setstatus**.  
  
6.  Chiudere la traccia con **sp_trace_setstatus**.  
  
    > [!NOTE]  
    >  Mediante le stored procedure di sistema di [!INCLUDE[tsql](../../includes/tsql-md.md)] viene creata una traccia sul lato server, evitando in tal modo la perdita di eventi a condizione che lo spazio su disco sia sufficiente e non si verifichino errori di scrittura. Se il disco si riempie o si verifica un errore, l'esecuzione dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] continua ma la traccia viene arrestata. Se l'opzione **c2 audit mode** è impostata e si verifica un errore di scrittura, la traccia viene arrestata e l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene chiusa. Per altre informazioni sull'impostazione **c2 audit mode** , vedere [Opzione di configurazione del server c2 audit mode](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Ottimizzare l'utilizzo di Traccia SQL](../../relational-databases/sql-trace/optimize-sql-trace.md)|Contiene informazioni sulle strategie per ridurre gli effetti della traccia sulle prestazioni del sistema.|  
|[Filtrare una traccia](../../relational-databases/sql-trace/filter-a-trace.md)|Contiene informazioni sull'utilizzo di filtri per la traccia.|  
|[Limitare le dimensioni di file di traccia e tabelle](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md)|Contiene informazioni sulla procedura per limitare le dimensioni di file e tabelle in cui sono registrati i dati di traccia. Si noti che è possibile registrare informazioni di traccia nelle tabelle solo tramite [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .|  
|[Pianificare tracce](../../relational-databases/sql-trace/schedule-traces.md)|Contiene informazioni sull'impostazione dell'ora di inizio e di fine della traccia.|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
