---
title: Eseguire l'aggiornamento a SQL Server 2014 usando l'installazione guidata (programma di installazione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- upgrading Database Engine
- Database Engine [SQL Server], upgrading
ms.assetid: cef118a5-a7ce-4bfa-8b9d-c81996284cfc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8330702d8c886cc9197dcd944878c3f794780205
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775407"
---
# <a name="upgrade-to-sql-server-2014-using-the-installation-wizard-setup"></a>Eseguire l'aggiornamento a SQL Server 2014 utilizzando l'Installazione guidata (programma di installazione)
  Nell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile un singolo albero delle funzionalità per aggiornare i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È inoltre possibile eseguire l'installazione side-by-side di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a una versione precedente oppure eseguire la migrazione di database e impostazioni di configurazione esistenti da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e applicarli a un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [Aggiornamenti di versione ed edizione supportati](supported-version-and-edition-upgrades.md)  
  
-   [Usare più versioni e istanze di SQL Server](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
  
-   [Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server &#40;installazione&#41;](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
-   [Installazione di SQL Server 2014 dal prompt dei comandi](install-sql-server-from-the-command-prompt.md)  
  
-   [Usare Copia guidata database](../../relational-databases/databases/use-the-copy-database-wizard.md)  
  
> [!NOTE]  
>  In un computer in cui viene eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Server Core SP1 non è supportato l'aggiornamento di una versione precedente di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]. Per altre informazioni sulle installazioni Server Core, vedere [installare SQL Server 2014 in Server Core](install-sql-server-on-server-core.md).  
  
## <a name="prerequisites"></a>Prerequisiti  
 È necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio che disponga di autorizzazioni di lettura ed esecuzione per questa condivisione remota e che a eseguire l'operazione sia un amministratore locale.  
  
 Prima di aggiornare il [!INCLUDE[ssDE](../../includes/ssde-md.md)], vedere gli argomenti seguenti:  
  
-   [Aggiornamento a SQL Server 2014](upgrade-sql-server.md)  
  
-   [Requisiti hardware e software per l'installazione di SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [Parametri di controllo di Controllo configurazione sistema](check-parameters-for-the-system-configuration-checker.md)  
  
-   [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [Compatibilità con le versioni precedenti del motore di database di SQL Server](../sql-server-database-engine-backward-compatibility.md)  
  
> [!WARNING]  
>  Non è possibile modificare le funzionalità da aggiornare, né aggiungere funzionalità durante l'operazione di aggiornamento. Per altre informazioni su come aggiungere funzionalità a un'istanza aggiornata del [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] una volta completata l'operazione di aggiornamento, vedere [aggiunta di caratteristiche a un'istanza di SQL Server 2014 &#40;installazione&#41;](add-features-to-an-instance-of-sql-server-setup.md).  
  
## <a name="procedure"></a>Routine  
  
#### <a name="to-upgrade-to-includesscurrentincludessscurrent-mdmd"></a>Per eseguire l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Inserire il supporto di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , quindi nella cartella radice fare doppio clic sul file Setup.exe. Per eseguire l'installazione da una condivisione di rete, passare alla cartella radice nella condivisione, quindi fare doppio clic sul file Setup.exe.  
  
2.  L'Installazione guidata consente di avviare il Centro installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per aggiornare un'istanza esistente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], fare clic su **Installazione** nell'area di navigazione a sinistra, quindi fare clic su **Aggiorna da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]**.  
  
3.  Nella pagina relativa al codice Product Key selezionare un'opzione per indicare se si intende eseguire l'aggiornamento a un'edizione gratuita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o se si dispone di una chiave PID per una versione di produzione del prodotto. Per altre informazioni, vedere [edizioni e componenti di SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) e [Supported Version and Edition Upgrades](supported-version-and-edition-upgrades.md).  
  
4.  Nella pagina Condizioni di licenza leggere il contratto di licenza e, per accettare, selezionare la casella di controllo **Accetto le condizioni di licenza** , quindi fare clic su **Avanti**. Per migliorare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è inoltre possibile abilitare l'opzione relativa all'utilizzo delle funzionalità e inviare report a [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
5.  Nella finestra Regole globali, con la procedura di installazione si passerà automaticamente alla finestra Aggiornamenti prodotti se non vi sono errori di regole.  
  
6.  La pagina di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update verrà visualizzata successivamente se la casella di controllo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update non è selezionata in Pannello di controllo\Tutti gli elementi del Pannello di controllo\Windows Update\Modifica impostazioni. Se si seleziona la pagina [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, le impostazioni del computer vengono modificate per includere gli aggiornamenti quando si effettua l'analisi di Windows Update.  
  
7.  Nella pagina Aggiornamenti prodotto vengono visualizzati gli aggiornamenti più recenti sul prodotto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se non si vogliono includere gli aggiornamenti, deselezionare la casella di controllo **Includi aggiornamenti prodotto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. Se non viene individuato alcun aggiornamento del prodotto, durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa pagina non viene visualizzata e viene aperta automaticamente la pagina **Installazione dei file di installazione** .  
  
8.  Nella pagina Installazione dei file di installazione viene mostrato lo stato del download, dell'estrazione e dell'installazione dei file di installazione. Se viene individuato un aggiornamento per il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ne viene specificata l'inclusione, verrà installato anche questo aggiornamento.  
  
9. Nella finestra Regole di aggiornamento, con la procedura di installazione si passerà automaticamente alla finestra Seleziona istanza se non vi sono errori di regole.  
  
10. Nella pagina Seleziona istanza specificare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da aggiornare. Per aggiornare gli strumenti di gestione e le funzionalità condivise, selezionare **Aggiorna solo le funzionalità condivise**.  
  
11. Nella pagina Seleziona funzionalità le funzionalità da aggiornare saranno preselezionate. Dopo aver selezionato il nome della funzionalità desiderata, nel riquadro a destra verrà visualizzata una descrizione per ogni gruppo di componenti.  
  
     I prerequisiti per le funzionalità selezionate vengono visualizzati nel riquadro di destra. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno installati i prerequisiti che non sono stati ancora installati durante la procedura di installazione descritta più avanti in questo argomento.  
  
    > [!NOTE]  
    >  Se si è scelto di aggiornare le funzionalità condivise selezionando **\<Aggiorna solo le funzionalità condivise>** nella pagina **Seleziona istanza**, tutte le funzionalità condivise sono preselezionate nella pagina Selezione funzionalità. Tutti i componenti condivisi vengono aggiornati contemporaneamente.  
  
12. Nella pagina Configurazione istanza specificare l'ID istanza per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **ID istanza** : per impostazione predefinita, come ID istanza viene usato il nome dell'istanza. Tale nome viene utilizzato per identificare le directory di installazione e le chiavi del Registro di sistema per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si tratta del caso delle istanze predefinite e delle istanze denominate. Per un'istanza predefinita, il nome di istanza e l'ID istanza sono MSSQLSERVER. Per utilizzare un ID istanza non predefinito, specificare un valore per la casella di testo **ID istanza** .  
  
     Tutti i Service Pack e gli aggiornamenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno applicati a ogni componente di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **Istanze installate**: la griglia visualizzerà le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presenti nel computer in cui viene eseguita l'installazione. Se nel computer è già installata un'istanza predefinita, è necessario installare un'istanza denominata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
13. Il flusso di lavoro relativo alla parte rimanente di questo argomento dipende dalle funzionalità specificate per l'installazione. Le pagine visualizzate dipendono dalle selezioni effettuate.  
  
14. Nella pagina Configurazione server - Account di servizio vengono visualizzati gli account del servizio predefiniti per i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I servizi effettivamente configurati in questa pagina dipendono dalle funzionalità sottoposte ad aggiornamento.  
  
     Le informazioni relative all'autenticazione e all'accesso verranno trasferite dall'istanza precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile assegnare lo stesso account di accesso a tutti i servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure configurare singolarmente l'account di ogni servizio. È inoltre possibile specificare se i servizi verranno avviati automaticamente, manualmente o se sono disabilitati. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di configurare singolarmente gli account del servizio in modo da garantire ai servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le autorizzazioni minime necessarie per completare le attività. Per altre informazioni, vedere [Configurare account di servizio e autorizzazioni di Windows](../configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Per specificare lo stesso account di accesso per tutti gli account del servizio nell'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], immettere le credenziali nei campi visualizzati nella parte inferiore della pagina.  
  
     **Nota sulla sicurezza** [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     Dopo aver specificato le informazioni di accesso per i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fare clic su **Avanti**.  
  
15. Nella pagina Opzioni di aggiornamento della ricerca full-text specificare le opzioni per i database da aggiornare. Per altre informazioni, vedere [Opzioni di aggiornamento della ricerca full-text](../../sql-server/install/full-text-search-upgrade-options.md).  
  
16. Se tutte le regole vengono soddisfatte si procede automaticamente dalla finestra Regole funzionalità.  
  
17. Nella pagina Inizio aggiornamento è presente una visualizzazione albero delle opzioni specificate durante l'installazione. Per continuare, fare clic su **Installa**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno innanzitutto installati i prerequisiti obbligatori per le funzionalità selezionate e, successivamente, le funzionalità stesse.  
  
18. Durante l'installazione, nella pagina relativa allo stato è possibile monitorare lo stato di avanzamento dell'installazione.  
  
19. Al termine dell'installazione nella pagina Operazione completata viene visualizzato un collegamento al file di log di riepilogo del processo di installazione e ad altre note importanti. Per completare il processo di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fare clic su **Chiudi**.  
  
20. Se viene richiesto, riavviare il computer. È importante leggere il messaggio visualizzato nell'Installazione guidata al termine dell'installazione. Per altre informazioni sui file di log del programma di installazione, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Passaggi successivi  
 Al termine dell'aggiornamento a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], completare le attività seguenti:  
  
-   **Registrare i server**: dato che l'operazione di aggiornamento rimuove le impostazioni del Registro di sistema per la precedente istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in seguito all'aggiornamento è necessario registrare nuovamente i server.  
  
-   **Aggiornare le statistiche**: per ottimizzare le prestazioni delle query, dopo l'aggiornamento è consigliabile aggiornare le statistiche per tutti i database. Utilizzare la stored procedure `sp_updatestats` per aggiornare le statistiche nelle tabelle definite dall'utente dei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Configurare la nuova installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: per ridurre la superficie di attacco di un sistema, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono installati e abilitati in modo selettivo i servizi e le funzionalità principali. Per ulteriori informazioni sulla configurazione della superficie di attacco, vedere il file Leggimi per questa versione.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire l'aggiornamento a SQL Server 2014](upgrade-sql-server.md)   
 [Compatibilità con le versioni precedenti](../../getting-started/backward-compatibility.md)  
  
  
