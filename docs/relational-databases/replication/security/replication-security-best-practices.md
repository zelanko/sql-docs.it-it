---
title: Procedure consigliate per la sicurezza della replica | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], best practices
- security [SQL Server replication], between domains
- authentication [SQL Server replication]
- Internet [SQL Server replication], security
ms.assetid: 1ab2635d-0992-4c99-b17d-041d02ec9a7c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a282ed4ce04df00a062fb1b910318125e23b1634
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078779"
---
# <a name="replication-security-best-practices"></a>Procedure consigliate per la sicurezza della replica
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replica implica lo spostamento di dati in ambienti distribuiti che includono reti Intranet in un singolo dominio, applicazioni che accedono a dati tra domini non attendibili e Internet. È importante individuare l'approccio migliore per la protezione delle connessioni di replica in queste diverse circostanze.  
  
 Le informazioni seguenti sono applicabili alla replica in qualsiasi ambiente:  
  
-   Crittografare le connessioni tra computer in una topologia di replica utilizzano un metodo standard, ad esempio le reti private virtuali (VPN, Virtual Private Network), la crittografia SSL (Secure Sockets Layer) o lo standard IPSec (Internet Protocol Security). Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md). Per informazioni sull'utilizzo di reti VPN e del protocollo SSL per la replica di dati su Internet, vedere [Securing Replication Over the Internet](../../../relational-databases/replication/security/securing-replication-over-the-internet.md).  
  
     Se si usa SSL per proteggere le connessioni tra computer in una topologia di replica, specificare un valore pari a **1** o **2** per il parametro **-EncryptionLevel** di ogni agente di replica. È consigliabile usare un valore pari a **2** . Un valore pari a **1** indica che è utilizzata la crittografia, ma l'agente non verifica che il certificato SSL del server sia firmato da un'autorità emittente attendibile; un valore pari a **2** indica che il certificato viene verificato. I parametri degli agenti possono essere specificati nei profili agente e dalla riga di comando. Per altre informazioni, vedere:  
  
    -   [Usare i profili agenti di replica](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Visualizzare e modificare i parametri del prompt dei comandi dell'agente di replica &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   Eseguire ogni agente di replica con un diverso account di Windows e utilizzare l'autenticazione di Windows per tutte le connessioni agli agenti di replica. Per altre informazioni su come specificare gli account, vedere [Controllo di identità e accesso (replica)](../../../relational-databases/replication/security/identity-and-access-control-replication.md).  
  
-   Concedere agli agenti solo le autorizzazioni necessarie. Per ulteriori informazioni, vedere la sezione relativa alle autorizzazioni necessarie per gli agenti in [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Verificare che tutti gli account degli agenti di merge e di distribuzione siano inclusi nell'elenco di accesso alla pubblicazione. Per altre informazioni, vedere [Proteggere il server di pubblicazione](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
-   Attenersi al principio dei privilegi minimi, concedendo agli account nell'elenco di accesso alla pubblicazione solo le autorizzazioni necessarie per eseguire le attività di replica. Non aggiungere gli account di accesso ad alcun ruolo predefinito del server che non sia necessario per la replica.  
  
-   Configurare la condivisione snapshot in modo da consentire l'accesso in lettura a tutti gli agenti di merge e di distribuzione. Se vengono utilizzati snapshot per pubblicazioni con filtri con parametri, verificare che ogni cartella sia configurata per l'accesso in lettura solo per gli account degli agenti di merge appropriati.  
  
-   Configurare la condivisione snapshot per consentire l'accesso in scrittura all'agente snapshot.  
  
-   Se si utilizzano sottoscrizioni pull, inserire la cartella snapshot in una condivisione di rete anziché in un percorso locale.  
  
 Se nella topologia di replica sono inclusi computer di domini diversi o di domini che non hanno relazioni di trust, è possibile utilizzare l'autenticazione di Windows o l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per le connessioni eseguite dagli agenti. Per ulteriori informazioni sui domini, vedere la documentazione di Windows. È consigliabile, dal punto di vista della sicurezza, utilizzare l'autenticazione di Windows.  
  
-   Per utilizzare l'autenticazione di Windows:  
  
    -   Aggiungere un account di Windows locale (non un account di dominio) per ogni agente nei nodi appropriati, utilizzando lo stesso nome e password per ogni nodo. Ad esempio, l'agente di distribuzione per una sottoscrizione push viene eseguito nel server di distribuzione e stabilisce connessioni al server di distribuzione e al Sottoscrittore. L'account di Windows per l'agente di distribuzione deve essere aggiunto al server di distribuzione e al Sottoscrittore.  
  
    -   Verificare che un determinato agente, ad esempio l'agente di distribuzione per una sottoscrizione, venga eseguito con lo stesso account in ogni computer.  
  
-   Per utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
    -   Aggiungere un account di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per ogni agente nei nodi appropriati, utilizzando lo stesso nome e password per ogni nodo. Ad esempio, l'agente di distribuzione per una sottoscrizione push viene eseguito nel server di distribuzione e stabilisce connessioni al server di distribuzione e al Sottoscrittore. L'account di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per l'agente di distribuzione deve essere aggiunto al server di distribuzione e al Sottoscrittore.  
  
    -   Verificare che un determinato agente, ad esempio l'agente di distribuzione per una sottoscrizione, stabilisca connessioni utilizzando lo stesso account in ogni computer.  
  
    -   Nei casi in cui è necessaria l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , l'accesso alle condivisioni snapshot UNC spesso non è disponibile, ad esempio, può essere bloccato da un firewall. In tal caso, è possibile trasferire lo snapshot ai Sottoscrittori tramite FTP. Per altre informazioni, vedere [Trasferire snapshot tramite FTP](../../../relational-databases/replication//publish/deliver-a-snapshot-through-ftp.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitare connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replica su Internet](../../../relational-databases/replication/replication-over-the-internet.md)   
 [Proteggere il sottoscrittore](../../../relational-databases/replication/security/secure-the-subscriber.md)   
 [Proteggere il database di distribuzione](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [Proteggere il server di pubblicazione](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
