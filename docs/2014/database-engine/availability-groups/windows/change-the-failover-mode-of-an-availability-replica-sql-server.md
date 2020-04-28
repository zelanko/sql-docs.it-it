---
title: Modificare la modalità di failover di una replica di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover modes [SQL Server]
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], failover modes
- Availability Groups [SQL Server], configuring
ms.assetid: 619a826f-8e65-48eb-8c34-39497d238279
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6750456d708d68e57aadd4b1139f6e108a93b9ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783022"
---
# <a name="change-the-failover-mode-of-an-availability-replica-sql-server"></a>Modificare la modalità di failover di una replica di disponibilità (SQL Server)
  In questo argomento viene illustrato come modificare la modalità di failover di una replica di disponibilità in un gruppo di disponibilità AlwaysOn in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell. La modalità di failover è una proprietà della replica che determina la modalità di failover per le repliche eseguite nella modalità di disponibilità con commit sincrono. Per altre informazioni, vedere [Failover e modalità di failover &#40;gruppi di disponibilità AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md) e [Modalità di disponibilità &#40;gruppi di disponibilità AlwaysOn&#41;](availability-modes-always-on-availability-groups.md).  
  

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites-and-restrictions"></a><a name="Prerequisites"></a> Prerequisiti e restrizioni  
  
-   Questa attività può essere eseguita solo sulle repliche primarie. È necessario essere connessi all'istanza del server che ospita la replica primaria.  
  
-   Le istanze del cluster di failover di SQL Server non supportano il failover automatico da gruppi di disponibilità, pertanto le replica di disponibilità ospitate da un'istanza del cluster di failover possono essere configurate solo per il failover manuale.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per modificare la modalità di failover di una replica di disponibilità**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica primaria ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Fare clic sul gruppo di disponibilità di cui si desidera modificare la replica.  
  
4.  Fare clic con il pulsante destro del mouse sulla replica e scegliere **Proprietà**.  
  
5.  Nella finestra di dialogo **Proprietà replica di disponibilità** utilizzare l'elenco a discesa **Modalità di failover** per modificare la modalità di failover di questa replica.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per modificare la modalità di failover di una replica di disponibilità**  
  
1.  Connettersi all'istanza del server che ospita la replica primaria.  
  
2.  Utilizzare l'istruzione [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) , come indicato di seguito:  
  
     ALTER AVAILABILITY GROUP *nome_gruppo* MODIFY REPLICA ON '*nome_server*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     }  )  
  
     where  
  
    -   *nome_gruppo* è il nome del gruppo di disponibilità.  
  
    -   {'*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]'}  
  
         Specifica l'indirizzo dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che ospita la replica di disponibilità da modificare. I componenti di questo indirizzo sono i seguenti:  
  
         *_sistema*  
         Nome NetBIOS del computer in cui risiede un'istanza autonoma del server.  
  
         *nome_rete_FCI*  
         Nome di rete utilizzato per accedere a un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui un'istanza del server di destinazione è un partner di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
         *instance_name*  
         Nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che ospita la replica di disponibilità di destinazione. Per un'istanza del server predefinita, *nome_istanza* è facoltativo.  
  
     Per altre informazioni su questi parametri, vedere [ALTER AVAILABILITY GROUP &#40; Transact-SQL &#41;](/sql/t-sql/statements/alter-availability-group-transact-sql).  
  
     L'esempio seguente, relativo alla replica primaria del gruppo di disponibilità *MyAG* , mostra come impostare la modalità di failover automatico sulla replica di disponibilità situata in un'istanza del server predefinita in un computer denominato *COMPUTER01*.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG MODIFY REPLICA ON 'COMPUTER01' WITH  
       (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Utilizzo di PowerShell  

### <a name="to-change-the-failover-mode-of-an-availability-replica"></a>Per modificare la modalità di failover di una replica di disponibilità
  
1.  Spostarsi nella directory (`cd`) dell'istanza del server che ospita la replica primaria.  
  
2.  Utilizzare il cmdlet `Set-SqlAvailabilityReplica` con il parametro `FailoverMode`. Quando si imposta una replica su failover automatico, potrebbe essere necessario utilizzare il parametro `AvailabilityMode` per impostare la replica su modalità di disponibilità con commit sincrono.  
  
     Ad esempio, con il comando seguente si modifica la replica `MyReplica` nel gruppo di disponibilità `MyAg` in modo da utilizzare la modalità di disponibilità con commit asincrono e supportare il failover automatico.  
  
    ```powershell
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `
     -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\Replicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
Per configurare e usare il provider di SQL Server PowerShell, vedere [provider di SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md).
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
 [Modalità di disponibilità &#40;Gruppi di disponibilità AlwaysOn&#41;](availability-modes-always-on-availability-groups.md)   
 [Failover e modalità di failover &#40;Gruppi di disponibilità AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md) 
