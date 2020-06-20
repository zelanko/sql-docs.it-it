---
title: Aggiornare e aggiornare i server del gruppo di disponibilità con tempi di inattività e perdita di dati minimi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: f670af56-dbcc-4309-9119-f919dcad8a65
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 46777707354b1379d50b6379e21aabd02ffb5097
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936318"
---
# <a name="upgrade-and-update-of-availability-group-servers-with-minimal-downtime-and-data-loss"></a>Aggiornamento dei server dei gruppi di disponibilità con tempi di inattività e perdita dei dati minimi
  Quando si aggiornano istanze del server da SQL Server 2012 a un Service Pack o a una versione più recente, è possibile ridurre i tempi di inattività per un gruppo di disponibilità alla durata di un singolo failover manuale eseguendo un aggiornamento in sequenza. L'aggiornamento in sequenza può essere effettuato sia per passare a versioni successive di SQL Server sia per aggiornare la versione corrente con hotfix o Service Pack.  
  
 In questo argomento vengono illustrate esclusivamente le modalità di aggiornamento di SQL Server. Per gli aggiornamenti o gli aggiornamenti relativi al sistema operativo in cui sono in esecuzione le istanze di SQL Server a disponibilità elevata, vedere [migrazione tra cluster di gruppi di disponibilità AlwaysOn per gli aggiornamenti del sistema operativo](https://msdn.microsoft.com/library/jj873730.aspx)  
  
## <a name="rolling-upgradeupdate-best-practices-for-alwayson-availability-groups"></a>Procedure consigliate relative all'aggiornamento in sequenza per i gruppi di disponibilità AlwaysOn  
 Quando si eseguono aggiornamenti dei server, è consigliabile attenersi alle procedure consigliate illustrate di seguito allo scopo di ridurre al minimo i tempi di inattività e la perdita di dati per i gruppi di disponibilità:  
  
-   Prima di avviare l'aggiornamento in sequenza:  
  
    -   Effettuare un failover manuale di prova su almeno una delle repliche con commit sincrono  
  
    -   Proteggere i dati eseguendo un backup completo di ogni database di disponibilità  
  
    -   Eseguire il comando DBCC CHECKDB su ogni database di disponibilità  
  
-   Aggiornare sempre prima i nodi di replica secondaria remota, quindi quelli di replica secondaria locale e infine il nodo di replica primaria.  
  
-   Non è possibile eseguire backup su un database in corso di aggiornamento.  Prima di eseguire l'aggiornamento delle repliche secondarie, configurare la preferenza per i backup automatici in modo che vengano eseguiti solo sulla replica primaria.  Prima di aggiornare la replica primaria, modificare questa impostazione per l'esecuzione dei backup solo nelle repliche secondarie.  
  
-   Per evitare failover accidentali del gruppo di disponibilità durante il processo di aggiornamento, prima di iniziare rimuovere il failover di disponibilità da tutte le repliche con commit sincrono.  
  
-   Non aggiornare il nodo di replica primaria prima di aver effettuato il failover del gruppo di disponibilità a un nodo aggiornato con una replica secondaria. In caso contrario, le applicazioni client potrebbero subire tempi di inattività prolungati durante l'aggiornamento sulla replica primaria.  
  
-   Effettuare sempre il failover del gruppo di disponibilità a un nodo di replica secondaria con commit sincrono. Se si effettua il failover a una replica secondaria con commit asincrono, si verificheranno perdite di dati nei database e lo spostamento dei dati verrà automaticamente sospeso finché non verrà ripreso manualmente.  
  
-   Non aggiornare il nodo di replica primaria prima di aver aggiornato tutti gli altri nodi di replica secondaria. Tramite una replica primaria aggiornata non è più possibile recapitare log alle repliche secondarie non ancora aggiornate alla stessa versione. Se viene sospeso lo spostamento dei dati in una replica secondaria, il failover automatico per quest'ultima non può essere eseguito e nei database di disponibilità possono verificarsi perdite di dati.  
  
-   Prima di effettuare il failover di un gruppo di disponibilità, verificare che lo stato di sincronizzazione della destinazione di failover risulti essere SINCRONIZZATO.  
  
## <a name="rolling-upgradeupdate-process"></a>Processo di aggiornamento in sequenza  
 Il processo effettivo dipende da fattori quali la topologia di distribuzione dei gruppi di disponibilità e la modalità di commit di ogni replica. Nello scenario più semplice, l'aggiornamento in sequenza è articolato in un processo a più fasi che nella sua forma essenziale prevede i passaggi seguenti:  
  
 ![Aggiornamento del gruppo di disponibilità nello scenario di ripristino di emergenza a disponibilità elevata](../../media/alwaysonupgrade-ag-hadr.gif "Aggiornamento del gruppo di disponibilità nello scenario di ripristino di emergenza a disponibilità elevata")  
  
1.  Rimuovere il failover automatico in tutte le repliche con commit sincrono  
  
2.  Aggiornare tutte le istanze del server remoto in cui vengono eseguite repliche secondarie con commit asincrono  
  
3.  Aggiornare tutte le istanze del server locale in cui non è attualmente in esecuzione la replica primaria  
  
4.  Effettuare manualmente il failover del gruppo di disponibilità a una replica secondaria con commit sincrono  
  
5.  Aggiornare l'istanza del server in cui, in precedenza, era ospitata la replica primaria  
  
6.  Configurare i partner di failover automatico nel modo desiderato  
  
 Se necessario, è possibile eseguire un ulteriore failover manuale per ripristinare la configurazione originale del gruppo di disponibilità.  
  
## <a name="availability-group-with-one-remote-secondary-replica"></a>Gruppo di disponibilità con una replica secondaria remota  
 Se è stato distribuito un gruppo di disponibilità solo a fini di ripristino di emergenza, potrebbe essere necessario effettuarne il failover a una replica secondaria con commit asincrono. Questo tipo di configurazione è illustrato nella figura seguente:  
  
 ![Aggiornamento del gruppo di disponibilità nello scenario di ripristino di emergenza](../../media/agupgrade-ag-dr.gif "Aggiornamento del gruppo di disponibilità nello scenario di ripristino di emergenza")  
  
 In questo caso, è necessario effettuare il failover del gruppo di disponibilità a una replica secondaria con commit asincrono durante l'aggiornamento in sequenza. Per evitare perdite di dati, modificare la modalità di commit impostando il commit sincrono e attendere che venga completata la sincronizzazione della replica secondaria prima di effettuare il failover del gruppo di disponibilità. Il processo di aggiornamento in sequenza può quindi avvenire come segue:  
  
1.  Aggiornare il server remoto  
  
2.  Impostare la modalità di commit sincrono  
  
3.  Attendere che lo stato di sincronizzazione sia SINCRONIZZATO  
  
4.  Effettuare il failover del gruppo di disponibilità a un sito remoto  
  
5.  Aggiornare il server locale (sito primario)  
  
6.  Effettuare il failover del gruppo di disponibilità al sito primario  
  
7.  Impostare la modalità di commit asincrono  
  
 Poiché la modalità di commit sincrono non è consigliata per la sincronizzazione dei dati con un sito remoto, tramite le applicazioni client potrebbe essere rilevato un aumento immediato della latenza del database in seguito alla modifica dell'impostazione. Inoltre, l'esecuzione di un failover causerà la rimozione di tutti i messaggi di log non riconosciuti. La quantità di messaggi di log rimossi può essere notevole a causa dell'elevata latenza di rete tra i due siti, il che determina un numero elevato di errori delle transazioni con i client. È possibile ridurre l'impatto per le applicazioni client nel modo seguente:  
  
-   Scegliere con attenzione una finestra di manutenzione nei periodi di minore traffico client  
  
-   Durante l'aggiornamento di SQL Server nel sito primario, impostare di nuovo la modalità di commit asincrono, quindi ripristinare il commit sincrono una volta pronti a effettuare nuovamente il failover al sito primario  
  
## <a name="availability-group-with-failover-cluster-instance-nodes"></a>Gruppo di disponibilità con nodi di istanze del cluster di failover  
 Se in un gruppo di disponibilità sono contenuti nodi di istanze del cluster di failover, è consigliabile aggiornare i nodi inattivi prima di quelli attivi. Nella figura seguente è illustrato uno scenario comune di gruppi di disponibilità con istanze del cluster di failover per la disponibilità elevata locale e il commit asincrono tra le istanze stesse ai fini del ripristino di emergenza remoto ed è indicata la relativa sequenza di aggiornamento.  
  
 ![Aggiornamento del gruppo di disponibilità con istanze del cluster di failover](../../media/agupgrade-ag-fci-dr.gif "Aggiornamento del gruppo di disponibilità con istanze del cluster di failover")  
  
1.  Aggiornare REMOTE2  
  
2.  Effettuare il failover dell'istanza FCI2 a REMOTE2  
  
3.  Aggiornare REMOTE1  
  
4.  Aggiornare PRIMARY2  
  
5.  Effettuare il failover dell'istanza FCI1 a PRIMARY2  
  
6.  Aggiornare PRIMARY1  
  
## <a name="upgradeupdate-sql-server-instances-with-multiple-availability-groups"></a>Aggiornare le istanze di SQL Server con più gruppi di disponibilità  
 Se si eseguono più gruppi di disponibilità con repliche primarie su nodi server distinti (configurazione Attiva/Attiva), il percorso di aggiornamento prevede più passaggi di failover allo scopo di preservare la disponibilità elevata durante il processo. Si supponga di disporre di tre gruppi di disponibilità in tre nodi server come illustrato nella tabella seguente e che tutte le repliche secondarie vengano eseguite in modalità di commit sincrono.  
  
|Gruppo di disponibilità|Nodo1|Nodo2|Nodo3|  
|------------------------|-----------|-----------|-----------|  
|AG1|Principale|||  
|AG2||Principale||  
|AG3|||Principale|  
  
 In determinate situazioni potrebbe essere opportuno eseguire un aggiornamento in sequenza con bilanciamento del carico articolato come segue:  
  
1.  Effettuare il failover di AG2 a Nodo3 (per liberare Nodo2)  
  
2.  Aggiornare Nodo2  
  
3.  Effettuare il failover di AG1 a Nodo2 (per liberare Nodo1)  
  
4.  Aggiornare Nodo1  
  
5.  Effettuare il failover di AG2 e AG3 a Nodo1 (per liberare Nodo3)  
  
6.  Aggiornare Nodo3  
  
7.  Effettuare il failover di AG3 a Nodo3  
  
 Questa sequenza di aggiornamento implica un tempo di inattività medio inferiore alla durata di due failover per ciascun gruppo di disponibilità. La configurazione risultante è illustrata nella tabella seguente.  
  
|Gruppo di disponibilità|Nodo1|Nodo2|Nodo3|  
|------------------------|-----------|-----------|-----------|  
|AG1||Principale||  
|AG2|Principale|||  
|AG3|||Principale|  
  
 Il percorso di aggiornamento e i tempi di inattività per le applicazioni client possono variare a seconda della specifica implementazione in uso.  
  
  
