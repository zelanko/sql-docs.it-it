---
title: Mapping SQL-DMO a SMO | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
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
|Oggetto BackupDevice|<xref:Microsoft.SqlServer.Management.Smo.BackupDevice>oggetti|  
|Oggetto BulkCopy e oggetto BulkCopy2|Rimosso e sostituito dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.|  
|Oggetto Category|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>. Sostituito dagli oggetti <xref:Microsoft.SqlServer.Management.Smo.Agent.AlertCategory>, <xref:Microsoft.SqlServer.Management.Smo.Agent.OperatorCategory>, <xref:Microsoft.SqlServer.Management.Smo.Agent.JobCategory>.|  
|Oggetto Check|<xref:Microsoft.SqlServer.Management.Smo.Check>oggetto|  
|Oggetto Column e oggetto Column2|<xref:Microsoft.SqlServer.Management.Smo.Column>oggetto.|  
|Oggetto Configuration|Oggetti <xref:Microsoft.SqlServer.Management.Smo.Configuration> e <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase>.|  
|Oggetto ConfigValue|<xref:Microsoft.SqlServer.Management.Smo.ConfigProperty>oggetto.|  
|Oggetto Database e oggetto Database2|<xref:Microsoft.SqlServer.Management.Smo.Database>oggetto.|  
|Oggetto DatabaseRole e oggetto DatabaseRole2|<xref:Microsoft.SqlServer.Management.Smo.DatabaseRole>oggetto.|  
|Oggetto DBFile|<xref:Microsoft.SqlServer.Management.Smo.DataFile>oggetto.|  
|Oggetto DBOption e oggetto DBOption2|Spostato nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions>.|  
|Oggetto Default e oggetto Default2|<xref:Microsoft.SqlServer.Management.Smo.Default>oggetto.|  
|Oggetto DistributionArticle e oggetto DistributionArticle2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto DistributionDatabase e oggetto DistributionDatabase2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto DistributionPublication e oggetto DistributionPublication2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto DistributionSubscription e oggetto DistributionSubscription2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto Distributor e oggetto Distributor2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto DRIDefault|Spostato nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.ScriptingOptions>.|  
|Oggetto FileGroup e oggetto FileGroup2|<xref:Microsoft.SqlServer.Management.Smo.FileGroup>oggetto.|  
|Oggetto FullTextCatalog e oggetto FullTextCatalog2|Oggetti <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> e <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex>.|  
|Oggetto Index e oggetto Index2|<xref:Microsoft.SqlServer.Management.Smo.Index>oggetto|  
|Oggetto IntegratedSecurity|Funzionalità spostata nell'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Common>.|  
|Oggetto Job|<xref:Microsoft.SqlServer.Management.Smo.Agent.Job>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto JobFilter|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobFilter>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto JobHistoryFilter|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobHistoryFilter>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto JobSchedule|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto JobServer e oggetto JobServer2|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto JobStep|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto Key|Oggetti <xref:Microsoft.SqlServer.Management.Smo.ForeignKey> e <xref:Microsoft.SqlServer.Management.Smo.Index>.|  
|Oggetto LinkedServer e oggetto LinkedServer2|<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>oggetto.|  
|Oggetto LinkedServerLogin|<xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin>oggetto.|  
|Oggetto LogFile|<xref:Microsoft.SqlServer.Management.Smo.LogFile>oggetto.|  
|Oggetto Login e oggetto Login2|<xref:Microsoft.SqlServer.Management.Smo.Login>oggetto.|  
|Oggetto MergeArticle e oggetto MergeArticle2|<xref:Microsoft.SqlServer.Replication.MergeArticle>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto MergeDynamicSnapshotJob|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto MergePublication e oggetto MergePublication2|<xref:Microsoft.SqlServer.Replication.MergePublication>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto MergePullSubscription e oggetto MergePullSubscription2|<xref:Microsoft.SqlServer.Replication.MergePullSubscription>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto MergeSubscription|<xref:Microsoft.SqlServer.Replication.MergeSubscription>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto MergeSubsetFilter|Spostato nello spazio dei nomi `N:Microsoft.SqlServer.Replication`.|  
|Oggetto NameList|Rimosso. Funzionalità alternativa nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Scripter>.|  
|Oggetto Operator|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto Permission e oggetto Permission2|Oggetti <xref:Microsoft.SqlServer.Management.Smo.ServerPermission>, <xref:Microsoft.SqlServer.Management.Smo.DatabasePermission>, <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> e <xref:Microsoft.SqlServer.Management.Smo.ObjectPermission>.|  
|Oggetto Property|`Property`oggetto.|  
|Oggetto Publisher e oggetto Publisher2|<xref:Microsoft.SqlServer.Replication.ReplicationServer>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto QueryResults e oggetto QueryResults2|Sostituito dall'oggetto di sistema <xref:System.Data.DataTable> o <xref:System.Data.DataSet>.|  
|Oggetto RegisteredServer|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto RegisteredSubscriber|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto Registry e oggetto Registry2|Rimosso.|  
|Oggetto RemoteLogin|<xref:Microsoft.SqlServer.Management.Common.ServerConnection>oggetto. Spostato nello spazio dei nomi comune.|  
|Oggetto RemoteServer e oggetto RemoteServer2|<xref:Microsoft.SqlServer.Management.Common.ServerConnection>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Common>.|  
|Oggetto Replication|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto ReplicationDatabase e oggetto ReplicationDatabase2|<xref:Microsoft.SqlServer.Replication.ReplicationDatabase>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto ReplicationSecurity|<xref:Microsoft.SqlServer.Management.Common.ServerConnection>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Common>.|  
|Oggetto ReplicationStoredProcedure e oggetto ReplicationStoredProcedure2|<xref:Microsoft.SqlServer.Replication.ReplicationStoredProcedure>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto ReplicationTable e oggetto ReplicationTable2|<xref:Microsoft.SqlServer.Replication.ReplicationTable>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto Restore e oggetto Restore2|Oggetti <xref:Microsoft.SqlServer.Management.Smo.Restore> e <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase>.|  
|Oggetto Rule e oggetto Rule2|<xref:Microsoft.SqlServer.Management.Smo.Rule>oggetto|  
|Oggetto Schedule|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto ServerGroup|Rimosso.|  
|Oggetto ServerRole|<xref:Microsoft.SqlServer.Management.Smo.ServerRole>oggetto.|  
|Oggetto SQLObjectList|<xref:Microsoft.SqlServer.Management.Smo.SqlSmoObject>matrice.|  
|Oggetto SQLServer e oggetto SQLServer2|<xref:Microsoft.SqlServer.Management.Smo.Server>oggetto.|  
|Oggetto StoredProcedure e oggetto StoredProcedure2|<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure>oggetti <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> e|  
|Oggetto Subscriber e oggetto Subscriber2|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto SystemDatatype e oggetto SystemDataType2|<xref:Microsoft.SqlServer.Management.Smo.DataType>oggetto.|  
|Oggetto Table e oggetto Table2|<xref:Microsoft.SqlServer.Management.Smo.Table>oggetto.|  
|Oggetto TargetServer|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto TargetServerGroup|Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Oggetto TransactionLog|Funzionalità spostata nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>.|  
|Oggetto TransArticle e oggetto TransArticle2|<xref:Microsoft.SqlServer.Replication.TransArticle>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Metodo Transfer e oggetto Transfer2|<xref:Microsoft.SqlServer.Management.Smo.Transfer>oggetto.|  
|Oggetto TransPublication e oggetto TransPublication2|<xref:Microsoft.SqlServer.Replication.TransPublication>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto TransPullSubscription e oggetto TransPullSubscription2|<xref:Microsoft.SqlServer.Replication.TransPullSubscription>oggetto. Spostato nello spazio dei nomi <xref:Microsoft.SqlServer.Replication>.|  
|Oggetto Trigger e oggetto Trigger2|<xref:Microsoft.SqlServer.Management.Smo.Trigger>oggetto.|  
|Oggetto User e oggetto User2|<xref:Microsoft.SqlServer.Management.Smo.User>oggetto.|  
|Oggetto UserDefinedDatatype e oggetto UserDefinedDataType2|<xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>oggetto.|  
|Oggetto UserDefinedFunction|Oggetti <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> e <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>.|  
|Oggetto View e oggetto View2|<xref:Microsoft.SqlServer.Management.Smo.View>oggetto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida alla programmazione di SQL Server Management Objects &#40;SMO&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
