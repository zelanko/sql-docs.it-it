---
title: Creare un join di una replica secondaria a un gruppo di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.joinreplica.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
ms.assetid: e5bd2489-097a-490e-8ea1-34fe48378ad1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 39ee8bfc079445e177aa9b175019ae385b9f9f36
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797664"
---
# <a name="join-a-secondary-replica-to-an-availability-group-sql-server"></a>Creare un join di una replica secondaria a un gruppo di disponibilità (SQL Server)
  In questo argomento si illustra come creare un join di una replica secondaria a un gruppo di disponibilità AlwaysOn utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Dopo l'aggiunta di una replica secondaria a un gruppo di disponibilità AlwaysOn, è necessario creare un join della replica secondaria al gruppo di disponibilità. L'operazione di join della replica deve essere eseguita nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui viene ospitata la replica secondaria.  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti](#Prerequisites)  
  
     [Security](#Security)  
  
-   **Per preparare un database secondario tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Completamento:** [Configurare i database secondari](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisites  
  
-   La replica primaria del gruppo di disponibilità deve essere attualmente online.  
  
-   È necessario essere connessi all'istanza del server che ospita una replica secondaria di cui non sia ancora stato creato un join al gruppo di disponibilità.  
  
-   L'istanza del server locale deve essere in grado di connettersi all'endpoint del mirroring del database dell'istanza del server che ospita la replica primaria.  
  
> [!IMPORTANT]  
>  Se nessuno dei prerequisiti viene soddisfatto, l'operazione di join non viene completata. Al termine di un tentativo di join errato, potrebbe essere necessario connettersi all'istanza del server in cui è ospitata la replica primaria per rimuovere e aggiungere nuovamente la replica secondaria, prima di poter creare un join al gruppo di disponibilità. Per altre informazioni, vedere [Rimuovere una replica secondaria da un gruppo di disponibilità &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md) e [Aggiungere una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> Permissions  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per creare un join di una replica di disponibilità a un gruppo di disponibilità**  
  
1.  In Esplora oggetti connettersi all'istanza del server in cui viene ospitata la replica secondaria e fare clic sul nome del server per espandere il relativo albero.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Selezionare il gruppo di disponibilità della replica secondaria a cui si è connessi.  
  
4.  Fare clic con il pulsante destro del mouse sulla replica secondaria e scegliere **Crea un join del gruppo di disponibilità**.  
  
5.  In questo modo verrà aperta la finestra di dialogo **Creare un join della replica al gruppo di disponibilità** .  
  
6.  Per creare un join della replica secondaria al gruppo di disponibilità, fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 **Per creare un join di una replica di disponibilità a un gruppo di disponibilità**  
  
1.  Connettersi all'istanza del server che ospita la replica secondaria.  
  
2.  Utilizzare l'istruzione [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) , come indicato di seguito:  
  
     ALTER AVAILABILITY GROUP *nome_gruppo* JOIN  
  
     dove *nome_gruppo* è il nome del gruppo di disponibilità.  
  
     Nell'esempio seguente viene creato un join della replica secondaria al gruppo di disponibilità `MyAG` .  
  
    ```sql
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    ```  
  
    > [!NOTE]  
    >  Per un esempio di questa istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] impiegata in un contesto, vedere [Creare un gruppo di disponibilità &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md).  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Per creare un join di una replica di disponibilità a un gruppo di disponibilità**  
  
 Nel provider PowerShell per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
1.  Impostare la directory (`cd`) sull'istanza del server in cui viene ospitata la replica secondaria.  
  
2.  Creare un join della replica secondaria al gruppo di disponibilità eseguendo il cmdlet **Join-SqlAvailabilityGroup** con il nome del gruppo di disponibilità.  
  
     Ad esempio, tramite il comando seguente è possibile creare un join di una replica secondaria ospitata dall'istanza del server presente nel percorso specificato al gruppo di disponibilità denominato `MyAg`.  Questa istanza del server deve ospitare una replica secondaria in questo gruppo di disponibilità.  
  
    ```powershell
    Join-SqlAvailabilityGroup -Path SQLSERVER:\SQL\SecondaryServer\InstanceName -Name 'MyAg'  
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Completamento: Configurare i database secondari  
 Per ogni database nel gruppo di disponibilità, è necessario un database secondario nell'istanza del server in cui viene ospitata la replica secondaria. È possibile configurare i database secondari prima o dopo la creazione di un join di una replica secondaria a un gruppo di disponibilità, come indicato di seguito:  
  
1.  Ripristinare i backup dei log e dei database recenti di ogni database primario nell'istanza del server in cui viene ospitata la replica secondaria, utilizzando RESTORE WITH NORECOVERY per ogni operazione di ripristino. Per altre informazioni, vedere [Manually Prepare a Secondary Database for an Availability Group &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
2.  Creare un join di ogni database secondario al gruppo di disponibilità. Per altre informazioni, vedere [Join a Secondary Database to an Availability Group &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione e configurazione di gruppi di disponibilità &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41; ](overview-of-always-on-availability-groups-sql-server.md)    
 [Risolvere i problemi &#40;di&#41;configurazione gruppi di disponibilità AlwaysOn SQL Server eliminati](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
