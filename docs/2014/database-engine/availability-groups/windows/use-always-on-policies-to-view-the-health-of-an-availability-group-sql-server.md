---
title: Usare i criteri AlwaysOn per visualizzare l'integrità di un gruppo di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6f1bcbc3-1220-4071-8e53-4b957f5d3089
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 12a183718ee13915fd6236caf943fea03819e723
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812978"
---
# <a name="use-alwayson-policies-to-view-the-health-of-an-availability-group-sql-server"></a>Utilizzare i criteri AlwaysOn per visualizzare l'integrità di un gruppo di disponibilità (SQL Server)
  In questo argomento viene illustrato come determinare l'integrità operativa di un gruppo di disponibilità AlwaysOn utilizzando i criteri AlwaysOn in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Per informazioni sulla gestione basata su criteri AlwaysOn, vedere [i criteri AlwaysOn per problemi operativi con gruppi di disponibilità AlwaysOn (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md).  
  
> [!IMPORTANT]  
>  Per i criteri AlwaysOn, i nomi delle categorie vengono utilizzati come ID. La modifica del nome di una categoria AlwaysOn causa l'interruzione della funzionalità di valutazione dell'integrità. Pertanto, i nomi di categoria AlwaysOn non devono mai essere modificati.  
  

  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre delle autorizzazioni CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION.  
  
##  <a name="SSMSProcedure"></a> Utilizzo del Dashboard AlwaysOn  
 **Per aprire il AlwaysOn Dashboard**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita una delle repliche di disponibilità. Per visualizzare informazioni su tutte le repliche di disponibilità di un determinato gruppo, connettersi all'istanza del server che ospita la replica primaria.  
  
2.  Fare clic sul nome del server per espandere il relativo albero.  
  
3.  Espandere il nodo **Disponibilità elevata AlwaysOn** .  
  
     Fare clic con il pulsante destro del mouse sul nodo **Gruppi di disponibilità** o espandere il nodo e fare clic con il pulsante destro del mouse su un gruppo di disponibilità specifico.  
  
4.  Selezionare il comando **Mostra dashboard** .  
  
 Per informazioni su come usare il dashboard AlwaysOn, vedere [Utilizzare il Dashboard AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md).  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Usare i criteri AlwaysOn per visualizzare l'integrità di un gruppo di disponibilità**  
  
1.  Spostarsi sulla directory (`cd`) dell'istanza del server che ospita una delle repliche di disponibilità. Per visualizzare informazioni su tutte le repliche di disponibilità di un determinato gruppo, connettersi all'istanza del server che ospita la replica primaria.  
  
2.  Utilizzare i cmdlet seguenti:  
  
     `Test-SqlAvailabilityGroup`  
     Valuta l'integrità di un gruppo di disponibilità valutando i criteri della gestione basata su criteri di SQL Server. È necessario disporre delle autorizzazioni CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION per eseguire questo cmdlet.  
  
     Ad esempio, il comando seguente mostra tutti i gruppi di disponibilità con stato di integrità "Error" nell'istanza del server `Computer\Instance`.  
  
    ```powershell
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups |
        Test-SqlAvailabilityGroup |
        Where-Object { $_.HealthState -eq "Error" }  
    ```  
  
     `Test-SqlAvailabilityReplica`  
     Valuta l'integrità delle repliche di disponibilità valutando i criteri della gestione basata su criteri di SQL Server. È necessario disporre delle autorizzazioni CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION per eseguire questo cmdlet.  
  
     Ad esempio, il seguente comando valuta l'integrità della replica di disponibilità denominata `MyReplica` nel gruppo di disponibilità `MyAg` e restituisce un breve riepilogo.  
  
    ```powershell
    Test-SqlAvailabilityReplica `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
     `Test-SqlDatabaseReplicaState`  
     Valuta l'integrità di un database di disponibilità su tutte le repliche di disponibilità aggiunte valutando i criteri della gestione basata su criteri di SQL Server.  
  
     Ad esempio, il seguente comando valuta l'integrità di tutte i database di disponibilità nel gruppo di disponibilità `MyAg` e restituisce un breve riepilogo per ognuno di essi.  
  
    ```powershell
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\DatabaseReplicaStates |
        Test-SqlDatabaseReplicaState  
    ```  
  
     Questi cmdlet accettano le opzioni seguenti:  
  
    |Opzione|Descrizione|  
    |------------|-----------------|  
    |`AllowUserPolicies`|Esegue i criteri utente trovati nelle categorie dei criteri AlwaysOn.|  
    |`InputObject`|Raccolta di oggetti che rappresentano gruppi di disponibilità, repliche di disponibilità o stati dei database di disponibilità. Il cmdlet calcolerà l'integrità degli oggetti specificati.|  
    |`NoRefresh`|Quando questo parametro viene impostato, il cmdlet non aggiorna manualmente gli oggetti specificati dal parametro `-Path` o `-InputObject`.|  
    |`Path`|Percorso del gruppo di disponibilità, una o più repliche di disponibilità o stato del cluster della replica di database del database di disponibilità (a seconda del cmdlet utilizzato). Questo parametro è facoltativo. Se non specificato, il valore predefinito di questo parametro sarà il percorso di lavoro corrente.|  
    |`ShowPolicyDetails`|Mostra il risultato di ogni valutazione dei criteri eseguita da questo cmdlet. Il cmdlet restituisce un oggetto per ogni valutazione dei criteri e questo oggetto contiene campi che descrivono i risultati della valutazione, ovvero se i criteri sono stati soddisfatti, il nome e la categoria dei criteri e così via.|  
  
     Ad esempio, il seguente comando `Test-SqlAvailabilityGroup` specifica il parametro `-ShowPolicyDetails` per mostrare i risultati della valutazione per ciascun criterio eseguita da questo cmdlet per ciascun criterio della gestione basata su criteri eseguito sul gruppo di disponibilità `MyAg`.  
  
    ```powershell
    Test-SqlAvailabilityGroup `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\AgName `  
    -ShowPolicyDetails  
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Visualizzare la Guida di SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
 **SQL Server AlwaysOn Team blog: monitoraggio dell'integrità AlwaysOn con PowerShell:**  
  
-   [Parte 1: Panoramica dei cmdlet di base](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-1.aspx)  
  
-   [Parte 2: Utilizzo di cmdlet avanzati](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-2.aspx)  
  
-   [Parte 3: Semplice applicazione di monitoraggio](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/monitoring-alwayson-health-with-powershell-part-3.aspx)  
  
-   [Parte 4: Integrazione con SQL Server Agent](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/the-always-on-health-model-part-4.aspx)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Amministrazione di un gruppo di disponibilità &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [Monitoraggio di Gruppi di disponibilità &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Criteri AlwaysOn per problemi operativi con gruppi di disponibilità AlwaysOn (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md) 
  
  
