---
title: Configurare le impostazioni HealthCheckTimeout | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 3bbeb979-e6fc-4184-ad6e-cca62108de74
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4106de497a43404cb44606259d53beb1ed8f5a58
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797445"
---
# <a name="configure-healthchecktimeout-property-settings"></a>Configurazione delle impostazioni HealthCheckTimeout
  L'impostazione HealthCheckTimeout viene utilizzata per specificare la durata, in millisecondi, dell'attesa della DLL della risorsa di SQL Server relativamente alle informazioni restituite dalla stored procedure [sp_server_diagnostics](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) prima di stabilire la mancata risposta da parte dell'istanza del cluster di failover AlwaysOn. Le modifiche apportate alle impostazioni del timeout vengono applicate immediatamente e non richiedono il riavvio della risorsa di SQL Server.  
  
-   **Prima di iniziare:**  [limitazioni e restrizioni](#Limits), [sicurezza](#Security)  
  
-   **Per configurare l'impostazione l'HeathCheckTimeout utilizzando:**  [PowerShell](#PowerShellProcedure), [Gestione cluster di failover](#WSFC), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Limits"></a> Limitazioni e restrizioni  
 Il valore predefinito di questa proprietà è 60.000 millisecondi (60 secondi). Il valore minimo è 15.000 millisecondi (15 secondi).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre delle autorizzazioni ALTER SETTINGS e VIEW SERVER STATE.  
  
##  <a name="PowerShellProcedure"></a> Con PowerShell  
  
### <a name="to-configure-healthchecktimeout-settings"></a>Per configurare le impostazioni HealthCheckTimeout  
  
1.  Avviare Windows PowerShell con privilegi elevati tramite **Esegui come amministratore**.  
  
2.  Importare il modulo `FailoverClusters` per abilitare i cmdlet del cluster.  
  
3.  Utilizzare il `Get-ClusterResource` cmdlet per trovare la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] risorsa, quindi utilizzare `Set-ClusterParameter` il cmdlet per impostare la proprietà **HealthCheckTimeout** per l'istanza del cluster di failover.  
  
> [!TIP]  
>  Ogni volta che viene aperta una nuova finestra di PowerShell, è necessario importare il modulo `FailoverClusters`.  

 Nell'esempio seguente, l'impostazione HealthCheckTimeout nella risorsa di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] "`SQL Server (INST1)`" viene impostata su 60.000 millisecondi.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter HealthCheckTimeout 60000  
```  
  
### <a name="related-content-powershell"></a>Contenuto correlato (PowerShell)  
  
-   [Clustering and High-Availability](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (Failover Clustering and Network Load Balancing Team Blog) (Clustering e disponibilità elevata - Blog del team di clustering di failover e bilanciamento del carico di rete)  
  
-   [Introduzione a Windows PowerShell in un cluster di failover](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandi di risorse cluster e cmdlet di Windows PowerShell equivalenti](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a>Utilizzo dello snap-in Gestione cluster di failover  
 **Per configurare l'impostazione HealthCheckTimeout**  
  
1.  Aprire lo snap-in Gestione cluster di failover.  
  
2.  Espandere **Servizi e applicazioni** e selezionare l'istanza del cluster di failover.  
  
3.  Fare clic con il pulsante destro del mouse sulla risorsa **SQL Server** in **Altre risorse** e selezionare **Proprietà** dal menu di scelta rapida. Verrà aperta la finestra di dialogo **Proprietà** della risorsa di SQL Server.  
  
4.  Selezionare la scheda **Proprietà** , immettere il valore desiderato per la proprietà **HealthCheckTimeout** , quindi fare clic su **OK** per applicare la modifica.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
 Utilizzando l'istruzione [ALTER Server Configuration](/sql/t-sql/statements/alter-server-configuration-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] , è possibile specificare il valore della proprietà HealthCheckTimeout.  
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
 Nell'esempio seguente l'opzione HealthCheckTimeout viene impostata su 15.000 millisecondi (15 secondi).  
  
```sql
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Criteri di failover per le istanze del cluster di failover](failover-policy-for-failover-cluster-instances.md)  
