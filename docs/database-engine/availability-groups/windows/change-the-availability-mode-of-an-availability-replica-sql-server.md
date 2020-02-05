---
title: Modificare la modalità di disponibilità di una replica per un gruppo di disponibilità
description: Descrive come modificare la modalità di disponibilità di una replica all'interno di un gruppo di disponibilità Always On usando Transact-SQL (T-SQL), PowerShell o SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], availability modes
ms.assetid: c4da8f25-fb1b-45a4-8bf2-195df6df634c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b1a3b5d1dfdf3a5e8556058cee750a4e2e08476a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74822447"
---
# <a name="change-availability-mode-of-a-replica-within-an-always-on-availability-group"></a>Modificare la modalità di disponibilità di una replica in un gruppo di disponibilità Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questo argomento illustra come modificare la modalità di disponibilità di una replica di disponibilità in un gruppo di disponibilità Always On in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell. La modalità di disponibilità è una proprietà della replica che determina se il commit della replica viene eseguito in modo asincrono o sincrono. La*modalità con commit asincrono* ottimizza le prestazioni a discapito della disponibilità elevata e supporta solo il failover manuale forzato (con possibile perdita di dati), generalmente denominato *failover forzato*. La*modalità con commit sincrono* privilegia la disponibilità elevata rispetto alle prestazioni e, una volta sincronizzata la replica secondaria, supporta il failover manuale e, facoltativamente, quello automatico.  
    
##  <a name="Prerequisites"></a> Prerequisiti  
  
È necessario essere connessi all'istanza del server che ospita la replica primaria.  
  

##  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 **Per modificare la modalità di disponibilità di un gruppo di disponibilità**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica primaria ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità**.  
  
3.  Fare clic sul gruppo di disponibilità di cui si desidera modificare la replica.  
  
4.  Fare clic con il pulsante destro del mouse sulla replica e scegliere **Proprietà**.  
  
5.  Nella finestra di dialogo **Proprietà replica di disponibilità** utilizzare l'elenco a discesa **Modalità di disponibilità** per modificare la modalità di disponibilità di questa replica.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
 **Per modificare la modalità di disponibilità di un gruppo di disponibilità**  
  
1.  Connettersi all'istanza del server che ospita la replica primaria.  
  
2.  Utilizzare l'istruzione [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) , come indicato di seguito:  
  
     ALTER AVAILABILITY GROUP *nome_gruppo* MODIFY REPLICA ON '*nome_server*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     } )  
  
     dove *group_name* è il nome del gruppo di disponibilità e *server_name* è il nome dell'istanza del server che ospita la replica da modificare.  
  
    > [!NOTE]  
    >  FAILOVER_MODE = AUTOMATIC è supportata solo se si specifica anche AVAILABILITY_MODE = SYNCHRONOUS_COMMIT.  
  
     Nell'esempio seguente, relativo alla replica primaria del gruppo di disponibilità `AccountsAG` , vengono impostate le modalità di disponibilità e di failover sul commit sincrono e il failover automatico, rispettivamente, per la replica ospitata dall'istanza del server `INSTANCE09` .  
  
    ```  
  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="PowerShellProcedure"></a> Con PowerShell  
 **Per modificare la modalità di disponibilità di un gruppo di disponibilità**  
  
1.  Cambiare la directory (**cd**) impostandola sull'istanza del server che ospita la replica primaria.  
  
2.  Usare il cmdlet **Set-SqlAvailabilityReplica** con il parametro **AvailabilityMode** e, facoltativamente, il parametro **FailoverMode** .  
  
     Ad esempio, con il comando seguente si modifica la replica `MyReplica` nel gruppo di disponibilità `MyAg` in modo da utilizzare la modalità di disponibilità con commit asincrono e supportare il failover automatico.  
  
    ```  
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, usare il cmdlet **Get-Help** nell'ambiente PowerShell di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Modalità di disponibilità &#40;gruppi di disponibilità AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Failover e modalità di failover &#40;gruppi di disponibilità AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)  
  
  
