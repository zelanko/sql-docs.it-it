---
title: Disinstallare un'istanza esistente di SQL Server (programma di installazione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- removing instances of SQL Server
- uninstalling instances of SQL Server
- removing SQL Server
- instances of SQL Server, uninstalling
- uninstalling SQL Server
ms.assetid: 3c64b29d-61d7-4b86-961c-0de62261c6a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 484ef7dead58a6e8ae35639cdc6218d5c8223bd9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62990194"
---
# <a name="uninstall-an-existing-instance-of-sql-server-setup"></a>Disinstallare un'istanza esistente di SQL Server (programma di installazione)
  In questo articolo viene descritto come disinstallare un'istanza autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I passaggi inclusi in questo argomento consentono inoltre di preparare il sistema per poter reinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Per disinstallare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario essere un amministratore locale che dispone dell'autorizzazione necessaria per accedere come servizio.  
  
> [!NOTE]  
>  Per disinstallare un cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilizzare la funzionalità per la rimozione del nodo disponibile nel programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per rimuovere ogni nodo singolarmente. Per altre informazioni, vedere [Aggiungere o rimuovere nodi in un cluster di failover di SQL Server &#40;programma di installazione&#41;](../failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
 Prima di disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], considerare le informazioni importanti seguenti:  
  
-   Prima di rimuovere i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un computer che soddisfa i requisiti minimi di memoria fisica, verificare che la dimensione del file di paging sia sufficiente. La dimensione del file di paging deve essere doppia rispetto alla quantità di memoria fisica. L'insufficienza di memoria virtuale può provocare una rimozione incompleta di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Se si dispone di più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser verrà automaticamente disinstallato quando viene disinstallata l'ultima istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
     Per disinstallare tutti i componenti di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è necessario disinstallare manualmente il componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser da **Programmi e funzionalità** nel **Pannello di controllo**.  
  
### <a name="before-you-uninstall"></a>Operazioni preliminari alla disinstallazione  
  
1.  **Eseguire il backup dei dati.** È possibile che siano presenti database da salvare nello stato attuale. Potrebbe inoltre essere necessario salvare le modifiche apportate ai database di sistema. Se si verifica una di queste situazioni, accertarsi di eseguire il backup dei dati prima di disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In alternativa è possibile salvare una copia di tutti i dati e di tutti i file di log in una cartella diversa da MSSQL. La cartella MSSQL viene eliminata durante la disinstallazione.  
  
     Nei file da salvare sono inclusi i file di database seguenti:  
  
    -   Master.mdf  
  
    -   Mastlog.ldf  
  
    -   Model.mdf  
  
    -   Modellog.ldf  
  
    -   Msdbdata.mdf  
  
    -   Msdblog.ldf  
  
    -   Mssqlsystemresource.mdf  
  
    -   Mssqlsustemresource.ldf  
  
    -   Tempdb.mdf  
  
    -   Templog.ldf  
  
    -   `ReportServer[$InstanceName]` (Thisis il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] database predefinito.)  
  
    -   ReportServer[$InstanceName]TempDB, ovvero il database temporaneo predefinito di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  **Eliminare i gruppi di sicurezza locali.** Prima di disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], eliminare i gruppi di sicurezza locali per i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  **Arrestare tutti i** **servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** . Prima di disinstallare i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è consigliabile arrestare tutti i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le connessioni attive possono impedire la corretta esecuzione della disinstallazione.  
  
4.  **Utilizzare un account dotato di autorizzazioni appropriate.** Accedere al server utilizzando l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un account che dispone di autorizzazioni equivalenti. È possibile, ad esempio, accedere al server utilizzando un account membro del gruppo di amministratori locali.  
  
### <a name="to-uninstall-an-instance-of-includessnoversionincludesssnoversion-mdmd"></a>To Uninstall an Instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  Per avviare il processo di disinstallazione, nel **Pannello di controllo** scegliere **Programmi e funzionalità**.  
  
2.  Fare clic destro **[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** e selezionare **Disinstalla**. Fare clic su **Rimuovi**. Verrà avviata l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Verranno eseguite le regole di supporto dell'installazione per verificare la configurazione del computer. Scegliere **Avanti**per continuare.  
  
3.  Nella pagina Seleziona istanza utilizzare la casella di riepilogo a discesa per specificare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da rimuovere o indicare l'opzione per rimuovere solo gli strumenti di gestione e le funzionalità condivise di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Scegliere **Avanti**per continuare.  
  
4.  Nella pagina Seleziona funzionalità specificare le funzionalità da rimuovere dall'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Verranno eseguite le regole di rimozione per verificare l'esecuzione corretta dell'operazione.  
  
5.  Nella pagina **Inizio rimozione** esaminare l'elenco dei componenti e delle funzionalità che verranno disinstallate. Fare clic su **Rimuovi** per avviare la disinstallazione.  
  
6.  Immediatamente dopo la disinstallazione dell'ultima istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , gli altri programmi associati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] saranno ancora visibili nell'elenco dei programmi in **Programmi e funzionalità**. Tuttavia, se si chiude **Programmi e funzionalità**, alla successiva apertura di **Programmi e funzionalità**, l'elenco dei programmi verrà aggiornato per visualizzare solo i programmi ancora installati.  
  
### <a name="if-the-uninstallation-fails"></a>Se la disinstallazione non viene completata  
  
1.  Se il processo di disinstallazione non viene completato correttamente, tentare di eliminare la causa del problema. Gli articoli seguenti possono aiutare a individuare la causa della mancata disinstallazione:  
  
    -   [Come identificare i problemi del programma di installazione di SQL Server 2008 nei file di log dell'installazione](https://support.microsoft.com/kb/955396/en-us)  
  
    -   [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
2.  Se non è possibile eliminare la causa del problema di disinstallazione, contattare il Supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] . In alcuni casi, ad esempio quando si eliminano inavvertitamente file importanti, la reinstallazione del sistema operativo può essere necessaria per reinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel computer.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
