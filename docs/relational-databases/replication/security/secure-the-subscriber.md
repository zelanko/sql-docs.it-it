---
title: Proteggere il Sottoscrittore | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], security
- Subscribers [SQL Server replication], security
- security [SQL Server replication], Subscribers
ms.assetid: c8f0d62a-8b5d-4a21-9aec-223da52bb708
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 2ab65d61abb497c1930b94868f0a8b3433b44c95
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "70212300"
---
# <a name="secure-the-subscriber"></a>Sicurezza del Sottoscrittore
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Gli agenti di merge e di distribuzione si connettono al Sottoscrittore. Queste connessioni possono essere stabilite nel contesto di un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o di Windows. È importante specificare un account di accesso appropriato per questi agenti, attenendosi al principio di concedere i diritti minimi necessari e proteggere l'archiviazione di tutte le password. Per informazioni sulle autorizzazioni necessarie per ogni agente, vedere [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="distribution-agent"></a>Agente di distribuzione  
 È possibile utilizzare un agente di distribuzione per sottoscrizione, ovvero un agente indipendente in base all'impostazione predefinita per le pubblicazioni create nella Creazione guidata nuova pubblicazione, oppure un agente di distribuzione per coppia di database di pubblicazione e database di sottoscrizione, ovvero un agente condiviso. T  
  
 Per specificare le informazioni di connessione per le sottoscrizioni push, vedere [Creare una sottoscrizione push](../../../relational-databases/replication/create-a-push-subscription.md).  
  
 Per specificare le informazioni di connessione per le sottoscrizioni pull, vedere [Creare una sottoscrizione pull](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
## <a name="merge-agent"></a>Agente di merge  
 Per ogni sottoscrizione di tipo merge è disponibile un agente di merge specifico che si connette sia al server di pubblicazione che al Sottoscrittore, aggiornandoli entrambi.  
  
 Per specificare le informazioni di connessione per le sottoscrizioni push, vedere [Creare una sottoscrizione push](../../../relational-databases/replication/create-a-push-subscription.md).  
  
 Per specificare le informazioni di connessione per le sottoscrizioni pull, vedere [Creare una sottoscrizione pull](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
## <a name="immediate-updating-subscriptions"></a>Sottoscrizioni ad aggiornamento immediato  
 Quando si configura una sottoscrizione ad aggiornamento immediato, si specifica un account nel Sottoscrittore con cui vengono stabilite le connessioni al server di pubblicazione. Le connessioni vengono utilizzate dai trigger che si attivano presso il Sottoscrittore e propagano le modifiche al server di pubblicazione. Sono disponibili tre opzioni per il tipo di connessione:  
  
-   Server collegato creato dalla replica. La connessione viene stabilita con le credenziali specificate in fase di configurazione.  
  
-   Un server collegato creato dalla replica. La connessione viene eseguita con le credenziali dell'utente che apporta la modifica presso il Sottoscrittore.  
  
-   Un server collegato o remoto già definito.  
  
> [!IMPORTANT]  
>  Per specificare le informazioni di connessione, usare la stored procedure [sp_link_publication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). È possibile utilizzare anche la pagina **Account di accesso per sottoscrizioni aggiornabili** della Creazione guidata nuova sottoscrizione che chiama **sp_link_publication**. In alcune condizioni, questa stored procedure può avere esito negativo se nel Sottoscrittore è in esecuzione [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Service Pack 1 (SP1) o versioni successive e nel server di pubblicazione è in esecuzione una versione precedente. Se la stored procedure ha esito negativo in questo scenario, aggiornare il server di pubblicazione a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] SP1 o versioni successive.  
  
 Per altre informazioni, vedere [Creare una sottoscrizione aggiornabile di una pubblicazione transazionale](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md) e [Visualizzare e modificare le impostazioni di sicurezza della replica](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
> [!IMPORTANT]  
>  È consigliabile concedere all'account specificato per la connessione solo le autorizzazioni necessarie per l'inserimento, l'aggiornamento e l'eliminazione dei dati delle viste create dalla replica nel database di pubblicazione. Concedere autorizzazioni per le viste del database di pubblicazione con nomi nel formato **syncobj_** _\<NumeroEsadecimale>_ all'account configurato in ogni Sottoscrittore.  
  
## <a name="queued-updating-subscriptions"></a>Sottoscrizioni ad aggiornamento in coda  
 Quando si configurano sottoscrizioni ad aggiornamento in coda, è necessario tenere in considerazione due aspetti relativi alla sicurezza.  
  
-   Esiste un solo agente di lettura coda per ogni server di distribuzione. Per ogni server di distribuzione è consigliabile configurare al massimo una pubblicazione abilitata per le sottoscrizioni ad aggiornamento in coda.  
  
-   L'agente di lettura coda stabilisce connessioni al server di distribuzione, al server di pubblicazione e a ogni Sottoscrittore:  
  
    -   L'account con cui l'agente viene eseguito e stabilisce connessioni al server di distribuzione viene specificato al momento della creazione dell'agente. Se si utilizza la Creazione guidata nuova pubblicazione, l'agente viene creato quando si crea una pubblicazione abilitata per le sottoscrizioni aggiornabili.  
  
    -   L'account con cui l'agente stabilisce connessioni al server di pubblicazione viene specificato quando si configura la distribuzione per un server di pubblicazione. Specificare l'account di Windows con cui l'agente viene eseguito oppure un account di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    -   L'account con cui l'agente stabilisce connessioni al Sottoscrittore viene specificato quando si crea la sottoscrizione.  
  
    > [!IMPORTANT]  
    >  Utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per le connessioni ai Sottoscrittori e specificare un diverso account per la connessione a ogni Sottoscrittore. Se si utilizza una sottoscrizione pull, la connessione viene sempre impostata dalla replica in modo da utilizzare l'autenticazione di Windows. Per le sottoscrizioni pull, la replica non può infatti accedere ai metadati nel Sottoscrittore necessari per utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . In questo caso, modificare la connessione in modo da utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dopo la configurazione della sottoscrizione.  
  
     Per altre informazioni, vedere "Procedura: Creare una sottoscrizione aggiornabile di una pubblicazione transazionale (SQL Server Management Studio)" e [Visualizzare e modificare le impostazioni di sicurezza della replica](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitare connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sicurezza e protezione #40;replica&#41;](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
