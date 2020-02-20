---
title: Aggiornare un'istanza del cluster di failover
description: Passaggi per aggiornare un'istanza del cluster di failover di SQL Server usando il supporto di installazione.
ms.custom: seo-lt-2019
ms.date: 11/21/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 24607a6372ba733165aa12fd159baea10f80ebd4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74822022"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance"></a>Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta l'aggiornamento di un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a una nuova versione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o a un nuovo Service Pack o aggiornamento cumulativo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], oppure quando si esegue l'installazione in un nuovo Service Pack o aggiornamento cumulativo di Windows separatamente in tutti i nodi cluster di failover, con tempo di inattività limitato a un singolo failover manuale (o due failover manuali in caso di failback alla replica primaria originale).  
  
 L'aggiornamento del sistema operativo Windows di un cluster di failover non è supportato per i sistemi operativi precedenti a [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)]. Per aggiornare un nodo del cluster in esecuzione in [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] o versioni successive, vedere [Eseguire un aggiornamento o un aggiornamento in sequenza](#perform-a-rolling-upgrade-or-update).  
  
 I dettagli relativi al supporto sono i seguenti:  
  
-   L'aggiornamento di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è supportato sia tramite l'interfaccia utente che al prompt dei comandi. È possibile eseguire l'aggiornamento dal prompt dei comandi in ogni nodo del cluster di failover o tramite l'interfaccia utente del programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per aggiornare ogni nodo del cluster.  Per altre informazioni, vedere [Aggiornare un'istanza del cluster di failover di SQL Server &#40;programma di installazione&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) e [Installare SQL Server dal prompt dei comandi](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
-   In un aggiornamento di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non sono supportati gli scenari seguenti:  
  
    -   Non è possibile eseguire l'aggiornamento da un'istanza autonoma di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un cluster di failover.  
  
    -   Non è possibile aggiungere funzionalità a un cluster di failover. Non è possibile ad esempio aggiungere il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] a un cluster di failover solo di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]esistente.  
  
    -   Non è possibile effettuare il downgrade di un nodo del cluster di failover a un'istanza autonoma.  
  
    -   La modifica dell'edizione del cluster di failover è limitata a determinati scenari. Per altre informazioni, vedere [Aggiornamenti di versione ed edizione supportati](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
-   Durante l'aggiornamento del cluster di failover, il tempo di inattività è limitato alla durata del failover e al tempo necessario per l'esecuzione degli script di aggiornamento. Se si segue il processo di aggiornamento in sequenza del cluster di failover indicato sotto e sono soddisfatti tutti i prerequisiti in tutti i nodi prima di iniziare il processo di aggiornamento, il tempo di inattività è minimo. L'aggiornamento di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando le tabelle ottimizzate per la memoria sono in uso richiede un tempo maggiore. Per altre informazioni, vedere [pianificare e testare il Database Engine Upgrade Plan](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Prima di iniziare, esaminare le informazioni seguenti:  
  
-   [Aggiornamenti di versione ed edizione supportati](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): verificare che sia possibile eseguire l'aggiornamento a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] dalla versione del sistema operativo Windows e di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in uso. Non è ad esempio possibile eseguire l'aggiornamento direttamente da un'istanza di clustering di failover di SQL Server 2005 a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] o aggiornare un cluster di failover in esecuzione in [!INCLUDE[winxpsvr-md](../../../includes/winxpsvr-md.md)].  
  
-   [Scegliere un metodo di aggiornamento del motore di database](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): selezionare il metodo e la procedura di aggiornamento appropriati in base alla verifica degli aggiornamenti della versione e dell'edizione supportate e anche agli altri componenti installati nell'ambiente interessato per aggiornare i componenti nell'ordine corretto.  
  
-   [Pianificare e testare il piano di aggiornamento del motore di database](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): esaminare le note sulla versione, i problemi di aggiornamento noti, l'elenco di controllo pre-aggiornamento e sviluppare e testare il piano di aggiornamento.  
  
-   [Requisiti hardware e software per l'installazione di SQL Server ](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md):  esaminare i requisiti software per l'installazione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Se è necessario software aggiuntivo, installarlo in ogni nodo prima di iniziare il processo di aggiornamento per ridurre al minimo eventuali tempi di inattività.  
  
## <a name="perform-a-rolling-upgrade-or-update"></a>Eseguire un aggiornamento o un aggiornamento in sequenza  
 Per aggiornare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per aggiornare i nodi del cluster di failover, uno alla volta, a partire dai nodi passivi. Man mano che viene aggiornato, ogni nodo viene escluso dai possibili proprietari del cluster di failover. In caso di failover imprevisto, i nodi aggiornati non partecipano al failover fino a quando la proprietà del gruppo di risorse del cluster non viene spostata in un nodo aggiornato dal programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Per impostazione predefinita, il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] determina automaticamente il momento in cui eseguire il failover a un nodo aggiornato, che dipende dal numero complessivo di nodi nell'istanza del cluster di failover e dal numero di nodi già aggiornati. Quando un numero di nodi uguale o maggiore della metà è già stato aggiornato, il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esegue il failover a un nodo aggiornato nel momento in cui si esegue l'aggiornamento del nodo successivo. In seguito al failover a un nodo aggiornato, il gruppo cluster viene spostato in un nodo aggiornato. Tutti i nodi aggiornati vengono inseriti nell'elenco dei possibili proprietari e tutti i nodi non ancora aggiornati vengono rimossi da tale elenco. Man mano che ne viene eseguito l'aggiornamento, ogni nodo rimanente viene aggiunto ai possibili proprietari del cluster di failover.  
  
 Questo processo comporta un tempo di inattività limitato alla durata del failover e al tempo di esecuzione degli script di aggiornamento del database durante l'aggiornamento dell'intero cluster di failover.  
  
 Per controllare il comportamento del failover dei nodi del cluster durante il processo di aggiornamento, eseguire l'operazione di aggiornamento nel prompt dei comandi e utilizzare il parametro /FAILOVERCLUSTERROLLOWNERSHIP. Per altre informazioni, vedere [Installazione di SQL Server dal prompt dei comandi](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  

 ## <a name="upgrade-with-installation-media"></a>Aggiornamento con supporto di installazione 
  
1.  Dal supporto di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] relativo all'edizione corrispondente a quella da aggiornare, fare doppio clic su setup.exe nella cartella radice. È possibile che venga richiesto di installare i prerequisiti se non sono già stati installati in precedenza.  
  
2.  Una volta installati i prerequisiti, l'Installazione guidata avvia Centro installazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per aggiornare un'istanza esistente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], selezionare l'istanza.  
  
3.  Se sono necessari, i file di supporto per l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verranno installati dal programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se viene richiesto, riavviare il computer prima di continuare.  
  
4.  Controllo configurazione sistema consente di eseguire un'operazione di individuazione nel computer. Per continuare, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
5.  Nella pagina relativa al codice Product Key immettere la chiave PID relativa all'edizione della nuova versione corrispondente all'edizione della versione precedente del prodotto. Per aggiornare un cluster di failover dell'edizione Enterprise, ad esempio, è necessario specificare una chiave PID per [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]. Fare clic su **Avanti** per continuare. Si noti che la chiave PID utilizzata per l'aggiornamento del cluster di failover deve essere coerente in tutti i nodi del cluster della stessa istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
6.  Nella pagina Condizioni di licenza leggere il contratto di licenza, quindi selezionare la casella di controllo per accettarne le condizioni. Per migliorare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è inoltre possibile abilitare l'opzione relativa all'utilizzo delle funzionalità e inviare report a [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Fare clic su**Avanti**per continuare. Per terminare l'installazione, fare clic su **Annulla**.  
  
7.  Nella pagina Seleziona istanza specificare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da aggiornare a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Fare clic su**Avanti**per continuare.  
  
8.  Nella pagina Selezione funzionalità le funzionalità da aggiornare saranno preselezionate. Dopo aver selezionato il nome della funzionalità desiderata, nel riquadro a destra verrà visualizzata una descrizione per ogni gruppo di componenti. Non è possibile modificare le funzionalità da aggiornare, né aggiungere funzionalità durante l'operazione di aggiornamento. Per aggiungere funzionalità a un'istanza aggiornata di [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] dopo aver completato l'aggiornamento, vedere [Aggiungere funzionalità a un'istanza di SQL Server 2016 &#40;programma di installazione&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md).  
  
     I prerequisiti per le funzionalità selezionate vengono visualizzati nel riquadro di destra. Il programma di installazione di SQL Server consentirà di installare i prerequisiti che non sono già stati installati durante la procedura di installazione descritta più avanti in questo argomento. Per risparmiare tempo, è consigliabile preinstallare questi prerequisiti nei singoli nodi.  
  
9. Nella pagina Configurazione dell'istanza i campi vengono compilati automaticamente in base ai valori dell'istanza precedente, ma è possibile specificare i valori relativi al nuovo ID istanza.  
  
     **ID istanza** : per impostazione predefinita, come ID istanza viene usato il nome dell'istanza. Tale nome viene utilizzato per identificare le directory di installazione e le chiavi del Registro di sistema per l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si tratta del caso delle istanze predefinite e delle istanze denominate. Per un'istanza predefinita, il nome di istanza e l'ID istanza sono MSSQLSERVER. Per utilizzare un ID istanza non predefinito, selezionare la casella di controllo **ID istanza** e specificare un valore. Se si sostituisce il valore predefinito, è necessario specificare lo stesso ID istanza per l'istanza da aggiornare in tutti i nodi del cluster di failover. L'ID istanza per l'istanza aggiornata deve corrispondere in tutti i nodi.  
  
     **Istanze e funzionalità rilevate** : nella griglia vengono visualizzate le istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] presenti nel computer in cui viene eseguito il programma di installazione. Fare clic su**Avanti**per continuare.  
  
10. Nella pagina Requisiti di spazio su disco viene calcolato lo spazio su disco necessario per le funzionalità specificate e vengono confrontati i requisiti con lo spazio su disco disponibile nel computer in cui è in esecuzione il programma di installazione.  
  
11. Nella pagina per l'aggiornamento della ricerca full-text specificare le opzioni per i database da aggiornare. Per altre informazioni, vedere [Opzioni di aggiornamento della ricerca full-text](https://msdn.microsoft.com/library/16c9376b-5fbb-4495-a429-06a2493849c9).  
  
12. Nella pagina **Segnalazione errori** specificare le informazioni da inviare a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] per contribuire a migliorare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per impostazione predefinita, l'opzione per la segnalazione di errori è abilitata.  
  
13. Controllo configurazione sistema eseguirà uno o più set di regole per convalidare la configurazione del computer con le funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] specificate prima dell'inizio dell'operazione di aggiornamento.  
  
14. Nella pagina Report aggiornamento cluster vengono visualizzati l'elenco dei nodi dell'istanza del cluster di failover e le informazioni sulla versione dell'istanza per i componenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in ogni nodo. In tale pagina vengono visualizzati lo stato degli script del database e di replica, nonché messaggi informativi sulle conseguenze dell'atto di scegliere **Avanti**. In base al numero di nodi del cluster di failover già aggiornati e al numero di nodi complessivo, verrà visualizzato il comportamento del failover quando si sceglie **Avanti**. Verranno inoltre visualizzati avvisi relativi al tempo di inattività potenziale non necessario nel caso in cui i prerequisiti non sia già installati.   
  
15. Nella pagina Inizio aggiornamento è presente una visualizzazione albero delle opzioni specificate durante l'installazione. Per continuare, fare clic su **Aggiorna**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verranno innanzitutto installati i prerequisiti obbligatori per le funzionalità selezionate e, successivamente, le funzionalità stesse.  
  
16. Durante l'aggiornamento, nella pagina Stato è possibile monitorare lo stato del processo di aggiornamento nel nodo corrente durante l'esecuzione del programma di installazione.  
  
17. Dopo l'aggiornamento del nodo corrente, nella pagina Report aggiornamento cluster vengono visualizzate le informazioni sullo stato dell'aggiornamento per tutti i nodi del cluster di failover, nonché le funzionalità di ogni nodo del cluster e le relative informazioni sulla versione. Confermare le informazioni sulla versione visualizzate e continuare con l'aggiornamento dei nodi rimanenti. Nella pagina relativa allo stato viene indicata anche l'eventuale esecuzione del failover sui nodi aggiornati. Per eseguire la conferma, è possibile inoltre effettuare la verifica tramite lo strumento Amministrazione cluster di Windows.  
  
18. Al termine dell'aggiornamento, nella pagina Operazione completata viene visualizzato un collegamento al file di log di riepilogo dell'installazione e ad altre note importanti. Per completare il processo di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , fare clic su **Chiudi**.  
  
19. Se viene richiesto, riavviare il computer. È importante leggere il messaggio visualizzato nell'Installazione guidata al termine dell'installazione. Per altre informazioni sui file di log del programma di installazione, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
20. Per completare il processo di aggiornamento, ripetere questi passaggi in tutti gli altri nodi del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="upgrade-a-multi-subnet-failover-cluster"></a>Aggiornare un cluster di failover su più subnet  

Seguire questi passaggi per aggiornare l'istanza del cluster di failover di SQL Server in un ambiente con più subnet. 
  
### <a name="to-upgrade-to-a-ssnoversion-multi-subnet-failover-cluster-existing-ssnoversion-cluster-is-a-non-multi-subnet-cluster"></a>Per effettuare l'aggiornamento a un cluster di failover su più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (il cluster di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esistente non è un cluster su più subnet)  
  
1.  Seguire le istruzioni precedenti per aggiornare il cluster.  
  
2.  Aggiungere un nodo su una subnet diversa utilizzando l'azione del programma di installazione AddNode e confermare la dipendenza delle risorse indirizzo IP su OR nella pagina **Configurazione rete cluster** . Per altre informazioni, vedere [Aggiungere o rimuovere nodi in un cluster di failover di SQL Server &#40;programma di installazione&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>Per aggiornare un cluster su più subnet utilizzando momentaneamente la tecnologia V-Lan estesa.  
  
1.  Seguire le istruzioni precedenti per aggiornare il cluster a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
2.  Modificare le impostazioni di rete per spostare il nodo remoto in una subnet diversa.  
  
3.  Utilizzando lo strumento di gestione del cluster di failover Windows, aggiungere un nuovo indirizzo IP per la nuova subnet e impostare la dipendenza delle risorse indirizzo IP su OR.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Al termine dell'aggiornamento a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], completare le attività seguenti:  
  
-   [Completare l'aggiornamento al motore di database](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
-   [Modificare la modalità di compatibilità del database e usare l'archivio query](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)  
  
-   [Vantaggi delle nuove funzionalità di SQL Server 2016](https://msdn.microsoft.com/library/d8879659-8efa-4442-bcbb-91272647ae16)  
  

  
  
