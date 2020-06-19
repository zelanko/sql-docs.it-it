---
title: Creare un join di un database secondario a un gruppo di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.joindbs.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- secondary databases [SQL Server]
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: fd7efe79-c1f9-497d-bfe7-b2a2b2321cf5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b0d79325bcde33d13688003de079a42a9601cc41
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936772"
---
# <a name="join-a-secondary-database-to-an-availability-group-sql-server"></a>Creare un join di un database secondario a un gruppo di disponibilità (SQL Server)
  In questo argomento si spiega come creare un join di un database secondario a un gruppo di disponibilità AlwaysOn utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Dopo aver preparato un database secondario per una replica di secondaria, è necessario creare un join del database al gruppo di disponibilità non appena possibile. In questo modo verrà avviato lo spostamento di dati dal database primario corrispondente al database secondario.  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti](#Prerequisites)  
  
     [Sicurezza](#Security)  
  
-   **Per preparare un database secondario tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
> [!NOTE]  
>  Per informazioni sulle operazioni eseguite dopo l'aggiunta di un database secondario al gruppo, vedere [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
  
-   È necessario essere connessi all'istanza del server che ospita la replica secondaria.  
  
-   È necessario avere già creato un join della replica secondaria al gruppo di disponibilità. Per altre informazioni, vedere [Creare un join di una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
-   Il database secondario deve essere stato preparato recentemente. Per altre informazioni, vedere [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per creare un join di un database secondario a un gruppo di disponibilità**  
  
1.  In Esplora oggetti connettersi all'istanza del server in cui viene ospitata la replica secondaria ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Espandere il gruppo di disponibilità che si desidera modificare, quindi espandere il nodo **Database disponibili** .  
  
4.  Fare clic con il pulsante destro del mouse sul database e scegliere **Crea un join del gruppo di disponibilità**.  
  
5.  In questo modo verrà aperta la finestra di dialogo **Creare un join dei database al gruppo di disponibilità** . Verificare il nome del gruppo di disponibilità, visualizzato sulla barra del titolo, e il nome o i nomi dei database visualizzati nella griglia, quindi fare clic su **OK**o su **Annulla**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per creare un join di un database secondario a un gruppo di disponibilità**  
  
1.  Connettersi all'istanza del server che ospita la replica secondaria.  
  
2.  Utilizzare la [clausola SET HADR dell'istruzione ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) come indicato di seguito:  
  
     ALTER DATABASE *database_name* SET HADR AVAILABILITY GROUP = *group_name*  
  
     dove *database_name* è il nome del database di cui creare il join e *group_name* è il nome del gruppo di disponibilità.  
  
     Nell'esempio seguente viene creato un join del database secondario, `Db1`, alla replica secondaria locale del gruppo di disponibilità `MyAG`.  
  
    ```sql
    ALTER DATABASE Db1 SET HADR AVAILABILITY GROUP = MyAG;  
    ```  
  
    > [!NOTE]  
    >  Per un esempio di questa istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] impiegata in un contesto, vedere [Creare un gruppo di disponibilità &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md).  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Per creare un join di un database secondario a un gruppo di disponibilità**  
  
1.  Impostare la directory (`cd`) sull'istanza del server in cui viene ospitata la replica secondaria.  
  
2.  Utilizzare il cmdlet `Add-SqlAvailabilityDatabase` per creare un join di uno o più database secondari al gruppo di disponibilità.  
  
     Ad esempio, il seguente comando crea un join di un database secondario, `Db1`, al gruppo di disponibilità `MyAG` in una delle istanze del server che ospita una replica secondaria.  
  
    ```powershell
    Add-SqlAvailabilityDatabase -Path SQLSERVER:\SQL\SecondaryServer\InstanceName\AvailabilityGroups\MyAG -Database "Db1"  
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Creare un join di una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)   
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Risolvere i problemi di Gruppi di disponibilità AlwaysOn &#40;di configurazione SQL Server eliminati&#41;](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
