---
title: Visualizzare le impostazioni NodeWeight per il quorum del cluster | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: b845e73a-bb01-4de2-aac2-8ac12abebc95
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6d3b98adece53952f72afc999f950c0388b65c96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904918"
---
# <a name="view-cluster-quorum-nodeweight-settings"></a>Visualizzare le impostazioni NodeWeight per il quorum del cluster
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene illustrato come visualizzare le impostazioni NodeWeight per ogni nodo membro di un cluster WSFC (Windows Server Failover Clustering). Le impostazioni NodeWeight vengono utilizzate durante la votazione quorum per supportare scenari di ripristino di emergenza e multi-subnet per istanze del cluster di failover di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Prima di iniziare:**  [Prerequisiti](#Prerequisites), [Sicurezza](#Security)  
  
-   **Per visualizzare le impostazioni NodeWeight per il quorum:** [Uso di Transact-SQL](#TsqlProcedure), [Uso di Powershell](#PowerShellProcedure), [Uso di Cluster.exe](#CommandPromptProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Questa caratteristica è supportata solo in [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] o versioni successive.  
  
> [!IMPORTANT]  
>  Per utilizzare le impostazioni NodeWeight, è necessario applicare l'aggiornamento rapido seguente a tutti i server del cluster WSFC:  
>   
>  [KB2494036](https://support.microsoft.com/kb/2494036): è disponibile un aggiornamento rapido per configurare un nodo del cluster che non presenta voti quorum in [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e in [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
> [!TIP]  
>  Se questo aggiornamento rapido non viene installato, gli esempi in questo argomento restituiranno valori vuoti o NULL per NodeWeight.  
  
###  <a name="Security"></a> Sicurezza  
 L'utente deve disporre di un account di dominio che sia membro del gruppo Administrators locale su ogni nodo del cluster WSFC.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
##### <a name="to-view-nodeweight-settings"></a>Per visualizzare le impostazioni NodeWeight  
  
1.  Connettersi a qualsiasi istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel cluster.  
  
2.  Eseguire una query sulla vista [sys].[dm_hadr_cluster_members].  
  
### <a name="example-transact-sql"></a>Esempio (Transact-SQL)  
 Nell'esempio seguente viene eseguita una query su una vista di sistema affinché vengano restituiti valori per tutti i nodi del cluster dell'istanza.  
  
```sql  
SELECT  member_name, member_state_desc, number_of_quorum_votes  
 FROM   sys.dm_hadr_cluster_members;  
```  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di Powershell  
  
##### <a name="to-view-nodeweight-settings"></a>Per visualizzare le impostazioni NodeWeight  
  
1.  Avviare Windows PowerShell con privilegi elevati tramite **Esegui come amministratore**.  
  
2.  Importare il modulo `FailoverClusters` per abilitare i commandlet del cluster.  
  
3.  Utilizzare l'oggetto `Get-ClusterNode` per restituire una raccolta di oggetti del nodo del cluster.  
  
4.  Restituire le proprietà del nodo del cluster in un formato leggibile.  
  
### <a name="example-powershell"></a>Esempio (Powershell)  
 Nell'esempio seguente vengono restituite alcune delle proprietà del nodo per il cluster denominato "Cluster001".  
  
```powershell  
Import-Module FailoverClusters  
  
$cluster = "Cluster001"  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> Utilizzo di Cluster.exe  
  
> [!NOTE]  
>  L'utilità cluster.exe è deprecata nella versione [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] .  Utilizzare PowerShell con il clustering di failover per lo sviluppo futuro.  L'utilità cluster.exe verrà rimossa nella versione successiva di Windows Server. Per altre informazioni, vedere [Mapping Cluster.exe Commands to Windows PowerShell Cmdlets for Failover Clusters](https://technet.microsoft.com/library/ee619744\(WS.10\).aspx)(Mapping di comandi Cluster.exe a cmdlet di Windows PowerShell per i cluster di failover).  
  
##### <a name="to-view-nodeweight-settings"></a>Per visualizzare le impostazioni NodeWeight  
  
1.  Avviare un prompt dei comandi con privilegi elevati tramite **Esegui come amministratore**.  
  
2.  Utilizzare **cluster.exe** per restituire lo stato del nodo e i valori NodeWeight  
  
### <a name="example-clusterexe"></a>Esempio (Cluster.exe)  
 Nell'esempio seguente vengono restituite alcune delle proprietà del nodo per il cluster denominato "Cluster001".  
  
```ms-dos  
cluster.exe Cluster001 node /status /properties  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità quorum WSFC e configurazione del voto &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [Configurare le impostazioni NodeWeight per il quorum del cluster](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)   
 [Cmdlet del cluster di failover in Windows PowerShell elencati per attività](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
