---
title: Configurare le impostazioni NodeWeight per il quorum del cluster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: cb3fd9a6-39a2-4e9c-9157-619bf3db9951
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dfc31fa968952db56a64f93b180c2b88ec685725
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797614"
---
# <a name="configure-cluster-quorum-nodeweight-settings"></a>Configurare le impostazioni NodeWeight per il quorum del cluster
  In questo argomento viene illustrato come configurare le impostazioni NodeWeight per un nodo membro di un cluster WSFC (Windows Server Failover Clustering). Le impostazioni NodeWeight vengono utilizzate durante la votazione quorum per supportare scenari di ripristino di emergenza e multi-subnet per istanze del cluster di failover di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Before you start:**  [Prerequisites](#Prerequisites), [Security](#Security)  
  
-   **Per visualizzare le impostazioni NodeWeight del quorum utilizzando:** [Utilizzo di Powershell](#PowerShellProcedure), [Utilizzo di Cluster.exe](#CommandPromptProcedure)  
  
-   [Contenuto correlato](#RelatedContent)  
  
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
  
##  <a name="PowerShellProcedure"></a> Utilizzo di Powershell  
  
### <a name="to-configure-nodeweight-settings"></a>Per configurare le impostazioni NodeWeight
  
1.  Avviare Windows PowerShell con privilegi elevati tramite **Esegui come amministratore**.  
  
2.  Importare il modulo `FailoverClusters` per abilitare i commandlet del cluster.  
  
3.  Utilizzare l'oggetto `Get-ClusterNode` per impostare la proprietà `NodeWeight` per ogni nodo nel cluster.  
  
4.  Restituire le proprietà del nodo del cluster in un formato leggibile.  
  
 Nell'esempio seguente viene modificata l'impostazione NodeWeight per rimuovere il voto quorum per il nodo "AlwaysOnSrv1" e quindi vengono restituite le impostazioni per tutti i nodi del cluster.
  
```powershell  
Import-Module FailoverClusters  
  
$node = "AlwaysOnSrv1"  
(Get-ClusterNode $node).NodeWeight = 0  
  
$cluster = (Get-ClusterNode $node).Cluster  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> Utilizzo di Cluster.exe  
  
> [!NOTE]  
>  L'utilità cluster.exe è deprecata nella versione [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] .  Utilizzare PowerShell con il clustering di failover per lo sviluppo futuro.  L'utilità cluster.exe verrà rimossa nella versione successiva di Windows Server. Per altre informazioni, vedere [Mapping Cluster.exe Commands to Windows PowerShell Cmdlets for Failover Clusters](https://technet.microsoft.com/library/ee619744\(WS.10\).aspx)(Mapping di comandi Cluster.exe a cmdlet di Windows PowerShell per i cluster di failover).  
  
### <a name="to-configure-nodeweight-settings"></a>Per configurare le impostazioni NodeWeight
  
1.  Avviare un prompt dei comandi con privilegi elevati tramite **Esegui come amministratore**.  
  
2.  Utilizzare **cluster.exe** per impostare valori `NodeWeight` .  

 Nell'esempio seguente viene modificato il valore NodeWeight per rimuovere il voto quorum del nodo "AlwaysOnSrv1" nel cluster "Cluster001".  
  
```cmd
cluster.exe Cluster001 node AlwaysOnSrv1 /prop NodeWeight=0  
```  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   [Visualizzare eventi e registri per un cluster di failover](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Pagina relativa al cluster di failover Get-ClusterLog](https://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità quorum WSFC e configurazione del voto &#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [Visualizzare le impostazioni NodeWeight per il quorum del cluster](view-cluster-quorum-nodeweight-settings.md)   
 [Cmdlet del cluster di failover in Windows PowerShell elencati per attività](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
