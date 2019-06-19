---
title: Creare un Endpoint del mirroring per i gruppi di disponibilità AlwaysOn (SQL Server PowerShell) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], endpoint
ms.assetid: 6197bbe7-67d4-446d-ba5f-cabfa5df77f1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 77df7902f5dd1673736f4a993c4e29c50d7accc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62814667"
---
# <a name="create-a-database-mirroring-endpoint-for-alwayson-availability-groups-sql-server-powershell"></a>Creare un endpoint del mirroring del database per i gruppi di disponibilità AlwaysOn (SQL Server PowerShell)
  In questo argomento viene illustrato come creare un endpoint del mirroring del database che verrà utilizzato da [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite PowerShell.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  [Sicurezza](#Security)  
  
-   **Per creare un endpoint del mirroring del database usando:**  [PowerShell](#PowerShellProcedure)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
> [!IMPORTANT]  
>  L'algoritmo RC4 è deprecato. [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] È consigliabile utilizzare AES.  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione CREATE ENDPOINT o l'appartenenza al ruolo predefinito del server sysadmin. Per altre informazioni, vedere [GRANT - autorizzazioni per endpoint &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql).  
  
##  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
 **Per creare un endpoint del mirroring del database**  
  
1.  Spostarsi sulla directory (`cd`) dell'istanza del server per la quale creare l'endpoint del mirroring del database.  
  
2.  Utilizzare il cmdlet `New-SqlHadrEndpoint` per creare l'endpoint, quindi utilizzare `Set-SqlHadrEndpoint` per avviare l'endpoint.  
  
###  <a name="PShellExample"></a> Esempio (PowerShell)  
 I comandi di PowerShell seguenti creano un endpoint del mirroring del database in un'istanza di SQL Server (*Machine*\\*Instance*). L'endpoint utilizza la porta 5022.  
  
> [!IMPORTANT]  
>  Questo esempio funziona solo su un'istanza del server che attualmente non dispone di un endpoint del mirroring del database.  
  
```  
# Create the endpoint.  
$endpoint = New-SqlHadrEndpoint MyMirroringEndpoint -Port 5022 -Path SQLSERVER:\SQL\Machine\Instance  
  
# Start the endpoint  
Set-SqlHadrEndpoint -InputObject $endpoint -State "Started"  
  
```  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per configurare un endpoint del mirroring del database**  
  
-   [Creare un endpoint del mirroring del database per l'autenticazione Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Utilizzare certificati per un endpoint del mirroring del database &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [Impostare l'endpoint del mirroring del database per l'uso di certificati per le connessioni in uscita &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [Impostazione dell'endpoint del mirroring del database per l'utilizzo di certificati per le connessioni in ingresso &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Specificare un indirizzo di rete del server &#40;mirroring del database&#41;](../../database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Specificare l'URL dell'endpoint quando si aggiunge o si modifica una replica di disponibilità &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Per visualizzare informazioni sull'endpoint del mirroring del database**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un gruppo di disponibilità &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)   
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
