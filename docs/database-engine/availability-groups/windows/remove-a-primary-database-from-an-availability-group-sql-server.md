---
title: Rimuovere un database primario da un gruppo di disponibilità
description: Passaggi per rimuovere un database primario da un gruppo di disponibilità Always On usando Transact-SQL (T-SQL), PowerShell o SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.removeprimarydb.f1
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 6d4ca31e-ddf0-44bf-be5e-a5da060bf096
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5fb0b24d51c383466cf91e6e691717170c290f4
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202000"
---
# <a name="remove-a-primary-database-from-an-always-on-availability-group"></a>Rimuovere un database primario da un gruppo di disponibilità Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questo argomento illustra come rimuovere il database primario e il database o i database secondari corrispondenti da un gruppo di disponibilità Always On usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti e restrizioni](#Prerequisites)  
  
     [Sicurezza](#Security)  
  
-   **Per rimuovere un database di disponibilità utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Completamento:**  [dopo la rimozione di un database di disponibilità da un gruppo di disponibilità](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti e restrizioni  
  
-   Questa attività può essere eseguita solo sulle repliche primarie. È necessario essere connessi all'istanza del server che ospita la replica primaria.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per rimuovere un database di disponibilità**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica primaria del database o dei database da rimuovere ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità**.  
  
3.  Selezionare il gruppo di disponibilità ed espandere il nodo **Database di disponibilità** .  
  
4.  Questo passaggio dipende dalla scelta di rimuovere uno o più database:  
  
    -   Per rimuovere più database, utilizzare il riquadro **Dettagli Esplora oggetti** per visualizzare e selezionare tutti i database che si desidera rimuovere. Per altre informazioni, vedere [Utilizzare Dettagli Esplora oggetti per monitorare Gruppi di disponibilità &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Per rimuovere un singolo database, selezionarlo nel riquadro **Esplora oggetti** o **Dettagli Esplora oggetti** .  
  
5.  Fare clic con il pulsante destro del mouse sul database o sui database selezionati e scegliere **Rimuovere il database dal gruppo di disponibilità** nel menu dei comandi.  
  
6.  Nella finestra di dialogo **Rimuovi i database dal gruppo di disponibilità** scegliere **OK**per rimuovere tutti i database elencati. Se non si desidera rimuoverli tutti, scegliere **Annulla**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 **Per rimuovere un database di disponibilità**  
  
1.  Connettersi all'istanza del server che ospita la replica primaria.  
  
2.  Utilizzare l'istruzione [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) , come indicato di seguito:  
  
     ALTER AVAILABILITY GROUP *group_name* REMOVE DATABASE *availability_database_name*  
  
     dove *group_name* è il nome del gruppo di disponibilità e *database_name* è il nome di un database da aggiungere al gruppo.  
  
     Nell'esempio seguente viene rimosso un database denominato `Db6` dal gruppo di disponibilità `MyAG` .  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG REMOVE DATABASE Db6;  
    ```  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Per rimuovere un database di disponibilità**  
  
1.  Cambiare la directory (**cd**) impostandola sull'istanza del server che ospita la replica primaria.  
  
2.  Usare il cmdlet **Remove-SqlAvailabilityDatabase** specificando il nome del database di disponibilità da rimuovere dal gruppo di disponibilità. Quando si è connessi all'istanza del server che ospita la replica primaria, il database primario e i database secondari corrispondenti vengono tutti rimossi dal gruppo di disponibilità.  
  
     Ad esempio, il seguente comando rimuove il database di disponibilità `MyDb9` dal gruppo di disponibilità denominato `MyAg`. Dal momento che il comando viene eseguito nell'istanza del server che ospita la replica primaria, il database primario e tutti i relativi database secondari corrispondenti vengono rimossi dal gruppo di disponibilità. La sincronizzazione dei dati non verrà più eseguita per questo database in nessuna replica secondaria.  
  
    ```  
    Remove-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\PrimaryComputer\InstanceName\AvailabilityGroups\MyAg\AvailabilityDatabases\MyDb9
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, usare il cmdlet **Get-Help** nell'ambiente [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Completamento: dopo la rimozione di un database di disponibilità da un gruppo di disponibilità  
 La rimozione di un database di disponibilità dal relativo gruppo di disponibilità termina la sincronizzazione dati tra il database primario precedente e i database secondari corrispondenti. Il database primario precedente rimane online. Ogni database secondario corrispondente viene posto nello stato RESTORING.  
  
 A questo punto sono disponibili modi alternativi per gestire un database secondario rimosso:  
  
-   Se un determinato database secondario non è più necessario, è possibile eliminarlo.  
  
     Per altre informazioni, vedere [Eliminare un database](../../../relational-databases/databases/delete-a-database.md).  
  
-   Se si desidera accedere a un database secondario dopo che è stato rimosso dal gruppo di disponibilità, è possibile recuperare il database. Tuttavia, se si recupera un database secondario rimosso, saranno online due database indipendenti e divergenti con lo stesso nome. È necessario assicurarsi che i client possano accedere a uno solo di essi, di solito al database primario più recente.  
  
     Per altre informazioni, vedere [Recuperare un database senza ripristino dei dati &#40;Transact-SQL&#41;](../../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Rimuovere un database secondario da un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
  
