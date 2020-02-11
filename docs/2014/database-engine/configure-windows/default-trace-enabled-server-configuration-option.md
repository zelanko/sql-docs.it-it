---
title: Opzione di configurazione server default trace enabled | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], traces
- traces [SQL Server], logs
- default trace enabled option
ms.assetid: 1322d668-44f4-469e-8fd6-e0d02a81c8f2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d5e85a3685804fa834c9a92887a46c72b7cb69a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62811315"
---
# <a name="default-trace-enabled-server-configuration-option"></a>Opzione di configurazione server default trace enabled
  L'opzione **Default Trace Enabled** consente di abilitare o disabilitare i file di log della traccia predefinita. Tramite la funzionalità di traccia predefinita è possibile ottenere un log completo e persistente delle attività e delle modifiche correlate principalmente alle opzioni di configurazione.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] In alternativa, usare Eventi estesi.  
  
## <a name="purpose"></a>Scopo  
 La traccia predefinita rappresenta un supporto alla risoluzione dei problemi per gli amministratori di database, poiché consente di disporre dei dati del log necessari per diagnosticare i problemi non appena si verificano.  
  
## <a name="viewing"></a>Visualizzazione  
 È possibile aprire ed esaminare i log di traccia predefiniti utilizzando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] oppure eseguire query su tali log mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzando la funzione di sistema `fn_trace_gettable` . [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] è in grado di aprire i file di log delle tracce predefinite come i normali file di output delle tracce. Per impostazione predefinita, il log di traccia predefinito viene archiviato nella directory `\MSSQL\LOG` tramite un file di traccia consecutivo. Il nome file di base del log di traccia predefinito è `log.trc`. In un'installazione tipica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la traccia predefinita è attivata e viene pertanto denominata TraceID 1. Se attivato dopo l'installazione e la creazione di altre tracce, TraceID può essere associato a un numero maggiore.  
  
 Per altre informazioni sull'uso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler per la visualizzazione di questo file di traccia, vedere [Aprire un file di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md).  
  
### <a name="example"></a>Esempio:  
 L'istruzione seguente consente di aprire il log di traccia predefinito nel percorso predefinito:  
  
```  
SELECT *   
FROM fn_trace_gettable  
('C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\LOG\log.trc', default);  
GO  
  
```  
  
## <a name="configuring"></a>Configurazione  
 Se impostata su 1, l'opzione **Default Trace Enabled** abilita la **traccia predefinita**. L'impostazione predefinita per questa opzione è 1 (ON). Se si imposta il valore 0 si disabilita la traccia.  
  
 L'opzione **Default Trace Enabled** è un'opzione avanzata. Se si usa la stored procedure di sistema **sp_configure** per modificare l'impostazione, è possibile modificare l'opzione **Default Trace Enabled** solo quando il valore di **Show Advanced Options** è impostato su 1. L'impostazione diventa effettiva immediatamente e non richiede il riavvio del server.  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
