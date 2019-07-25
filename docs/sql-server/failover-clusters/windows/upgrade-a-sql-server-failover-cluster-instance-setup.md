---
title: Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server (programma di installazione) | Microsoft Docs
ms.custom: ''
ms.date: 01/22/2016
ms.prod: sql
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
ms.openlocfilehash: 0e5232f1f8cad8ba9e6dc4ffcb9d838614a8c2c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044709"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server (installazione)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Per aggiornare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un cluster di failover di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] , è possibile usare l'interfaccia utente di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o il prompt dei comandi.  
  
 Per le installazioni locali, è necessario eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura per tale condivisione.  
  
 Prima dell'aggiornamento, vedere [Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md).  
  
##  <a name="UpgradeSteps"></a> Per aggiornare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
#### <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>Per aggiornare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
1.  Dal supporto di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] relativo all'edizione corrispondente a quella da aggiornare, fare doppio clic su setup.exe nella cartella radice. È possibile che venga richiesto di installare i prerequisiti se non sono già stati installati in precedenza.  
  
2.  Una volta installati i prerequisiti, l'Installazione guidata avvia Centro installazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per aggiornare un'istanza esistente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], selezionare l'istanza.  
  
3.  Se sono necessari, i file di supporto per l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verranno installati dal programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se viene richiesto, riavviare il computer prima di continuare.  
  
4.  Controllo configurazione sistema consente di eseguire un'operazione di individuazione nel computer. Per continuare, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
5.  Nella pagina relativa al codice Product Key immettere la chiave PID relativa all'edizione della nuova versione corrispondente all'edizione della versione precedente del prodotto. Per aggiornare un cluster di failover dell'edizione Enterprise, ad esempio, è necessario specificare una chiave PID per [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]. Per continuare, fare clic su **Avanti** . Si noti che la chiave PID utilizzata per l'aggiornamento del cluster di failover deve essere coerente in tutti i nodi del cluster della stessa istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
6.  Nella pagina Condizioni di licenza leggere il contratto di licenza, quindi selezionare la casella di controllo per accettarne le condizioni. Per migliorare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è inoltre possibile abilitare l'opzione relativa all'utilizzo delle funzionalità e inviare report a [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Fare clic su**Avanti**per continuare. Per terminare l'installazione, fare clic su **Annulla**.  
  
7.  Nella pagina Seleziona istanza specificare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da aggiornare a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Fare clic su**Avanti**per continuare.  
  
8.  Nella pagina Selezione funzionalità le funzionalità da aggiornare saranno preselezionate. Dopo aver selezionato il nome della funzionalità desiderata, nel riquadro a destra verrà visualizzata una descrizione per ogni gruppo di componenti. Non è possibile modificare le funzionalità da aggiornare, né aggiungere funzionalità durante l'operazione di aggiornamento. Per aggiungere funzionalità a un'istanza aggiornata di [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] dopo aver completato l'aggiornamento, vedere [Aggiungere funzionalità a un'istanza di SQL Server 2016 &#40;programma di installazione&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md).  
  
     I prerequisiti per le funzionalità selezionate vengono visualizzati nel riquadro di destra. Il programma di installazione di SQL Server consentirà di installare i prerequisiti che non sono già stati installati durante la procedura di installazione descritta più avanti in questo argomento. Per risparmiare tempo, è consigliabile preinstallare questi prerequisiti nei singoli nodi.  
  
9. Nella pagina Configurazione dell'istanza i campi vengono compilati automaticamente in base ai valori dell'istanza precedente, ma è possibile specificare i valori relativi al nuovo ID istanza.  
  
     **ID istanza** : per impostazione predefinita, come ID istanza viene utilizzato il nome dell'istanza. Tale nome viene utilizzato per identificare le directory di installazione e le chiavi del Registro di sistema per l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si tratta del caso delle istanze predefinite e delle istanze denominate. Per un'istanza predefinita, il nome di istanza e l'ID istanza sono MSSQLSERVER. Per utilizzare un ID istanza non predefinito, selezionare la casella di controllo **ID istanza** e specificare un valore. Se si sostituisce il valore predefinito, è necessario specificare lo stesso ID istanza per l'istanza da aggiornare in tutti i nodi del cluster di failover. L'ID istanza per l'istanza aggiornata deve corrispondere in tutti i nodi.  
  
     **Istanze e funzionalità rilevate** : nella griglia vengono visualizzate le istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] presenti nel computer in cui viene eseguito il programma di installazione. Fare clic su**Avanti**per continuare.  
  
10. Nella pagina Requisiti di spazio su disco viene calcolato lo spazio su disco necessario per le funzionalità specificate e vengono confrontati i requisiti con lo spazio su disco disponibile nel computer in cui è in esecuzione il programma di installazione.  
  
11. Nella pagina per l'aggiornamento della ricerca full-text specificare le opzioni per i database da aggiornare. Per altre informazioni, vedere [Opzioni di aggiornamento della ricerca full-text](https://msdn.microsoft.com/library/16c9376b-5fbb-4495-a429-06a2493849c9).  
  
12. Nella pagina **Segnalazione errori** specificare le informazioni da inviare a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] per migliorare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per impostazione predefinita, l'opzione per la segnalazione di errori è abilitata.  
  
13. Controllo configurazione sistema eseguirà uno o più set di regole per convalidare la configurazione del computer con le funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] specificate prima dell'inizio dell'operazione di aggiornamento.  
  
14. Nella pagina Report aggiornamento cluster vengono visualizzati l'elenco dei nodi dell'istanza del cluster di failover e le informazioni sulla versione dell'istanza per i componenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in ogni nodo. In tale pagina vengono visualizzati lo stato degli script del database e di replica, nonché messaggi informativi sulle conseguenze dell'atto di scegliere **Avanti**. In base al numero di nodi del cluster di failover già aggiornati e al numero di nodi complessivo, verrà visualizzato il comportamento del failover quando si sceglie **Avanti**. Verranno inoltre visualizzati avvisi relativi al tempo di inattività potenziale non necessario nel caso in cui i prerequisiti non sia già installati.  
  
15. Nella pagina Inizio aggiornamento è presente una visualizzazione albero delle opzioni specificate durante l'installazione. Per continuare, fare clic su **Aggiorna**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Il programma di installazione consentirà innanzitutto di installare i prerequisiti obbligatori per le funzionalità selezionate e, successivamente, le funzionalità stesse.  
  
16. Durante l'aggiornamento, nella pagina Stato è possibile monitorare lo stato del processo di aggiornamento nel nodo corrente durante l'esecuzione del programma di installazione.  
  
17. Dopo l'aggiornamento del nodo corrente, nella pagina Report aggiornamento cluster vengono visualizzate le informazioni sullo stato dell'aggiornamento per tutti i nodi del cluster di failover, nonché le funzionalità di ogni nodo del cluster e le relative informazioni sulla versione. Confermare le informazioni sulla versione visualizzate e continuare con l'aggiornamento dei nodi rimanenti. Nella pagina relativa allo stato viene indicata anche l'eventuale esecuzione del failover sui nodi aggiornati. Per eseguire la conferma, è possibile inoltre effettuare la verifica tramite lo strumento Amministrazione cluster di Windows.  
  
18. Al termine dell'aggiornamento, nella pagina Operazione completata viene visualizzato un collegamento al file di log di riepilogo dell'installazione e ad altre note importanti. Per completare il processo di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , fare clic su **Chiudi**.  
  
19. Se viene richiesto, riavviare il computer. È importante leggere il messaggio visualizzato nell'Installazione guidata al termine dell'installazione. Per altre informazioni sui file di log del programma di installazione, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
20. Per completare il processo di aggiornamento, ripetere questi passaggi in tutti gli altri nodi del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>Per aggiornare un cluster di failover su più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
#### <a name="to-upgrade-to-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster-existing-includessnoversionincludesssnoversion-mdmd-cluster-is-a-non-multi-subnet-cluster"></a>Per effettuare l'aggiornamento a un cluster di failover su più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (il cluster di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esistente non è un cluster su più subnet)  
  
1.  Seguire le istruzioni precedenti per aggiornare il cluster a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
2.  Aggiungere un nodo su una subnet diversa utilizzando l'azione del programma di installazione AddNode e confermare la dipendenza delle risorse indirizzo IP su OR nella pagina **Configurazione rete cluster**. Per altre informazioni, vedere [Aggiungere o rimuovere nodi in un cluster di failover di SQL Server &#40;programma di installazione&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>Per aggiornare un cluster su più subnet utilizzando momentaneamente la tecnologia V-Lan estesa.  
  
1.  Seguire le istruzioni precedenti per aggiornare il cluster a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
2.  Modificare le impostazioni di rete per spostare il nodo remoto in una subnet diversa.  
  
3.  Utilizzando lo strumento di gestione del cluster di failover Windows, aggiungere un nuovo indirizzo IP per la nuova subnet e impostare la dipendenza delle risorse indirizzo IP su OR.  
  
## <a name="next-steps"></a>Next Steps  
 Al termine dell'aggiornamento a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], completare le attività seguenti:  
  
-   [Completare l'aggiornamento al motore di database](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
-   [Modificare la modalità di compatibilità del database e usare l'archivio query](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)  
  
-   [Vantaggi delle nuove funzionalità di SQL Server 2016](https://msdn.microsoft.com/library/d8879659-8efa-4442-bcbb-91272647ae16)  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)   
 [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Aggiungere funzionalità a un'istanza di SQL Server 2016 &#40;programma di installazione&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)  
  
  
