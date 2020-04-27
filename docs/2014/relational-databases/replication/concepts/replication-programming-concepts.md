---
title: Concetti di base relativi alla programmazione della replica | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- replication [SQL Server], planning
- programming [SQL Server replication], planning
- programming [SQL Server replication]
ms.assetid: 2cd846e7-5bf3-4144-8772-703c4f439a2a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bf393a3e0f117098dc4a85bae3e6c68728f43a64
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62721809"
---
# <a name="replication-programming-concepts"></a>Concetti di base relativi alla programmazione della replica
  Prima di sviluppare un'applicazione che utilizza funzionalità di replica, è necessario eseguire i passaggi generali per la pianificazione seguenti:  
  
1.  Definire la topologia di replica.  
  
2.  Definire le funzionalità dell'applicazione.  
  
3.  Pianificare la sicurezza  
  
4.  Scegliere un ambiente di sviluppo.  
  
5.  Scegliere l'interfaccia di programmazione della replica appropriata.  
  
 Questi passaggi vengono descritti in modo più dettagliato nella parte restante di questo argomento. È incluso un esempio che consente di illustrare il processo di pianificazione.  
  
## <a name="defining-the-replication-topology"></a>Definizione della topologia di replica  
 Il primo passaggio nella programmazione della replica consiste nel definire la topologia di replica per l'applicazione. Se si sta scrivendo un'applicazione che utilizzerà una topologia di replica esistente, ad esempio un'applicazione client che accede a dati in un sottoscrittore esistente, è necessario andare al passaggio successivo.  
  
> [!NOTE]  
>  In alcuni casi, la distribuzione della topologia di replica rappresenterà l'unico scopo dell'applicazione.  
  
 La scelta della topologia di replica da definire dipende dai molti fattori, inclusi i seguenti:  
  
-   Se i dati replicati devono essere o meno aggiornati ed eventualmente da chi.  
  
-   Consistenza, autonomia e latenza sono aspetti da considerare nella distribuzione dei dati.  
  
-   Ambiente di replica, inclusi utenti aziendali, infrastruttura tecnica, rete e sicurezza e caratteristiche dei dati.  
  
-   Tipi di replica e opzioni di replica.  
  
-   Topologie di replica e come queste si allineano con i tipi di replica.  
  
 Se non si ha familiarità con la replica di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [Tipi di replica](../types-of-replication.md).  
  
## <a name="defining-application-functionality"></a>Definizione delle funzionalità dell'applicazione  
 Dopo aver definito la topologia di replica, è necessario decidere quali funzionalità verranno offerte dall'applicazione. Queste funzionalità possono variare da uno script che sincronizza una sottoscrizione a un'applicazione con un'interfaccia utente che consente di configurare la replica. La replica supporta le attività di programmazione generali seguenti:  
  
-   Impostazione della replica.  
  
-   Sincronizzazione dei sottoscrittori.  
  
-   Gestione di una topologia di replica.  
  
-   Monitoraggio di una topologia di replica.  
  
-   Risoluzione dei problemi di replica.  
  
 È inoltre comune estendere l'applicazione combinando le funzionalità di replica con altre funzionalità fornite da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Nella tabella seguente sono evidenziate alcune funzionalità estese che è possibile fornire nell'applicazione di replica.  
  
|Funzionalità|Esempio|  
|-------------------|-------------|  
|Amministrazione di server mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO)|Applicazione che consente a un amministratore di associare e configurare un database come server di pubblicazione in una topologia di replica.|  
|Accesso ai dati mediante ADO.NET|Applicazione che consente agli utenti di accedere e di modificare a livello di codice i dati di vendita replicati in un database del sottoscrittore locale in modalità offline, quindi di connettere e sincronizzare la sottoscrizione pull facendo clic su un pulsante.|  
  
## <a name="planning-for-security"></a>Pianificazione della sicurezza  
 Poiché la sicurezza è un aspetto importante per qualsiasi applicazione, è necessario completarne la pianificazione prima della scrittura del codice. La sicurezza dell'applicazione può essere suddivisa in tre parti principali, ovvero protezione del database, protezione della replica e scrittura di codice sicuro.  
  
 Negli argomenti seguenti vengono fornite informazioni sulla sicurezza:  
  
-   [Sicurezza replica di SQL Server](../security/view-and-modify-replication-security-settings.md)  
  
-   [Centro sicurezza per il motore di Database di SQL Server e il Database SQL di Azure](../../security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
## <a name="choosing-a-development-environment"></a>Scelta di un ambiente di sviluppo  
 Nello sviluppo di un'applicazione di replica è necessario considerare tre ambienti di sviluppo di base. Ogni ambiente di sviluppo dispone dell'accesso alle stesse funzionalità di replica, ma con alcune eccezioni. Le applicazioni di replica possono essere sviluppate in ognuno degli ambienti seguenti.  
  
-   **Codice gestito**  
  
     Ambiente di sviluppo orientato agli oggetti che sfrutta i vantaggi offerti dalla programmazione con [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] e da Common Language Runtime .NET (CLR). Il codice gestito rappresenta l'ambiente di programmazione consigliato sia per lo sviluppo .NET che di applicazioni [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Le interfacce di replica gestite consentono la programmazione dell'amministrazione della replica in modalità orientata agli oggetti senza che sia necessario conoscere [!INCLUDE[tsql](../../../includes/tsql-md.md)] e forniscono inoltre alcune funzionalità di callback durante l'esecuzione di agenti di replica non disponibili dagli script. Il codice gestito rappresenta l'ambiente ideale per lo sviluppo di componenti riutilizzabili e applicazioni dell'interfaccia utente.  
  
-   **Scripting**  
  
     Applicazioni semplici che eseguono una serie di comandi come stored procedure del sistema di replica in script [!INCLUDE[tsql](../../../includes/tsql-md.md)] o comandi all'interno di file batch. Sebbene sia possibile eseguire script in un ambiente gestito utilizzando il provider gestito [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in-process, è possibile ottenere le stesse funzionalità utilizzando le interfacce di replica gestite, che forniscono inoltre funzionalità di callback. La generazione di script rappresenta l'ambiente ideale per l'esecuzione di attività che verranno eseguite raramente e nei casi in cui non sono richieste funzionalità di callback, ad esempio l'installazione di un server di replica.  
  
-   **Codice nativo**  
  
     Ambiente di sviluppo orientato agli oggetti che utilizza l'accesso diretto al sistema o agli oggetti COM in cui il codice non è gestito da CLR. Le interfacce di replica del codice nativo sono deprecate o non più supportate. Per altre informazioni, vedere [Funzionalità deprecate nella replica di SQL Server](../deprecated-features-in-sql-server-replication.md) o [Compatibilità con le versioni precedenti della replica](../replication-backward-compatibility.md).  
  
## <a name="choose-the-appropriate-replication-programming-interface"></a>Scegliere l'interfaccia di programmazione della replica appropriata  
 L'ultimo passaggio della pianificazione consiste nello scegliere l'interfaccia di programmazione della replica appropriata che consenta di implementare le funzionalità di replica desiderate per l'ambiente di sviluppo scelto. Nella tabella seguente vengono illustrate le interfacce di programmazione della replica disponibili.  
  
|Interfaccia|Environment|Utilizzi|  
|---------------|-----------------|----------|  
|[Concetti di base relativi a RMO (Replication Management Objects)](replication-management-objects-concepts.md)|Codice gestito|Amministrazione, monitoraggio e sincronizzazione.|  
|<xref:Microsoft.SqlServer.Replication>|Codice gestito|Sincronizzazione.|  
|<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|Codice gestito|Creazione di gestori della logica di business per integrare la logica personalizzata con il processo di sincronizzazione di unione.|  
|[Stored procedure per la replica &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql)|Scripting|Amministrazione e monitoraggio.|  
|[Replication Agent Executables Concepts](replication-agent-executables-concepts.md)|Scripting|Sincronizzazione.|  
  
## <a name="example"></a>Esempio  
 La società [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] ha la necessità di pubblicare dati per 200 rappresentanti distribuiti in tutto il mondo. I rappresentanti viaggiano spesso e avranno quindi l'esigenza di utilizzare computer portatili o PDA per modificare i dati relativi ai clienti e aggiungere nuovi ordini. Le modifiche dovranno quindi essere sincronizzate con il server di pubblicazione nel momento in cui il rappresentante connette il computer portatile alla rete.  
  
 Per questa applicazione, i passaggi di pianificazione potrebbero essere analoghi ai seguenti:  
  
1.  La topologia di replica per questa applicazione esiste già. È tuttavia necessario creare una nuova sottoscrizione pull nel client. La pubblicazione deve utilizzare filtri con parametri per replicare un set di dati univoco per ogni rappresentante.  
  
2.  Oltre all'accesso ai dati tipico richiesto per un'applicazione di vendita, questa applicazione deve consentire a un venditore di sincronizzare la sottoscrizione pull su richiesta facendo clic su un pulsante. Dopo aver installato ed eseguito l'applicazione, i rappresentanti dovranno inoltre essere in grado di configurare una sottoscrizione e applicare lo snapshot iniziale al client. L'applicazione utilizzerà eventualmente l'infrastruttura fornita da Windows per individuare la connettività wireless e per sincronizzare automaticamente la sottoscrizione nel momento in cui viene rilevata una connessione.  
  
3.  Seguire tutte le linee guida per la sicurezza della replica, incluso l'utilizzo dell'autenticazione di Windows e di una rete privata virtuale (VPN, Virtual Private Network) per la connessione al server di pubblicazione. In caso di implementazione della sincronizzazione Web, utilizzare una connessione SSL (Secure Sockets Layer). Per altre informazioni, vedere [Configure Web Synchronization](../configure-web-synchronization.md).  
  
4.  Per sfruttare le caratteristiche offerte da [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], l'applicazione viene sviluppata utilizzando un linguaggio di codice gestito.  
  
5.  In base a questi requisiti, l'interfaccia gestita RMO (Replication Management Objects) è in grado di fornite tutte le funzionalità di replica necessarie per questa applicazione.  
  
 Questo scenario di esempio è stato implementato in un'applicazione di esempio inclusa in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
  
