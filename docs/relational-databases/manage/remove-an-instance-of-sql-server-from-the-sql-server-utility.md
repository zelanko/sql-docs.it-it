---
title: Rimuovere un'istanza di SQL Server da Utilità SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.utility.remove.f1
ms.assetid: ae1d126a-46d2-47bf-b339-17c743df6491
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 785c056b50ed3594fe9886eb9c6a9ec79f7895c1
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908655"
---
# <a name="remove-an-instance-of-sql-server-from-the-sql-server-utility"></a>Rimuovere un'istanza di SQL Server da Utilità SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Usare i passaggi seguenti per rimuovere un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa procedura rimuove l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dalla visualizzazione elenco del punto di controllo dell'utilità e arresta la raccolta dati in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene disinstallata.  
  
> [!IMPORTANT]  
>  Prima di utilizzare questa procedura per rimuovere un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verificare che i servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e SQL Server Agent siano in esecuzione nell'istanza da rimuovere.  
  
1.  Da Esplora utilità in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]fare clic su **Istanze gestite**. Osservare la visualizzazione elenco delle istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel riquadro del contenuto di Esplora utilità.  
  
2.  Nella colonna **Nome istanza di SQL Server** della visualizzazione elenco selezionare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da rimuovere da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Fare clic con il pulsante destro del mouse sull'istanza da rimuovere e scegliere **Rimuovi istanza gestita**.  
  
3.  Specificare le credenziali con privilegi di amministratore per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: Fare clic su **Connetti**, verificare le informazioni nella finestra di dialogo **Connetti al server** e quindi fare clic su **Connetti**. Le informazioni di accesso verranno visualizzate nella finestra di dialogo **Rimuovi istanza gestita** .  
  
4.  Fare clic su **OK**per confermare l'operazione. Per uscire dall'operazione, scegliere **Annulla**.  

## <a name="manually-remove-a-managed-instance-of-sql-server-from-a-sql-server-utility"></a>Rimozione manuale di un'istanza gestita di SQL Server da un'Utilità SQL Server  
 Questa procedura rimuove l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dalla visualizzazione elenco del punto di controllo dell'utilità e arresta la raccolta dati in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene disinstallata.  
  
 È possibile usare PowerShell per rimuovere un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . lo script esegue le operazioni seguenti:  
  
-   Ottiene il punto di controllo dell'utilità tramite il nome dell'istanza del server.  
  
-   Rimuove l'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
```  
# Get Ucp connection  
$UcpServerInstanceName = "ComputerName\InstanceName";  
$UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $UcpServerInstanceName;  
$UcpConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($UcpConnection);  
  
# Now remove the ManagedInstance from the SQL Server Utility  
$ServerInstanceName = "ComputerName\InstanceName";  
$Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $ServerInstanceName;  
$InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
$ManagedInstance = $Utility.ManagedInstances[$ServerInstanceName];  
$ManagedInstance.Remove($InstanceConnection);  
```  
  
 Si tenga presente che è importante fare riferimento esattamente al nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come viene archiviato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Su un'istanza con distinzione tra maiuscole e minuscole di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessario specificare il nome dell'istanza usando la combinazione di maiuscole e minuscole esatta restituita da @@SERVERNAME. Per ottenere il nome dell'istanza per l'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], eseguire la seguente query sull'istanza gestita:  
  
```  
select @@SERVERNAME AS instance_name  
```  
  
 A questo punto, l'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene rimossa completamente dal punto di controllo dell'utilità. Al successivo aggiornamento dei dati per Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non risulterà più presente nella visualizzazione elenco. Il risultato è identico al caso in cui un utente esegue la rimozione dell'istanza gestita nell'interfaccia utente di SSMS.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di Esplora utilità per gestire Utilità SQL Server](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [Risoluzione dei problemi relativi a Utilità SQL Server](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
