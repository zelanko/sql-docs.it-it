---
title: Scelta di un protocollo di rete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
- Named Pipes [SQL Server]
- TCP [SQL Server]
- network protocols [SQL Server], choosing
- protocols [SQL Server], choosing
- NWLink IPX/SPX [SQL Server]
- client configuration [SQL Server], protocols
- VIA
- Multiprotocol Net-Library [SQL Server]
- IPX/SPX [SQL Server]
- Banyan VINES
- protocols [SQL Server], client configuration
ms.assetid: 6565fb7d-b076-4447-be90-e10d0dec359a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 9c167994c7145bce348b6959a57533e398e1d6bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035286"
---
# <a name="choosing-a-network-protocol"></a>Scelta di un protocollo di rete
  Per connettersi al [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] è necessario che sia abilitato un protocollo di rete. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può gestire le richieste su più protocolli contemporaneamente. I client eseguono la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un unico protocollo. Se il programma client non conosce il protocollo sul quale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in attesa, configurarlo per l'esecuzione di tentativi in sequenza su più protocolli. Utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per abilitare, disabilitare e configurare i protocolli di rete.  
  
## <a name="shared-memory"></a>Shared Memory  
 Shared Memory è il protocollo più semplice da utilizzare e non richiede la configurazione di impostazioni. Poiché i client che utilizzano questo protocollo possono connettersi solo a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguita sullo stesso computer, Shared Memory non è adatto per la maggior parte delle attività del database. Utilizzare il protocollo Shared Memory per la risoluzione dei problemi quando si sospetta che gli altri protocolli siano configurati in modo non corretto.  
  
> [!NOTE]  
>  I client che utilizzano MDAC 2.8 o versioni precedenti non possono utilizzare il protocollo Shared Memory. Se tentano di utilizzarlo, vengono automaticamente impostati sul protocollo Named Pipes.  
  
## <a name="tcpip"></a>TCP/IP  
 TCP/IP è un protocollo comune ampiamente utilizzato in Internet. Consente la comunicazione in reti interconnesse di computer con architetture hardware eterogenee e sistemi operativi diversi. Include gli standard per il routing del traffico di rete e offre caratteristiche di sicurezza avanzate. È il protocollo più diffuso nel settore aziendale. La configurazione del computer per l'utilizzo del protocollo TCP/IP può essere una procedura complessa, ma nella maggior parte dei casi i computer in rete sono già configurati in modo corretto. Per configurare le impostazioni TCP/IP non esposte in Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere la documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
## <a name="named-pipes"></a>Named Pipe  
 Il protocollo Named Pipes è stato sviluppato per le reti locali. Un parte della memoria viene utilizzata da un processo per il passaggio di informazioni a un altro processo, in modo che l'output dell'uno corrisponda all'input dell'altro. Il secondo processo può essere locale (in esecuzione nello stesso computer del primo) o remoto (in un computer in rete).  
  
## <a name="named-pipes-vs-tcpip-sockets"></a>Named Pipes e Socket TCP/IP  
 In un ambiente di rete locale (LAN) veloce, i client Named Pipes e i socket TCP/IP sono paragonabili in termini di prestazioni. La differenza di prestazioni tra i client diventa evidente con reti più lente, ad esempio nelle reti WAN (Wide Area Network) o nelle reti remote. Ciò dipende dalle diverse modalità di comunicazione impostate tra i peer dal meccanismo di comunicazione interprocesso (IPC).  
  
 Nel caso di Named Pipes, le comunicazioni di rete sono in genere caratterizzate da un maggior livello di interattività. Un peer invia i dati soltanto quando un altro peer li richiede tramite un comando di lettura. Un'operazione di lettura in rete genera solitamente una serie di messaggi di peek sulle named pipe prima dell'inizio della lettura dei dati. Tali messaggi possono risultare particolarmente onerosi in una rete lenta e provocare un traffico eccessivo, con conseguenze sulle prestazioni degli altri client di rete.  
  
 È inoltre importante distinguere tra pipe locali e pipe di rete. Se l'applicazione server viene eseguita a livello locale nel computer che esegue un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il protocollo Named Pipes locale è un'opzione consigliata. Il protocollo Named Pipes locale viene eseguito in modalità kernel a velocità molto elevate.  
  
 Con i socket TCP/IP le trasmissioni di dati sono più efficienti e comportano un minor overhead. Le trasmissioni di dati possono inoltre sfruttare i meccanismi di ottimizzazione delle prestazioni dei socket TCP/IP, quali il windowing, gli acknowledgement posticipati e così via. Questo può essere molto utile in una rete lenta. A seconda del tipo di applicazione, queste differenze di prestazioni possono risultare significative.  
  
 I socket TCP/IP supportano inoltre una coda di backlog. Questo assicura una maggiore continuità di funzionamento (anche se limitata) rispetto a Named Pipes con il quale possono verificarsi errori di pipe occupata durante i tentativi di connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 TCP/IP è generalmente preferibile in una rete LAN, WAN o remota lenta, mentre Named Pipes può rappresentare una scelta migliore quando la velocità della rete non costituisce un problema. Named Pipes offre infatti un maggior numero di funzionalità e opzioni di configurazione e il suo utilizzo risulta più semplice.  
  
## <a name="enabling-the-protocol"></a>Abilitazione del protocollo  
 Per il corretto funzionamento, è necessario abilitare il protocollo sia nel client che nel server. Il server può restare in attesa di richieste su tutti i protocolli abilitati contemporaneamente. I computer client possono sceglierne uno oppure tentare tutti i protocolli nell'ordine indicato in Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per una breve esercitazione sulla configurazione dei protocolli e sulla connessione al [!INCLUDE[ssDE](../../includes/ssde-md.md)], vedere [Esercitazione: Introduzione al motore di database](../../relational-databases/tutorial-getting-started-with-the-database-engine.md).  
  
  
