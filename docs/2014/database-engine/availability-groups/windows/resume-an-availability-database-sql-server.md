---
title: Riprendere un database di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.resumedatamove.f1
helpviewer_keywords:
- Availability Groups [SQL Server], resuming a database
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], databases
ms.assetid: 20e9147b-e985-4caa-910e-fc4b38dbf9a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2b85a2b6e7d574c1752eba84d1bfc2bce8dbafc6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788718"
---
# <a name="resume-an-availability-database-sql-server"></a>Riprendere un database di disponibilità (SQL Server)
  In [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] è possibile riprendere un database di disponibilità sospeso utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Quando si riprende un database sospeso, viene attivato lo stato SYNCHRONIZING per il database. Con la ripresa del database primario vengono inoltre ripresi anche eventuali database secondari sospesi in seguito alla sospensione del database primario. Se un database secondario è stato sospeso in locale, dall'istanza del server che ospita la replica secondaria, è necessario riprendere tale database secondario in locale. Quando un database secondario e il database primario corrispondente sono nello stato SYNCHRONIZING, la sincronizzazione dei dati viene ripresa nel database secondario.  
  
> [!NOTE]  
>  La sospensione e la ripresa di un database secondario AlwaysOn non incide direttamente sulla disponibilità del database primario. Tuttavia, la sospensione di un database secondario può avere un impatto sulle funzionalità di ridondanza e failover del database primario, finché il database secondario sospeso non viene ripreso. Questo comportamento è diverso rispetto al mirroring del database, in cui lo stato del mirroring risulta sospeso sia sul database mirror che sul database principale, finché il mirroring non viene ripreso. La sospensione di un database primario AlwaysOn comporta la sospensione dello spostamento di dati su tutti i database secondari corrispondenti, mentre le funzionalità di ridondanza e failover cessano per tale database finché il database primario non viene ripreso.  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Prerequisiti](#Prerequisites)  
  
     [Sicurezza](#Security)  
  
-   **Per riprendere un database secondario tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Un comando RESUME viene restituito non appena è stato accettato dalla replica che ospita il database di destinazione, ma la ripresa effettiva del database avviene in modo asincrono.  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   È necessario essere connessi all'istanza del server che ospita il database da riprendere.  
  
-   Il gruppo di disponibilità deve essere online.  
  
-   Il database primario deve essere online e disponibile.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per il database.  
  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per riprendere un database secondario**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica di disponibilità in cui si desidera riprendere un database ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Espandere il gruppo di disponibilità.  
  
4.  Espandere il nodo **Database di disponibilità** , fare clic con il pulsante destro del mouse sul database e fare clic su **Riprendi spostamento dati**.  
  
5.  Nella finestra di dialogo **Riprendi spostamento dati** fare clic su **OK**.  
  
> [!NOTE]  
>  Per riprendere database aggiuntivi in questo percorso di replica, ripetere i passaggi 4 e 5 per ogni database.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 **Per riprendere un database secondario sospeso in locale**  
  
1.  Connettersi all'istanza del server che ospita la replica secondaria di cui si desidera riprendere il database.  
  
2.  Riprendere il database secondario usando l'istruzione [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-hadr)seguente:  
  
     ALTER DATABASE *nome_database* SET HADR RESUME  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Per riprendere un database secondario**  
  
1.  Impostare la directory (`cd`) sull'istanza del server che ospita la replica di cui si desidera riprendere il database. Per altre informazioni, vedere la sessione [Prerequisiti](#Prerequisites)più indietro in questo argomento.  
  
2.  Usare il cmdlet **Resume-SqlAvailabilityDatabase** per riprendere il gruppo di disponibilità.  
  
     Ad esempio, il seguente comando riprende la sincronizzazione dati per il database di disponibilità `MyDb3` nel gruppo di disponibilità `MyAg`.  
  
    ```  
    Resume-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Sospendere un database di disponibilità &#40;SQL Server&#41;](suspend-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
