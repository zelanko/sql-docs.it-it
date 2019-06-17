---
title: Mapping SQL-DMO, SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 590f5396-98d5-485e-9b41-728c6ed7cb9d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a6273032f88807291bfc7024f1abcdbd1440073
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62780681"
---
# <a name="sql-dmo-mapping-to-smo"></a>Mapping di SQL-DMO agli oggetti SMO
  SQL Distributed Management Objects (SQL-DMO) non è più incluso in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. È necessario convertire le applicazioni SQL-DMO per utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO). Il modello a oggetti SMO è analogo a SQL-DMO e pertanto la maggior parte degli oggetti SQL-DMO esegue il mapping a un oggetto con lo stesso nome in SMO. Nel passaggio a SMO alcuni oggetti SQL-DMO sono stati tuttavia modificati o eliminati. In questa tabella vengono elencate le operazioni consigliate da eseguire per gli oggetti SQL-DMO non convertiti direttamente in SMO.  
  
|Oggetto SQL-DMO|Azione in SMO|  
|---------------------|-------------------|  
|Oggetto View2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto AlertSystem|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto Application|Rimosso.|  
|Oggetto Backup e oggetto Backup2|Oggetti <xref:Microsoft.SqlServer.Management.Smo.Backup> e <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase>.|  
|Oggetto BackupDevice|Oggetti <xref:Microsoft.SqlServer.Management.Smo.BackupDevice>|  
|Oggetto BulkCopy e oggetto BulkCopy2|Rimosso e sostituito dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.|  
|Oggetto Category|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>. Sostituito dagli oggetti <xref:Microsoft.SqlServer.Management.Smo.Agent.AlertCategory>, <xref:Microsoft.SqlServer.Management.Smo.Agent.OperatorCategory>, <xref:Microsoft.SqlServer.Management.Smo.Agent.JobCategory>.|  
|Oggetto Check|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Check>|  
|Oggetto Column e oggetto Column2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Column>.|  
|Oggetto Configuration|Oggetti <xref:Microsoft.SqlServer.Management.Smo.Configuration> e <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase>.|  
|Oggetto ConfigValue|Oggetto <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty>.|  
|Oggetto Database e oggetto Database2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>.|  
|Oggetto DatabaseRole e oggetto DatabaseRole2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.DatabaseRole>.|  
|Oggetto DBFile|Oggetto <xref:Microsoft.SqlServer.Management.Smo.DataFile>.|  
|Oggetto DBOption e oggetto DBOption2|Spostato nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions>.|  
|Oggetto Default e oggetto Default2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Default>.|  
|Oggetto DistributionArticle e oggetto DistributionArticle2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto DistributionDatabase e oggetto DistributionDatabase2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto DistributionPublication e oggetto DistributionPublication2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto DistributionSubscription e oggetto DistributionSubscription2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto Distributor e oggetto Distributor2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto DRIDefault|Spostato nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.ScriptingOptions>.|  
|Oggetto FileGroup e oggetto FileGroup2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.FileGroup>.|  
|Oggetto FullTextCatalog e oggetto FullTextCatalog2|Oggetti <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> e <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex>.|  
|Oggetto Index e oggetto Index2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Index>|  
|Oggetto IntegratedSecurity|Funzionalità spostata nell'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Common>.|  
|Oggetto Job|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Agent.Job>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto JobFilter|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobFilter>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto JobHistoryFilter|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobHistoryFilter>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto JobSchedule|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto JobServer e oggetto JobServer2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto JobStep|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto Key|Oggetti <xref:Microsoft.SqlServer.Management.Smo.ForeignKey> e <xref:Microsoft.SqlServer.Management.Smo.Index>.|  
|Oggetto LinkedServer e oggetto LinkedServer2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>.|  
|Oggetto LinkedServerLogin|Oggetto <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin>.|  
|Oggetto LogFile|Oggetto <xref:Microsoft.SqlServer.Management.Smo.LogFile>.|  
|Oggetto Login e oggetto Login2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Login>.|  
|Oggetto MergeArticle e oggetto MergeArticle2|Oggetto <xref:Microsoft.SqlServer.Replication.MergeArticle>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto MergeDynamicSnapshotJob|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto MergePublication e oggetto MergePublication2|Oggetto <xref:Microsoft.SqlServer.Replication.MergePublication>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto MergePullSubscription e oggetto MergePullSubscription2|Oggetto <xref:Microsoft.SqlServer.Replication.MergePullSubscription>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto MergeSubscription|Oggetto <xref:Microsoft.SqlServer.Replication.MergeSubscription>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto MergeSubsetFilter|Spostato nello spazio dei nomi `N:Microsoft.SqlServer.Replication`.|  
|Oggetto NameList|Rimosso. Funzionalità alternativa nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Scripter>.|  
|Oggetto Operator|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto Permission e oggetto Permission2|Oggetti <xref:Microsoft.SqlServer.Management.Smo.ServerPermission>, <xref:Microsoft.SqlServer.Management.Smo.DatabasePermission>, <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> e <xref:Microsoft.SqlServer.Management.Smo.ObjectPermission>.|  
|Oggetto Property|Oggetto `Property`.|  
|Oggetto Publisher e oggetto Publisher2|Oggetto <xref:Microsoft.SqlServer.Replication.ReplicationServer>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto QueryResults e oggetto QueryResults2|Sostituito dall'oggetto di sistema <xref:System.Data.DataTable> o <xref:System.Data.DataSet>.|  
|Oggetto RegisteredServer|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto RegisteredSubscriber|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto Registry e oggetto Registry2|Rimosso.|  
|Oggetto RemoteLogin|Oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Spostato nello spazio dei nomi comune.|  
|Oggetto RemoteServer e oggetto RemoteServer2|Oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Common>.|  
|Oggetto Replication|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto ReplicationDatabase e oggetto ReplicationDatabase2|Oggetto <xref:Microsoft.SqlServer.Replication.ReplicationDatabase>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto ReplicationSecurity|Oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Common>.|  
|Oggetto ReplicationStoredProcedure e oggetto ReplicationStoredProcedure2|Oggetto <xref:Microsoft.SqlServer.Replication.ReplicationStoredProcedure>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto ReplicationTable e oggetto ReplicationTable2|Oggetto <xref:Microsoft.SqlServer.Replication.ReplicationTable>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto Restore e oggetto Restore2|Oggetti <xref:Microsoft.SqlServer.Management.Smo.Restore> e <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase>.|  
|Oggetto Rule e oggetto Rule2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Rule>|  
|Oggetto Schedule|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto ServerGroup|Rimosso.|  
|Oggetto ServerRole|Oggetto <xref:Microsoft.SqlServer.Management.Smo.ServerRole>.|  
|Oggetto SQLObjectList|Matrice <xref:Microsoft.SqlServer.Management.Smo.SqlSmoObject>.|  
|Oggetto SQLServer e oggetto SQLServer2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Server>.|  
|Oggetto StoredProcedure e oggetto StoredProcedure2|Oggetti <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> e <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>.|  
|Oggetto Subscriber e oggetto Subscriber2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto SystemDatatype e oggetto SystemDataType2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.DataType>.|  
|Oggetto Table e oggetto Table2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Table>.|  
|Oggetto TargetServer|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto TargetServerGroup|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto TransactionLog|Funzionalità spostata nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>.|  
|Oggetto TransArticle e oggetto TransArticle2|Oggetto <xref:Microsoft.SqlServer.Replication.TransArticle>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Metodo Transfer e oggetto Transfer2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.|  
|Oggetto TransPublication e oggetto TransPublication2|Oggetto <xref:Microsoft.SqlServer.Replication.TransPublication>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto TransPullSubscription e oggetto TransPullSubscription2|Oggetto <xref:Microsoft.SqlServer.Replication.TransPullSubscription>. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto Trigger e oggetto Trigger2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.Trigger>.|  
|Oggetto User e oggetto User2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.User>.|  
|Oggetto UserDefinedDatatype e oggetto UserDefinedDataType2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>.|  
|Oggetto UserDefinedFunction|Oggetti <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> e <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>.|  
|Oggetto View e oggetto View2|Oggetto <xref:Microsoft.SqlServer.Management.Smo.View>.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida alla programmazione di SQL Server Management Objects &#40;SMO&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
