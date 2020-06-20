---
title: Configurare le impostazioni della proprietà FailureConditionLevel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 513dd179-9a46-46da-9fdd-7632cf6d0816
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8924b864d7cc8be078b370e3182713114f54ff6c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062522"
---
# <a name="configure-failureconditionlevel-property-settings"></a>Configurare le impostazioni della proprietà FailureConditionLevel
  Utilizzare la proprietà FailureConditionLevel per impostare le condizioni per il failover o il riavvio dell'istanza del cluster di failover AlwaysOn. Le modifiche apportate a questa proprietà vengono applicate immediatamente senza richiedere il riavvio del servizio cluster di failover di Windows Server (WSFC) o della risorsa istanza cluster di failover.  
  
-   **Prima di iniziare:**  [Impostazioni della proprietà FailureConditionLevel](#Restrictions), [Sicurezza](#Security)  
  
-   **Per configurare le impostazioni della proprietà FailureConditionLevel usando** [PowerShell](#PowerShellProcedure), [Gestione cluster di failover](#WSFC), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="failureconditionlevel-property-settings"></a><a name="Restrictions"></a> Impostazioni della proprietà FailureConditionLevel  
 Le condizioni di errore vengono impostate in base a un ordine crescente. In ognuno dei livelli 1-5 sono incluse tutte le condizioni dei livelli precedenti oltre alle proprie condizioni specifiche. Pertanto, in ogni livello la probabilità di un failover o di un riavvio è maggiore.  Per ulteriori informazioni, vedere la sezione "Determinazione di errori" nell'argomento [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md) .  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessario disporre delle autorizzazioni ALTER SETTINGS e VIEW SERVER STATE.  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
  
### <a name="to-configure-failureconditionlevel-settings"></a>Per configurare le impostazioni FailureConditionLevel  
  
1.  Avviare Windows PowerShell con privilegi elevati tramite **Esegui come amministratore**.  
  
2.  Importare il modulo `FailoverClusters` per abilitare i cmdlet del cluster.  
  
3.  Utilizzare il `Get-ClusterResource` cmdlet per trovare la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] risorsa, quindi utilizzare il `Set-ClusterParameter` cmdlet per impostare la proprietà **FailureConditionLevel** per un'istanza del cluster di failover.  
  
> [!TIP]  
>  Ogni volta che viene aperta una nuova finestra di PowerShell, è necessario importare il modulo `FailoverClusters`.  

 Nell'esempio seguente, l'impostazione FailureConditionLevel nella risorsa di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] "`SQL Server (INST1)`" viene impostata per eseguire il failover o il riavvio in caso di errori critici del server.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter FailureConditionLevel 3
```  
  
### <a name="related-content-powershell"></a>Contenuto correlato (PowerShell)  
  
-   [Clustering and High-Availability](https://techcommunity.microsoft.com/t5/failover-clustering/bg-p/FailoverClustering) (Failover Clustering and Network Load Balancing Team Blog) (Clustering e disponibilità elevata - Blog del team di clustering di failover e bilanciamento del carico di rete)  
  
-   [Introduzione a Windows PowerShell in un cluster di failover](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandi di risorse cluster e cmdlet di Windows PowerShell equivalenti](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="using-the-failover-cluster-manager-snap-in"></a><a name="WSFC"></a> Utilizzo dello snap-in Gestione cluster di failover  

### <a name="to-configure-failureconditionlevel-property-settings"></a>Per configurare le impostazioni delle proprietà FailureConditionLevel
  
1.  Aprire lo snap-in Gestione cluster di failover.  
  
2.  Espandere **Servizi e applicazioni** e selezionare l'istanza del cluster di failover.  
  
3.  Fare clic con il pulsante destro del mouse su **Risorsa di SQL Server** in **Altre risorse**, quindi, nel menu, selezionare **Proprietà** . Verrà aperta la finestra di dialogo **Proprietà** della risorsa di SQL Server.  
  
4.  Selezionare la scheda **Proprietà** , immettere il valore desiderato per la proprietà **FailureConditionLevel** , quindi fare clic su **OK** per applicare la modifica.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  

### <a name="to-configure-failureconditionlevel-property-settings"></a>Per configurare le impostazioni delle proprietà FailureConditionLevel
  
 Utilizzando l'istruzione [ALTER Server Configuration](/sql/t-sql/statements/alter-server-configuration-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] , è possibile specificare il valore della proprietà FailureConditionLevel.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Esempio (Transact-SQL)  
 Quando nel seguente esempio la proprietà FailureConditionLevel viene impostata su 0, viene indicato che con qualsiasi condizione di errore non verrà attivato automaticamente alcun failover o riavvio.  
  
```sql
ALTER SERVER CONFIGURATION SET FAILOVER CLUSTER PROPERTY FailureConditionLevel = 0;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_server_diagnostics &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)   
 [Criteri di failover per le istanze del cluster di failover](failover-policy-for-failover-cluster-instances.md)  
