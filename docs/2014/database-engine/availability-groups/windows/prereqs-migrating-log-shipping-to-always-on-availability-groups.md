---
title: Prerequisiti per la migrazione dal log shipping al Gruppi di disponibilità AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 2738ce65-205e-4682-92d8-dc7e37c58b2b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c517850e7dfc7dfb134389b50feee77b3d1cbfbf
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936632"
---
# <a name="prerequisites-for-migrating-from-log-shipping-to-alwayson-availability-groups-sql-server"></a>Prerequisiti per la migrazione dal log shipping ai gruppi di disponibilità AlwaysOn (SQL Server)
  In questo argomento vengono descritti i prerequisiti per convertire un database primario per il log shipping insieme a uno o più dei relativi database secondari in un database primario AlwaysOn e nei relativi database secondari.  
  
> [!NOTE]  
>  In un gruppo di disponibilità è possibile configurare qualsiasi database primario o secondario (possibilmente leggibile) come un database primario per il log shipping.  
  
 **Contenuto dell'argomento:**  
  
-   [Prerequisiti dei gruppi di disponibilità](#AGPrereqsRealAddress)  
  
-   [Prerequisiti per il log shipping](#LogShipPrereqs)  
  
-   [Attività correlate](#RelatedTasks)  
  
-   [Contenuto correlato](#RelatedContent)  
  
##  <a name="availability-group-prerequisites"></a><a name="AGPrereqsRealAddress"></a>Prerequisiti del gruppo di disponibilità  
 Per consentire l'esecuzione dei processi di backup sulla replica primaria del gruppo di disponibilità, utilizzare le seguenti impostazioni per i gruppi di disponibilità AlwaysOn:  
  
|Proprietà|Impostazione|  
|--------------|-------------|  
|Preferenza di backup automatico del gruppo di disponibilità.|Solo nella replica primaria|  
|Priorità di backup della replica primaria.|>0|  
  
 **Per ulteriori informazioni:**  
  
 [Visualizzare le proprietà dei gruppi di disponibilità &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
 [Configurare il backup su repliche di disponibilità &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="log-shipping-prerequisites"></a><a name="LogShipPrereqs"></a> Prerequisiti per il log shipping  
  
-   È necessario che il database primario per il log shipping risieda nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che ospita la replica primaria iniziale/corrente del gruppo di disponibilità.  
  
-   Per fare in modo che un determinato database secondario per il log shipping venga convertito in un database secondario AlwaysOn, tale database dovrà:  
  
    -   Utilizzare lo stesso nome del database primario.  
  
    -   Risiedere su un'istanza del server in cui viene ospitata una replica secondaria del gruppo di disponibilità.  
  
 Dopo l'esecuzione del processo di backup sul database primario, disabilitare il processo di backup e al termine dell'esecuzione del processo di ripristino su un determinato database secondario, disabilitare il processo di ripristino.  
  
 Dopo avere creato tutti i database secondari per il gruppo di disponibilità, se si desidera eseguire backup sulle repliche secondarie, è necessario configurare nuovamente la preferenza di backup automatico del gruppo di disponibilità.  
  
 **Per ulteriori informazioni:**  
  
 [Converting a logshipping configuration to Availability Group](https://blogs.msdn.com/b/sqlalwayson/archive/2012/01/09/converting-a-logshipping-configuration-to-availability-group.aspx) (Conversione di una configurazione per il log shipping in un gruppo di disponibilità) (blog su SQL Server)  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
 **Log shipping**  
  
-   [Aggiornare il log shipping a SQL Server 2014 &#40;Transact-SQL&#41;](../../log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Rimuovere il log shipping &#40;SQL Server&#41;](../../log-shipping/remove-log-shipping-sql-server.md)  
  
 **Gruppi di disponibilità AlwaysOn**  
  
-   [Usare la Creazione guidata Gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Utilizzare la finestra di dialogo Nuovo gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Creare un gruppo di disponibilità &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [Creare un gruppo di disponibilità &#40;PowerShell SQL Server&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [Creare un join di un database secondario a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Configurare il backup su repliche di disponibilità &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Contenuto correlato  
  
-   **Blog:**  
  
     [Conversione di una configurazione per il log shipping in un gruppo di disponibilità](https://docs.microsoft.com/archive/blogs/sqlalwayson/converting-a-logshipping-configuration-to-availability-group)  
  
     [Pagina relativa all'aggiunta di un database primario e di database secondari per il log shipping in un gruppo di disponibilità esistente](https://docs.microsoft.com/archive/blogs/sqlalwayson/add-a-log-shipping-primary-database-and-secondary-databases-to-an-existing-availability-group)  
  
     [Blog del team di SQL Server AlwaysOn: Blog ufficiale del team di SQL Server AlwaysOn](https://docs.microsoft.com/archive/blogs/sqlalwayson/)  
  
     [Pagina relativa ai blog del Servizio Supporto Tecnico Clienti per gli ingegneri di SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **White paper:**  
  
     [Pagina relativa alla guida alla migrazione in cui viene illustrata la migrazione in gruppi di disponibilità AlwaysOn da distribuzioni precedenti in cui vengono combinati il mirroring del database e il log shipping](https://msdn.microsoft.com/library/jj635217)  
  
     [Pagina relativa ai white paper Microsoft per SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Pagina relativa ai white paper del team di consulenza clienti di SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](../../log-shipping/about-log-shipping-sql-server.md)   
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Monitoraggio di Gruppi di disponibilità &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
