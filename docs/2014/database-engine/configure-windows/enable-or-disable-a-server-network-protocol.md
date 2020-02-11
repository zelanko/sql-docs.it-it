---
title: Abilitare o disabilitare un protocollo di rete del server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- network protocols [SQL Server], disabling
- remote connections [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], disabling using Configuration Manager
- disabling network protocols, Configuration Manager
- network protocols [SQL Server], enabling
- enabling network protocols, Configuration Manager
- surface area configuration [SQL Server], connection protocols
- connections [SQL Server], enabling remote using Configuration Manager
ms.assetid: ec5ccb69-61c9-4576-8843-014b976fd46e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 917abf00789cfca75ee6edb52ffef07832bfe981
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783034"
---
# <a name="enable-or-disable-a-server-network-protocol"></a>Abilitare o disabilitare un protocollo di rete del server
  Tutti i protocolli di rete vengono installati dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ma è possibile abilitarli o meno. In questo argomento viene descritto come abilitare o disabilitare un protocollo di rete del server in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o PowerShell. Per rendere effettive le modifiche, è necessario arrestare e riavviare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
> [!IMPORTANT]  
>  Durante l'installazione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] viene aggiunto un account di accesso per il gruppo BUILTIN\Users. In questo modo, tutti gli utenti autenticati del computer possono accedere all'istanza di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] come un membro del ruolo pubblico. L'account di accesso BUILTIN\Users può essere rimosso in sicurezza per limitare l'accesso del [!INCLUDE[ssDE](../../includes/ssde-md.md)] agli utenti di computer che dispongono di account di accesso singoli o sono membri di altri gruppi di Windows con account di accesso.  
  
> [!WARNING]  
>  I provider di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)] per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportano TLS 1.0 e SSL 3.0. Se si applica un protocollo diverso, ad esempio TLS 1.1 o TLS 1.2, apportando modifiche nel livello SChannel del sistema operativo, le connessioni a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbero non riuscire.  
  
 **Contenuto dell'articolo**  
  
-   **Per abilitare o disabilitare un protocollo di rete del server utilizzando:**  
  
     [Gestione configurazione SQL Server](#SSMSProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="to-enable-a-server-network-protocol"></a>Per abilitare un protocollo di rete del server  
  
1.  Nel riquadro della console di Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espandere **Configurazione di rete SQL Server**.  
  
2.  Nel riquadro della console fare clic su **protocolli per** * \<nome istanza>*.  
  
3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse sul protocollo da modificare e quindi scegliere **Abilita** o **Disabilita**.  
  
4.  Nel riquadro della console fare clic su **Servizi di SQL Server**.  
  
5.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **SQL Server (***\<nome istanza>***)**, quindi scegliere **Riavvia** per arrestare e riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="PowerShellProcedure"></a>Utilizzo di SQL Server PowerShell  
  
#### <a name="to-enable-a-server-network-protocol-using-powershell"></a>Per abilitare un protocollo di rete del server utilizzando PowerShell  
  
1.  Aprire un prompt dei comandi con autorizzazioni di amministratore.  
  
2.  Avviare Windows PowerShell 2.0 dalla barra delle applicazioni oppure fare clic su Start, Tutti i programmi, Accessori, Windows PowerShell e quindi ancora Windows PowerShell.  
  
3.  Importare il modulo **sqlps** immettendo`Import-Module "sqlps"`  
  
4.  Eseguire le seguenti istruzioni per abilitare i protocolli TCP e Named Pipes. Sostituire `<computer_name>` con il nome del computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si configura un'istanza denominata, sostituire `MSSQLSERVER` con il nome dell'istanza.  
  
     Per disabilitare i protocolli, impostare le proprietà `IsEnabled` su `$false`.  
  
    ```powershell
    $smo = 'Microsoft.SqlServer.Management.Smo.'  
    $wmi = new-object ($smo + 'Wmi.ManagedComputer').  
  
    # List the object properties, including the instance names.  
    $Wmi  
  
    # Enable the TCP protocol on the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    $Tcp = $wmi.GetSmoObject($uri)  
    $Tcp.IsEnabled = $true  
    $Tcp.Alter()  
    $Tcp  
  
    # Enable the named pipes protocol for the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Np']"  
    $Np = $wmi.GetSmoObject($uri)  
    $Np.IsEnabled = $true  
    $Np.Alter()  
    $Np  
    ```  
  
#### <a name="to-configure-the-protocols-for-the-local-computer"></a>Per configurare i protocolli per il computer locale  
  
-   Quando lo script viene eseguito localmente e configura il computer locale, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell offre una maggiore flessibilità per lo script determinando dinamicamente il nome del computer locale. Per recuperare il nome del computer locale, sostituire la riga che imposta la variabile `$uri` con la riga seguente.  
  
    ```powershell
    $uri = "ManagedComputer[@Name='" + (Get-Item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    ```  
  
#### <a name="to-restart-the-database-engine-by-using-sql-server-powershell"></a>Per riavviare il Motore di database tramite SQL Server PowerShell  
  
-   Dopo aver disabilitato o abilitato i protocolli, è necessario arrestare e riavviare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] per rendere effettiva la modifica. Eseguire le istruzioni seguenti per arrestare e avviare l'istanza predefinita tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Per arrestare e avviare un'istanza denominata, sostituire `'MSSQLSERVER'` con `'MSSQL$<instance_name>'`.  
  
    ```powershell
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\<computer_name>  
    $Wmi = (Get-Item .).ManagedComputer  
    # Get a reference to the default instance of the Database Engine.  
    $DfltInstance = $Wmi.Services['MSSQLSERVER']  
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Start the service again.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache and display the state of the service.  
    $DfltInstance.Refresh(); $DfltInstance  
    ```  
