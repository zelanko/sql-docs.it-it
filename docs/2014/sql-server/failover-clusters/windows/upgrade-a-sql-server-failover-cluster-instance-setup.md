---
title: Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server (programma di installazione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d018fb391c7633877f985b4e5e0798bfd803a5fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62680372"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server (installazione)
  Per aggiornare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un cluster di failover di [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], è possibile utilizzare l'Installazione guidata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o il prompt dei comandi.  
  
 Durante l'aggiornamento del cluster di failover, il tempo di inattività è limitato alla durata del failover e al tempo necessario per l'esecuzione degli script di aggiornamento. Se si segue il processo di aggiornamento in sequenza del cluster di failover, il tempo di inattività è minimo. In base alla disponibilità dei prerequisiti nei nodi del cluster di failover, è possibile che durante l'installazione di tali prerequisiti il tempo di inattività sia maggiore. Per ulteriori informazioni su come ridurre al minimo il tempo di inattività durante l'aggiornamento, vedere la sezione [procedure consigliate prima dell'aggiornamento del cluster di failover](#BestPractices) in questa pagina.  
  
 Per ulteriori informazioni su come eseguire l'aggiornamento, vedere [aggiornamenti di versione ed edizione supportati](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md) ed [eseguire l'aggiornamento a SQL Server 2014](../../../database-engine/install-windows/upgrade-sql-server.md).  
  
 Per ulteriori informazioni sulla sintassi di esempio per l'utilizzo del prompt dei comandi, vedere [Install SQL Server 2014 dal prompt dei comandi](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Prima di iniziare, esaminare le informazioni seguenti:  
  
-   [Operazioni preliminari all'installazione del clustering di failover](../install/before-installing-failover-clustering.md)  
  
-   [Utilizzare Preparazione aggiornamento per preparare gli aggiornamenti](../../install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
-   [Aggiornare il motore di database](../../../database-engine/install-windows/upgrade-database-engine.md)  
  
-   Il programma di installazione consente di installare .NET Framework 4.0 in un sistema operativo di tipo cluster. Per ridurre il tempo di inattività, si consideri di installare .NET Framework 4.0 prima di eseguire il programma di installazione.  
  
-   Per garantire la corretta installazione del componente Visual Studio, per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è necessaria l'installazione di un aggiornamento. Il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verifica la presenza di tale aggiornamento, quindi richiede di scaricarlo e installarlo prima che sia possibile procedere all'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per evitare l'interruzione dell'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , è possibile scaricare e installare l'aggiornamento prima di avviare l'operazione di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , come illustrato di seguito (o installare tutti gli aggiornamenti per .NET 3.5 SP1 disponibili in Windows Update).  
  
     Se si installa [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] in un computer con il sistema operativo Windows Server 2008 SP2, è possibile ottenere l'aggiornamento necessario da [qui](https://go.microsoft.com/fwlink/?LinkId=198093)  
  
     Se si installa [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] in un computer con il sistema operativo [!INCLUDE[win7](../../../includes/win7-md.md)] SP1 o [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] SP1, questo aggiornamento è incluso.  
  
-   .NET Framework 3.5 SP1 non viene più installato dal programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], tuttavia può essere richiesto durante l'istallazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)]. Per ulteriori informazioni, vedere [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] [Note sulla versione](https://go.microsoft.com/fwlink/?LinkId=296445).  
  
-   Per le installazioni locali, è necessario eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura per tale condivisione.  
  
-   Per aggiornare un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] cluster di failover di, l'istanza da aggiornare deve essere un cluster di failover di.  
  
     Per spostare un'istanza autonoma di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un cluster di failover di [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], installare un nuovo cluster di failover di [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], quindi eseguire la migrazione dei database utente dall'istanza autonoma tramite la Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="rolling-upgrades"></a>Aggiornamenti in sequenza  
 Per aggiornare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], è necessario eseguire il programma di installazione con l'azione di aggiornamento in ogni nodo del cluster di failover, uno alla volta, a partire dai nodi passivi. Man mano che viene aggiornato, ogni nodo viene escluso dai possibili proprietari del cluster di failover. In caso di failover imprevisto, i nodi aggiornati non partecipano al failover fino a quando la proprietà del gruppo di risorse del cluster non viene spostata in un nodo aggiornato dal programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Per impostazione predefinita, il programma di installazione determina automaticamente il momento in cui eseguire il failover a un nodo aggiornato, che dipende dal numero complessivo di nodi nell'istanza del cluster di failover e dal numero di nodi già aggiornati. Quando un numero di nodi uguale o maggiore della metà è già stato aggiornato, verrà eseguito un failover a un nodo aggiornato nel momento in cui si esegue l'aggiornamento del nodo successivo. In seguito al failover a un nodo aggiornato, il gruppo cluster viene spostato in un nodo aggiornato. Tutti i nodi aggiornati vengono inseriti nell'elenco dei possibili proprietari e tutti i nodi non ancora aggiornati vengono rimossi da tale elenco. Man mano che ne viene eseguito l'aggiornamento, ogni nodo rimanente viene aggiunto ai possibili proprietari del cluster di failover.  
  
 Questo processo comporta un tempo di inattività limitato alla durata del failover e al tempo di esecuzione degli script di aggiornamento del database durante l'aggiornamento dell'intero cluster di failover.  
  
 Per controllare il comportamento del failover dei nodi del cluster durante il processo di aggiornamento, eseguire l'operazione di aggiornamento nel prompt dei comandi e utilizzare il parametro /FAILOVERCLUSTERROLLOWNERSHIP. Per altre informazioni, vedere [Installare SQL Server 2014 dal prompt dei comandi](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
 **Nota** Se è presente un cluster di failover a nodo singolo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , il gruppo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di risorse viene portato offline dal programma di installazione.  
  
## <a name="considerations-when-upgrading-from-includessversion2005includesssversion2005-mdmd"></a>Considerazioni per l'esecuzione dell'aggiornamento da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]  
 Se sono stati specificati gruppi di domini per i criteri di sicurezza cluster, non è possibile specificare il SID del servizio in [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]. Se si desidera utilizzare il SID del servizio, è necessario un aggiornamento side-by-side.  
  
 Quando si seleziona il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] per l'aggiornamento, la ricerca full-text è inclusa nel programma di installazione indipendentemente dal fatto che sia installata o meno in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Se la ricerca full-text era abilitata in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], durante l'esecuzione del programma di installazione il catalogo di ricerca full-text viene ricompilato indipendentemente dalle opzioni disponibili.  
  
## <a name="upgrading-to-a-includesssql14includessssql14-mdmd-multi-subnet-failover-cluster"></a>Aggiornamento a un cluster di failover su più subnet di [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]  
 Esistono due possibili scenari di aggiornamento:  
  
1.  Il cluster di failover di[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è attualmente configurato su una singola subnet. È necessario aggiornare il cluster esistente a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] avviando il programma di installazione e seguendo il processo di aggiornamento. Dopo aver completato l'aggiornamento del cluster di failover esistente, aggiungere un nodo che si trova su una subnet diversa utilizzando la funzionalità AddNode. Confermare l'impostazione della dipendenza delle risorse indirizzo IP su OR nella pagina di configurazione della rete cluster. A questo punto è disponibile un cluster di failover su più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
2.  Cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] attualmente configurato su più subnet utilizzando la tecnologia V-LAN estesa. È necessario innanzitutto aggiornare il cluster esistente a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. Dal momento che la tecnologia V-LAN estesa consente di configurare una singola subnet, la configurazione della rete deve essere impostata su più subnet. Inoltre, è necessario modificare la dipendenza delle risorse indirizzo IP utilizzando lo strumento di amministrazione del cluster di failover Windows e impostare la dipendenza IP su OR.  
  
###  <a name="BestPractices"></a>Procedure consigliate prima dell' [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aggiornamento di un cluster di failover  
 Per eliminare il tempo di inattività imprevisto provocato da un riavvio, preinstallare il pacchetto che non richiede il riavvio di .NET Framework 4.0 in tutti i nodi del cluster di failover prima di eseguire l'aggiornamento nei nodi del cluster. Per preinstallare i prerequisiti, è consigliabile effettuare le operazioni seguenti:  
  
-   Installare il pacchetto che non richiede il riavvio di .NET Framework 4.0 e aggiornare solo i componenti condivisi, a partire dai nodi passivi. In questo modo verranno installati [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 4.0, Windows Installer 4.5 e i file di supporto di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Riavviare una o più volte, in base alle esigenze.  
  
-   Eseguire il failover a un nodo aggiornato.  
  
-   Aggiornare i componenti condivisi nell'ultimo nodo rimanente.  
  
 Dopo avere aggiornato tutti i componenti condivisi e avere installato i prerequisiti, avviare il processo di aggiornamento del cluster di failover. È necessario eseguire l'aggiornamento in ogni nodo del cluster di failover, a partire dai nodi passivi e continuando con il nodo proprietario del gruppo di risorse cluster.  
  
-   Non è possibile aggiungere funzionalità a un cluster di failover esistente.  
  
-   La modifica dell'edizione del cluster di failover è limitata a determinati scenari. Per ulteriori informazioni, vedere [aggiornamenti di versione ed edizione supportati](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
##  <a name="UpgradeSteps"></a>Per aggiornare un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cluster di failover  
  
#### <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>Per aggiornare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
1.  Inserire il supporto di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , quindi nella cartella radice fare doppio clic sul file Setup.exe. Per eseguire l'installazione da una condivisione di rete, passare alla cartella radice nella condivisione, quindi fare doppio clic sul file Setup.exe. È possibile che venga richiesto di installare i prerequisiti se non sono già stati installati in precedenza.  
  
2.  > [!IMPORTANT]  
    >  Per ulteriori informazioni sui passaggi 3 e 4, vedere la sezione [procedure consigliate prima dell'aggiornamento del cluster di failover](#BestPractices) .  
  
3.  Una volta installati i prerequisiti, l'Installazione guidata avvia Centro installazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per aggiornare un'istanza esistente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], fare clic su **Aggiorna [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]da [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)],, [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]o.**  
  
4.  Se sono necessari, i file di supporto per l'installazione verranno installati dal programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se viene richiesto, riavviare il computer prima di continuare.  
  
5.  Controllo configurazione sistema consente di eseguire un'operazione di individuazione nel computer. Per continuare, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
6.  Nella pagina relativa al codice Product Key immettere la chiave PID relativa all'edizione della nuova versione corrispondente all'edizione della versione precedente del prodotto. Per aggiornare un cluster di failover dell'edizione Enterprise, ad esempio, è necessario specificare una chiave PID per [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]. Fare clic su **Avanti** per continuare. Si noti che la chiave PID utilizzata per l'aggiornamento del cluster di failover deve essere coerente in tutti i nodi del cluster della stessa istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per ulteriori informazioni, vedere [edizioni e componenti di SQL Server 2014](../../editions-and-components-of-sql-server-2016.md) e [aggiornamenti di versione ed edizione supportati](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
7.  Nella pagina Condizioni di licenza leggere il contratto di licenza, quindi selezionare la casella di controllo per accettarne le condizioni. Per migliorare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è inoltre possibile abilitare l'opzione relativa all'utilizzo delle funzionalità e inviare report a [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. **Fare clic su Avanti per continuare**. Per terminare l'installazione, fare clic su **Annulla**.  
  
8.  Nella pagina Seleziona istanza specificare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da aggiornare a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. **Fare clic su Avanti per continuare**.  
  
9. Nella pagina Selezione funzionalità le funzionalità da aggiornare saranno preselezionate. Dopo aver selezionato il nome della funzionalità desiderata, nel riquadro a destra verrà visualizzata una descrizione per ogni gruppo di componenti. Non è possibile modificare le funzionalità da aggiornare, né aggiungere funzionalità durante l'operazione di aggiornamento. Per aggiungere funzionalità a un'istanza aggiornata di [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] al termine dell'operazione di aggiornamento, vedere [aggiungere funzionalità a un'istanza di SQL Server 2014 &#40;&#41;di installazione ](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md).  
  
     I prerequisiti per le funzionalità selezionate vengono visualizzati nel riquadro di destra. Il programma di installazione di SQL Server consentirà di installare i prerequisiti che non sono già stati installati durante la procedura di installazione descritta più avanti in questo argomento.  
  
10. Nella pagina Configurazione dell'istanza i campi vengono compilati automaticamente in base ai valori dell'istanza precedente, ma è possibile specificare i valori relativi al nuovo ID istanza.  
  
     **ID istanza** : per impostazione predefinita, il nome dell'istanza viene usato come ID istanza. Tale nome viene utilizzato per identificare le directory di installazione e le chiavi del Registro di sistema per l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si tratta del caso delle istanze predefinite e delle istanze denominate. Per un'istanza predefinita, il nome di istanza e l'ID istanza sono MSSQLSERVER. Per utilizzare un ID istanza non predefinito, selezionare la casella di controllo **ID istanza** e specificare un valore. Se si sostituisce il valore predefinito, è necessario specificare lo stesso ID istanza per l'istanza da aggiornare in tutti i nodi del cluster di failover. L'ID istanza per l'istanza aggiornata deve corrispondere in tutti i nodi.  
  
     **Istanze e funzionalità rilevate** : nella griglia vengono [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] visualizzate le istanze di presenti nel computer in cui è in esecuzione il programma di installazione. **Fare clic su Avanti per continuare**.  
  
11. Nella pagina Requisiti di spazio su disco viene calcolato lo spazio su disco necessario per le funzionalità specificate e vengono confrontati i requisiti con lo spazio su disco disponibile nel computer in cui è in esecuzione il programma di installazione.  
  
12. Nella pagina per l'aggiornamento della ricerca full-text specificare le opzioni per i database da aggiornare. Per altre informazioni, vedere [Opzioni di aggiornamento della ricerca full-text](../../install/full-text-search-upgrade-options.md).  
  
13. Nella pagina **segnalazione errori** specificare le informazioni che si desidera inviare a per contribuire a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] migliorare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per impostazione predefinita, l'opzione per la segnalazione di errori è abilitata.  
  
14. Controllo configurazione sistema eseguirà uno o più set di regole per convalidare la configurazione del computer con le funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] specificate prima dell'inizio dell'operazione di aggiornamento.  
  
15. Nella pagina Report aggiornamento cluster vengono visualizzati l'elenco dei nodi dell'istanza del cluster di failover e le informazioni sulla versione dell'istanza per i componenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in ogni nodo. In tale pagina vengono visualizzati lo stato degli script del database e di replica, nonché messaggi informativi sulle conseguenze dell'atto di scegliere **Avanti**. In base al numero di nodi del cluster di failover già aggiornati e al numero totale di nodi, il programma di installazione Visualizza il comportamento di failover che si verifica quando si fa clic su **Avanti**. Verranno inoltre visualizzati avvisi relativi al tempo di inattività potenziale non necessario nel caso in cui i prerequisiti non sia già installati.  
  
16. Nella pagina Inizio aggiornamento è presente una visualizzazione albero delle opzioni specificate durante l'installazione. Per continuare, fare clic su **Aggiorna**. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verranno innanzitutto installati i prerequisiti obbligatori per le funzionalità selezionate e, successivamente, le funzionalità stesse.  
  
17. Durante l'aggiornamento, nella pagina Stato è possibile monitorare lo stato del processo di aggiornamento nel nodo corrente durante l'esecuzione del programma di installazione.  
  
18. Dopo l'aggiornamento del nodo corrente, nella pagina Report aggiornamento cluster vengono visualizzate le informazioni sullo stato dell'aggiornamento per tutti i nodi del cluster di failover, nonché le funzionalità di ogni nodo del cluster e le relative informazioni sulla versione. Confermare le informazioni sulla versione visualizzate e continuare con l'aggiornamento dei nodi rimanenti. Nella pagina relativa allo stato viene indicata anche l'eventuale esecuzione del failover sui nodi aggiornati. Per eseguire la conferma, è possibile inoltre effettuare la verifica tramite lo strumento Amministrazione cluster di Windows.  
  
19. Al termine dell'aggiornamento, nella pagina Operazione completata viene visualizzato un collegamento al file di log di riepilogo dell'installazione e ad altre note importanti. Per completare il processo di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , fare clic su **Chiudi**.  
  
20. Se viene richiesto, riavviare il computer. È importante leggere il messaggio visualizzato nell'Installazione guidata al termine dell'installazione. Per altre informazioni sui file di log del programma di installazione, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
21. Per completare il processo di aggiornamento, ripetere i passaggi da 1 a 21 in tutti gli altri nodi del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>Per aggiornare un cluster di failover su più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
#### <a name="to-upgrade-to-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster-existing-includessnoversionincludesssnoversion-mdmd-cluster-is-a-non-multi-subnet-cluster"></a>Per effettuare l'aggiornamento a un cluster di failover su più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (il cluster di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esistente non è un cluster su più subnet)  
  
1.  Seguire i passaggi da 1 a 24 descritti nella sezione [per aggiornare un cluster di failover di SQL Server](#UpgradeSteps) precedente per aggiornare il [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]cluster a.  
  
2.  Aggiungere un nodo su una subnet diversa utilizzando l'azione del programma di installazione AddNode e confermare la dipendenza delle risorse indirizzo IP su OR nella pagina **Configurazione rete cluster** . Per altre informazioni, vedere [Aggiungere o rimuovere nodi in un cluster di failover di SQL Server &#40;programma di installazione&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>Per aggiornare un cluster su più subnet utilizzando momentaneamente la tecnologia V-Lan estesa.  
  
1.  Seguire i passaggi da 1 a 24 descritti nella sezione [per aggiornare un cluster di failover di SQL Server](#UpgradeSteps) precedente per aggiornare il [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]cluster a.  
  
2.  Modificare le impostazioni di rete per spostare il nodo remoto in una subnet diversa.  
  
3.  Utilizzando lo strumento di gestione del cluster di failover Windows, aggiungere un nuovo indirizzo IP per la nuova subnet e impostare la dipendenza delle risorse indirizzo IP su OR.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Al termine dell'aggiornamento a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], completare le attività seguenti:  
  
-   Registrare i server  
  
     Poiché l'operazione di aggiornamento rimuove le impostazioni del Registro di sistema per l'istanza precedente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], in seguito all'aggiornamento è necessario registrare nuovamente i server.  
  
-   Aggiornare le statistiche  
  
     Per ottimizzare le prestazioni delle query, in seguito all'aggiornamento è consigliabile aggiornare le statistiche per tutti i database. Utilizzare la stored procedure **sp_updatestats** per aggiornare le statistiche nelle tabelle definite dall'utente dei database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Configurazione della nuova installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
     Per ridurre la superficie di attacco di un sistema, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono installati e abilitati in modo selettivo i servizi e le funzionalità principali. Per ulteriori informazioni sulla configurazione della superficie di attacco, vedere il file Leggimi per questa versione.  
  
## <a name="see-also"></a>Vedere anche  
 [Installare SQL Server 2014 dal prompt dei comandi](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
