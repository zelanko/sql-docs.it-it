---
title: Creare il catalogo SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6ed56d36-18d9-40c2-b51f-f2a4c71d1e73
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ae7f6128f14db0e1ccc423b5433744de7d3dc5d4
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922056"
---
# <a name="create-the-ssis-catalog"></a>Creare il catalogo SSIS
  Dopo avere progettato e testato i pacchetti in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], è possibile distribuire i progetti che contengono i pacchetti in un server di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Prima di poter distribuire i progetti nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], in quest'ultimo deve essere incluso il catalogo `SSISDB`. Tramite il programma di installazione per [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] non viene creato automaticamente il catalogo. Sarà necessario crearlo manualmente usando le istruzioni seguenti.  
  
 Il catalogo SSISDB può essere creato in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Il catalogo può essere creato anche a livello di programmazione utilizzando Windows PowerShell.  
  
### <a name="to-create-the-ssisdb-catalog-in-sql-server-management-studio"></a>Per creare il catalogo SSISDB in SQL Server Management Studio  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  Connettersi al motore di database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
3.  In Esplora oggetti espandere il nodo del server, fare clic con il pulsante destro del mouse sul nodo **Cataloghi di Integration Services** e quindi fare clic su **Creazione catalogo**.  
  
4.  Fare clic su **Abilitazione integrazione con CLR**.  
  
     Nel catalogo vengono utilizzate stored procedure CLR.  
  
5.  Fare clic su **Abilita l'esecuzione automatica della stored procedure di Integration Services all'avvio di SQL Server** per abilitare l'esecuzione della stored procedure [catalog.startup](/sql/integration-services/system-stored-procedures/catalog-startup) a ogni riavvio dell’istanza del server [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
     La stored procedure esegue la manutenzione dello stato delle operazioni per il catalogo SSISDB. Corregge lo stato di eventuali pacchetti in esecuzione in caso di arresto dell'istanza del server [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
6.  Immettere una password e quindi fare clic su **OK**.  
  
     La password consente di proteggere la chiave del database master utilizzata per crittografare i dati del catalogo. Salvare la password in un percorso sicuro. È consigliabile eseguire inoltre il backup della chiave master del database. Per altre informazioni, vedere [Backup della chiave master di un database](../relational-databases/security/encryption/back-up-a-database-master-key.md).  
  
### <a name="to-create-the-ssisdb-catalog-programmatically"></a>Per creare il catalogo SSISDB a livello di programmazione  
  
1.  Eseguire lo script di PowerShell seguente:  
  
    ```powershell
    # Load the IntegrationServices Assembly  
    [Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices")  
  
    # Store the IntegrationServices Assembly namespace to avoid typing it every time  
    $ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"  
  
    Write-Host "Connecting to server ..."  
  
    # Create a connection to the server  
    $sqlConnectionString = "Data Source=localhost;Initial Catalog=master;Integrated Security=SSPI;"  
    $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString  
  
    # Create the Integration Services object  
    $integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection  
  
    # Provision a new SSIS Catalog  
    $catalog = New-Object $ISNamespace".Catalog" ($integrationServices, "SSISDB", "P@assword1")  
    $catalog.Create()
    ```  
  
     Per altri esempi di come usare Windows PowerShell e lo spazio dei nomi <xref:Microsoft.SqlServer.Management.IntegrationServices>, vedere l'intervento sul blog relativo a [SSIS e PowerShell in SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=242539) nel sito blogs.msdn.com. Per una panoramica dello spazio dei nomi e degli esempi di codice, vedere l'intervento sul blog relativo a [uno sguardo rapido del modello a oggetti gestito del catalogo SSIS](https://techcommunity.microsoft.com/t5/sql-server-integration-services/a-glimpse-of-the-ssis-catalog-managed-object-model/ba-p/387892)sul sito blogs.msdn.com.  
  
## <a name="see-also"></a>Vedere anche  
 [Catalogo SSIS](catalog/ssis-catalog.md)   
 [Backup, ripristino e spostamento del catalogo SSISDB](../../2014/integration-services/backup-restore-and-move-the-ssis-catalog.md)  
