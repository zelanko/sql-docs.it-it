---
title: Creare ed eseguire tracce usando stored procedure Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 80347417-338d-4bea-8885-91fae5181cfe
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7922638ed06f52740a3c34f6e66ff72dbb5bbd98
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62714808"
---
# <a name="create-and-run-traces-using-transact-sql-stored-procedures"></a>Creare ed eseguire tracce utilizzando stored procedure Transact-SQL
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
  
## <a name="in-this-section"></a>In questa sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Ottimizzare l'utilizzo di Traccia SQL](sql-trace.md)|Contiene informazioni sulle strategie per ridurre gli effetti della traccia sulle prestazioni del sistema.|  
|[Filtrare una traccia](filter-a-trace.md)|Contiene informazioni sull'utilizzo di filtri per la traccia.|  
|[Limitare le dimensioni di file di traccia e tabelle](limit-trace-file-and-table-sizes.md)|Contiene informazioni sulla procedura per limitare le dimensioni di file e tabelle in cui sono registrati i dati di traccia. Si noti che è possibile registrare informazioni di traccia nelle tabelle solo tramite [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .|  
|[Pianificare tracce](schedule-traces.md)|Contiene informazioni sull'impostazione dell'ora di inizio e di fine della traccia.|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)  
  
  
