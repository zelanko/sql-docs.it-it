---
title: Abilitare e disabilitare Gruppi di disponibilità AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], disabling
- Availability Groups [SQL Server], enabling
ms.assetid: 7c326958-5ae9-4761-9c57-905972276a8f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a441595fa07c86ff1cdbeac4e67e3a6ca0361f80
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72782980"
---
# <a name="enable-and-disable-alwayson-availability-groups-sql-server"></a>Abilitare e disabilitare la funzionalità Gruppi di disponibilità AlwaysOn (SQL Server)
  L'abilitazione di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] è un prerequisito per l'utilizzo di gruppi di disponibilità in un'istanza del server. Prima di poter creare e configurare un qualsiasi gruppo di disponibilità, la funzionalità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] deve essere stata abilitata in ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui sarà ospitata una replica di disponibilità per uno o più gruppi di disponibilità.  
  
> [!IMPORTANT]  
>  Se si elimina e si ricrea un cluster WSFC, è necessario disabilitare e riabilitare la funzionalità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui è ospitata una replica di disponibilità nel cluster WSFC originale.  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti](#Prerequisites)  
  
     [Sicurezza](#Security)  
  
-   **Come si fa:**  
  
    -   [Determinare se la funzionalità Gruppi di disponibilità AlwaysOn è abilitata](#IsEnabled)  
  
    -   [Abilita Gruppi di disponibilità AlwaysOn](#EnableAOAG)  
  
    -   [Disabilitare Gruppi di disponibilità AlwaysOn](#DisableAOAG)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a>Prerequisiti per l'abilitazione di Gruppi di disponibilità AlwaysOn  
  
-   L'istanza del server deve trovarsi in un nodo WSFC (Windows Server Failover Clustering).  
  
-   Nell'istanza del server deve essere in esecuzione un'edizione di SQL Server che supporta [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Per ulteriori informazioni, vedere [Features Supported by the Editions of SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   Abilitare Gruppi di disponibilità AlwaysOn in una sola istanza del server per volta. Dopo aver abilitato Gruppi di disponibilità AlwaysOn, attendere il riavvio del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] prima di continuare con un'altra istanza del server.  
  
 Per informazioni sui prerequisiti aggiuntivi per la creazione e la configurazione dei gruppi di disponibilità, vedere [prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Sicurezza  
 Mentre la funzionalità Gruppi di disponibilità AlwaysOn è abilitata in un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'istanza del server dispone del controllo completo nel cluster WSFC.  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'appartenenza al gruppo degli **amministratori** nel computer locale, nonché il controllo totale nel cluster WSCF. Quando si abilita AlwaysOn tramite PowerShell, aprire la finestra del prompt dei comandi utilizzando l'opzione **Esegui come amministratore** .  
  
 Richiede le autorizzazioni per la gestione e la creazione degli oggetti di Active Directory.  
  
##  <a name="IsEnabled"></a>Determinare se Gruppi di disponibilità AlwaysOn è abilitato  
  
-   [SQL Server Management Studio](#SSMS1Procedure)  
  
-   [Transact-SQL](#Tsql1Procedure)  
  
-   [PowerShell](#PowerShell1Procedure)  
  
###  <a name="SSMS1Procedure"></a> Con SQL Server Management Studio  
 **Per determinare se la funzionalità Gruppi di disponibilità AlwaysOn è abilitata**  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sull'istanza del server e scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **Proprietà server** scegliere la pagina **Generale** . Per la proprietà **Is HADR Enabled** è visualizzato uno dei valori seguenti:  
  
    -   **True**se gruppi di disponibilità AlwaysOn è abilitato  
  
    -   **False**se gruppi di disponibilità AlwaysOn è disabilitato.  
  
###  <a name="Tsql1Procedure"></a> Con Transact-SQL  
 **Per determinare se la funzionalità Gruppi di disponibilità AlwaysOn è abilitata**  
  
1.  Utilizzare l'istruzione [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql) seguente:  
  
    ```sql
    SELECT SERVERPROPERTY ('IsHadrEnabled');  
    ```  
  
     L'impostazione della proprietà del server `IsHadrEnabled` indica se un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è abilitata per Gruppi di disponibilità AlwaysOn, come indicato di seguito:  
  
    -   Se `IsHadrEnabled` = 1, la funzionalità Gruppi di disponibilità AlwaysOn è abilitata.  
  
    -   Se `IsHadrEnabled` = 0, la funzionalità Gruppi di disponibilità AlwaysOn è disabilitata.  
  
    > [!NOTE]  
    >  Per ulteriori informazioni sulla proprietà `IsHadrEnabled` del server, vedere [ServerProperty &#40;&#41;Transact-SQL ](/sql/t-sql/functions/serverproperty-transact-sql).  
  
###  <a name="PowerShell1Procedure"></a> Con PowerShell  
 **Per determinare se la funzionalità Gruppi di disponibilità AlwaysOn è abilitata**  
  
1.  Impostare il valore`cd`predefinito () sull'istanza del server, `\SQL\NODE1\DEFAULT`ad esempio, in cui si desidera determinare [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] se è abilitato.  
  
2.  Eseguire il comando PowerShell `Get-Item` riportato di seguito:  
  
    ```powershell
    Get-Item . | Select IsHadrEnabled  
    ```  
  
    > [!NOTE]  
    >  Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="EnableAOAG"></a> Abilitare Gruppi di disponibilità AlwaysOn  
 **Per abilitare AlwaysOn mediante:**  
  
-   [Gestione configurazione SQL Server](#SQLCM2Procedure)  
  
-   [PowerShell](#PScmd2Procedure)  
  
###  <a name="SQLCM2Procedure"></a> Utilizzo di Gestione configurazione SQL Server  
 **Per abilitare Gruppi di disponibilità AlwaysOn**  
  
1.  Connettersi al nodo WSCF (Windows Server Failover Clustering) in cui è ospitata l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nella quale si desidera abilitare Gruppi di disponibilità AlwaysOn.  
  
2.  Nel menu **Start** scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Strumenti di configurazione**, quindi fare clic su **Gestione configurazione SQL Server**.  
  
3.  In **Gestione configurazione SQL Server**fare clic su **servizi SQL Server**, fare clic con il pulsante destro del mouse ** < *`instance name`* ** su SQL Server (** < *`instance name`*>)**, dove è il nome di un'istanza del server locale per cui si desidera abilitare gruppi di disponibilità AlwaysOn e quindi fare clic su **Proprietà.**  
  
4.  Selezionare la scheda **Disponibilità elevata AlwaysOn** .  
  
5.  Verificare che nel campo **Nome cluster di failover Windows** sia incluso il nome del cluster di failover locale. Se il campo è vuoto, questa istanza del server non supporta attualmente [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Il computer locale non è un nodo del cluster, il cluster WSFC è stato chiuso, oppure si tratta di un'edizione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] che non supporta [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
6.  Selezionare la casella di controllo **abilita gruppi di disponibilità AlwaysOn** , quindi fare clic su **OK**.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Successivamente, è necessario riavviare manualmente il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . In questo modo è possibile scegliere un'ora per il riavvio che meglio soddisfa le esigenze aziendali. Al riavvio del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], AlwaysOn sarà abilitato e la proprietà del server `IsHadrEnabled` sarà impostata su 1.  
  
###  <a name="PScmd2Procedure"></a>Utilizzo di SQL Server PowerShell  
 **Per abilitare AlwaysOn**  
  
1.  Impostare la directory (`cd`) su un'istanza del server che si desidera abilitare per Gruppi di disponibilità AlwaysOn.  
  
2.  Utilizzare il cmdlet `Enable-SqlAlwaysOn` per abilitare Gruppi di disponibilità AlwaysOn.  
  
     Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
    > [!NOTE]  
    >  Per informazioni su come controllare se il `Enable-SqlAlwaysOn` cmdlet riavvia il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servizio, vedere [quando un cmdlet riavvia il servizio SQL Server?](#WhenCmdletRestartsSQL), più avanti in questo argomento.  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
####  <a name="ExmplEnable-SqlHadrServic"></a>Esempio: Enable-SqlAlwaysOn  
 Il comando di PowerShell seguente [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] Abilita in un'istanza di SQL Server (*istanza*del*computer*\\).  
  
```powershell
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
```  
  
##  <a name="DisableAOAG"></a>Disabilitare Gruppi di disponibilità AlwaysOn  
  
-   **Prima di disabilitare AlwaysOn:**  
  
     [Indicazioni](#Recommendations)  
  
-   **Per disabilitare AlwaysOn mediante:**  
  
    -   [Gestione configurazione SQL Server](#SQLCM3Procedure)  
  
    -   [PowerShell](#PScmd3Procedure)  
  
-   **Completamento: dopo la**  [disabilitazione di AlwaysOn](#FollowUp)  
  
> [!IMPORTANT]  
>  Disabilitare AlwaysOn in una sola un'istanza del server per volta. Dopo aver disabilitato Gruppi di disponibilità AlwaysOn, attendere il riavvio del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] prima di continuare con un'altra istanza del server.  
  
###  <a name="Recommendations"></a> Raccomandazioni  
 Prima di disabilitare AlwaysOn su un'istanza del server, si consiglia di eseguire le operazioni seguenti:  
  
1.  Se l'istanza del server sta attualmente ospitando la replica primaria di un gruppo di disponibilità che si desidera tenere, si consiglia di eseguire manualmente un failover sul gruppo di disponibilità a una replica secondaria sincronizzata, se possibile. Per altre informazioni, vedere [Eseguire un failover manuale pianificato di un gruppo di disponibilità &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md).  
  
2.  Rimuovere tutte le repliche secondarie locali. Per altre informazioni, vedere [Rimuovere una replica secondaria da un gruppo di disponibilità &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md).  
  
###  <a name="SQLCM3Procedure"></a> Utilizzo di Gestione configurazione SQL Server  
 **Per disabilitare AlwaysOn**  
  
1.  Connettersi al nodo WSCF (Windows Server Failover Clustering) nel quale è ospitata l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui si desidera disabilitare Gruppi di disponibilità AlwaysOn.  
  
2.  Dal menu **Start** scegliere **tutti i programmi**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **strumenti di configurazione**, quindi fare clic su **Gestione configurazione SQL Server**.  
  
3.  In **Gestione configurazione SQL Server**fare clic su **servizi SQL Server**, fare clic con il pulsante destro del mouse ** < *`instance name`* ** su SQL Server (** < *`instance name`*>)**, dove è il nome di un'istanza del server locale per cui si desidera disabilitare gruppi di disponibilità AlwaysOn, quindi fare clic su **Proprietà**.  
  
4.  Deselezionare la casella di controllo**Abilita gruppi di disponibilità AlwaysOn**nella scheda **Disponibilità elevata AlwaysOn** e scegliere **OK**.  
  
     
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è possibile salvare la modifica e riavviare il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Al riavvio del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], AlwaysOn sarà disabilitato e la proprietà del server `IsHadrEnabled` sarà impostata su 0, per indicare che la funzionalità Gruppi di disponibilità AlwaysOn è disabilitata.  
  
5.  Si consiglia di leggere le informazioni in [Completamento: Dopo la disabilitazione di AlwaysOn](#FollowUp), più avanti in questo argomento.  
  
###  <a name="PScmd3Procedure"></a>Utilizzo di SQL Server PowerShell  
 **Per disabilitare AlwaysOn**  
  
1.  Modificare la directory`cd`() in un'istanza del server attualmente abilitata che si desidera disattivarla per gruppi di disponibilità AlwaysOn.  
  
2.  Utilizzare il cmdlet `Disable-SqlAlwaysOn` per abilitare Gruppi di disponibilità AlwaysOn.  
  
     Il comando seguente, ad esempio, Disabilita gruppi di disponibilità AlwaysOn in un'istanza di SQL Server (*istanza*del*computer*\\).  Il comando richiede il riavvio dell'istanza per cui verrà richiesta la conferma all'utente.  
  
    ```powershell
    Disable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
    ```  
  
    > [!IMPORTANT]  
    >  Per informazioni su come controllare se il `Disable-SqlAlwaysOn` cmdlet riavvia il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servizio, vedere [quando un cmdlet riavvia il servizio SQL Server?](#WhenCmdletRestartsSQL), più avanti in questo argomento.  
  
     Per visualizzare la sintassi di un cmdlet, utilizzare il cmdlet `Get-Help` nell'ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Per altre informazioni, vedere [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
###  <a name="FollowUp"></a>Completamento: dopo la disabilitazione di AlwaysOn  
 Dopo avere disabilitato Gruppi di disponibilità AlwaysOn, è necessario riavviare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Gestione configurazione SQL Server riavvia l'istanza del server automaticamente. Tuttavia, se è stato utilizzato il cmdlet `Disable-SqlAlwaysOn`, sarà necessario riavviare manualmente l'istanza del server. Per altre informazioni, vedere [sqlservr Application](../../../tools/sqlservr-application.md).  
  
 Nell'istanza del server riavviata:  
  
-   Poiché i database di disponibilità non vengono avviati insieme a SQL Server, non saranno accessibili.  
  
-   L'unica istruzione AlwaysOn [!INCLUDE[tsql](../../../includes/tsql-md.md)] supportata è [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql). CREATE AVAILABILITY GROUP, ALTER AVAILABILITY GROUP e le opzioni SET HADR di ALTER DATABASE non sono supportate.  
  
-   I metadati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e i dati di configurazione di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in WSFC non sono interessati dalla disabilitazione di Gruppi di disponibilità AlwaysOn.  
  
 Se si disabilita in modo permanente Gruppi di disponibilità AlwaysOn su ogni istanza del server che ospita una replica di disponibilità per uno o più gruppi di disponibilità, si consiglia di completare i passaggi seguenti:  
  
1.  Se le repliche di disponibilità locali non sono state rimosse prima di disabilitare AlwaysOn, eliminare ogni gruppo di disponibilità per il quale l'istanza del server ospita una replica di disponibilità. Per informazioni sull'eliminazione di un gruppo di disponibilità, vedere [Rimuovere un gruppo di disponibilità &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md).  
  
2.  Per rimuovere i metadati rimanenti, eliminare ogni gruppo di disponibilità interessato su un'istanza del server che fa parte del cluster WSFC originale.  
  
3.  Tutti i database primari continuano a essere accessibili a tutte le connessioni, ma la sincronizzazione dei dati tra i database primario e secondario viene arrestata.  
  
4.  Per i database secondari viene impostato lo stato RESTORING. È possibile eliminare i database o ripristinarli tramite RESTORE WITH RECOVERY. Tuttavia, i database ripristinati non fanno più parte della sincronizzazione dei dati del gruppo di disponibilità.  
  
##  <a name="WhenCmdletRestartsSQL"></a>Quando un cmdlet riavvia il servizio SQL Server?  
 In un'istanza del server attualmente in esecuzione, l'utilizzo di `Enable-SqlAlwaysOn` o `Disable-SqlAlwaysOn` per modificare l'impostazione AlwaysOn corrente può causare il riavvio del servizio SQL Server. Il comportamento del riavvio dipende dalle condizioni seguenti:  
  
|Specifica del parametro -NoServiceRestart|Specifica del parametro -Force|Riavvio del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|--------------------------------------------|---------------------------------|---------------------------------------------------------|  
|No|No|Per impostazione predefinita. Tuttavia dal cmdlet è richiesto quanto segue:<br /><br /> **Per completare questa azione, è necessario riavviare il servizio SQL Server per l'istanza del server ' <instance_name>'. Continuare?**<br /><br /> **[Y] Sì [N] no [S] Sospendi [?] Guida (il valore predefinito è "Y"):**<br /><br /> Se si specifica **N** o **S**, il servizio non viene riavviato.|  
|No|Sì|Servizio riavviato.|  
|Sì|No|Servizio non riavviato.|  
|Sì|Sì|Servizio non riavviato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)  
