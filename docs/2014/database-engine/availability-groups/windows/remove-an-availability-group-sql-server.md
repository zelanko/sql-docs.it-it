---
title: Rimuovere un gruppo di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.deleteag.f1
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], dropping
ms.assetid: 4b7f7f62-43a3-49db-a72e-22d4d7c2ddbb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c17b7d5b362d8b4030d66ebf7ba0e425495410e7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936562"
---
# <a name="remove-an-availability-group-sql-server"></a>Rimuovere un gruppo di disponibilità (SQL Server)
  In questo argomento si illustra come eliminare (rimuovere) un gruppo di disponibilità AlwaysOn utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Se un'istanza del server che ospita una delle repliche di disponibilità è offline quando si elimina un gruppo di disponibilità, la replica di disponibilità locale verrà eliminata dall'istanza del server quando torna online. La rimozione di un gruppo di disponibilità comporta l'eliminazione di qualsiasi listener del gruppo di disponibilità associato.  
  
 Si noti che, se necessario, è possibile rimuovere un gruppo di disponibilità da qualsiasi nodo WSFC (Windows Server Failover Clustering) in cui siano disponibili le credenziali di sicurezza corrette per il gruppo di disponibilità. In questo modo, è possibile eliminare un gruppo di disponibilità quando non rimane nessuna delle relative repliche di disponibilità.  
  
> [!IMPORTANT]  
>  Se possibile, rimuovere il gruppo di disponibilità solo se connesso all'istanza del server in cui è ospitata la replica primaria. Se il gruppo di disponibilità viene rimosso dalla replica primaria, sono consentite modifiche nei database primari precedenti (senza protezione a disponibilità elevata). Eliminando un gruppo di disponibilità da una replica secondaria, la replica primaria viene mantenuta nello stato RESTORING e non sono consentite modifiche nei database.  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e consigli](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per eliminare un gruppo di disponibilità utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [Contenuto correlato](#RelatedContent)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-recommendations"></a><a name="Restrictions"></a>Limitazioni e consigli  
  
-   L'eliminazione del gruppo di disponibilità online da una replica secondaria determina la transizione della replica primaria allo stato RESTORING. Pertanto, se possibile, rimuovere il gruppo di disponibilità solo dall'istanza del server in cui è ospitata la replica primaria.  
  
-   Se si elimina un gruppo di disponibilità da un computer rimosso o eliminato dal cluster di failover WSFC, il gruppo di disponibilità viene eliminato solo localmente.  
  
-   Evitare di eliminare un gruppo di disponibilità se il cluster WSFC (Windows Server Failover Clustering) non dispone di quorum. Se è necessario eliminare un gruppo di disponibilità quando il cluster non dispone di quorum, non verrà rimosso il gruppo di disponibilità dei metadati archiviato nel cluster. Una volta che il cluster avrà riacquisito il quorum, sarà necessario eliminare nuovamente il gruppo di disponibilità per rimuoverlo dal cluster WSFC.  
  
-   In una replica secondaria è opportuno utilizzare DROP AVAILABILITY GROUP solo in casi di emergenza, poiché, se si elimina un gruppo di disponibilità, quest'ultimo viene portato offline. Se si elimina il gruppo di disponibilità da una replica secondaria, la replica primaria non è in grado di determinare se lo stato è passato OFFLINE a causa della perdita del quorum, di un failover forzato o di un comando DROP AVAILABILITY GROUP. La replica primaria passa allo stato RESTORING per impedire una possibile situazione split-brain. Per altre informazioni, vedere [How It Works: DROP AVAILABILITY GROUP Behaviors](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Funzionamento: comportamenti di DROP AVAILABILITY GROUP) nel blog del Supporto Tecnico di SQL Server.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER. Per eliminare un gruppo di disponibilità non ospitato dall'istanza del server locale, è necessaria l'autorizzazione CONTROL SERVER o CONTROL in tale gruppo di disponibilità.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per eliminare un gruppo di disponibilità**  
  
1.  In Esplora oggetti connettersi all'istanza del server in cui è ospitata la replica primaria, se possibile, o connettersi a un'altra istanza del server abilitata per la funzionalità Gruppi di disponibilità AlwaysOn in un nodo WSFC che dispone delle credenziali di sicurezza corrette per il gruppo di disponibilità. Espandere l'albero di server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Questo passaggio dipende dalla scelta di eliminare più gruppi di disponibilità o uno soltanto, come segue:  
  
    -   Per eliminare più gruppi di disponibilità le cui repliche primarie sono nell'istanza del server connesso, usare il riquadro **Dettagli Esplora oggetti** per visualizzare e selezionare tutti i gruppi di disponibilità da eliminare. Per altre informazioni, vedere [Utilizzare Dettagli Esplora oggetti per monitorare Gruppi di disponibilità &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Per eliminare un solo gruppo di disponibilità, selezionarlo nel riquadro **Esplora oggetti** o in quello **Dettagli Esplora oggetti** .  
  
4.  Fare clic con il pulsante destro del mouse sui gruppi di disponibilità selezionati e scegliere il comando **Elimina** .  
  
5.  Nella finestra di dialogo **Rimuovi gruppo di disponibilità** scegliere **OK**per eliminare tutti i gruppi di disponibilità elencati. Se non si desidera rimuovere tutti i gruppi di disponibilità elencati, fare clic su **Annulla**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per eliminare un gruppo di disponibilità**  
  
1.  Connettersi all'istanza del server in cui è ospitata la replica primaria, se possibile, o connettersi a un'altra istanza del server abilitata per la funzionalità Gruppi di disponibilità AlwaysOn in un nodo WSFC che dispone delle credenziali di sicurezza corrette per il gruppo di disponibilità.  
  
2.  Utilizzare l'istruzione [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql) , come indicato di seguito  
  
     DROP AVAILABILITY GROUP *nome_gruppo*  
  
     dove *nome_gruppo* è il nome del gruppo di disponibilità da rimuovere.  
  
     Nell'esempio seguente viene eliminato il gruppo di disponibilità `MyAG` .  
  
    ```sql
    DROP AVAILABILITY GROUP MyAG;  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Per eliminare un gruppo di disponibilità**  
  
 Nel provider PowerShell per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
1.  Impostare la directory (`cd`) sull'istanza del server in cui è ospitata la replica primaria, se possibile, o connettersi a un'altra istanza del server abilitata per la funzionalità Gruppi di disponibilità AlwaysOn in un nodo WSFC che dispone delle credenziali di sicurezza corrette per il gruppo di disponibilità.  
  
2.  Usare il cmdlet **Remove-SqlAvailabilityGroup** .  
  
     Ad esempio, il comando seguente rimuove il gruppo di disponibilità denominato `MyAg`. Il comando può essere eseguito in qualsiasi istanza del server che ospita una replica di disponibilità per il gruppo di disponibilità.  
  
    ```powershell
    Remove-SqlAvailabilityGroup -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Contenuto correlato  
  
-   [How It Works: DROP AVAILABILITY GROUP Behaviors](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Funzionamento: comportamenti di DROP AVAILABILITY GROUP) nel blog del Supporto Tecnico di SQL Server  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Creazione e configurazione di gruppi di disponibilità &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
