---
title: Chiavi di crittografia del database e di SQL Server (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- keys [SQL Server], database encryption
ms.assetid: 15c0a5e8-9177-484c-ae75-8c552dc0dac0
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: e214a46adece1bcee940f57805db897d1c8c76db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011314"
---
# <a name="sql-server-and-database-encryption-keys-database-engine"></a>Chiavi di crittografia del database e di SQL Server (Motore di database)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa le chiavi di crittografia per la protezione di dati, credenziali e informazioni di connessione archiviate in un database del server. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dispone di due tipi di chiavi: *simmetrica* e *asimmetrica*. Le chiavi simmetriche utilizzano la stessa password per crittografare e decrittografare i dati. Le chiavi asimmetriche usano una password per crittografare i dati (chiave *pubblica* ) e un'altra per decrittografare i dati (chiave *privata* ).  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], le chiavi di crittografia sono costituite da una combinazione di chiavi pubbliche, private e simmetriche utilizzate per proteggere dati riservati. La chiave simmetrica viene creata durante l'inizializzazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando si avvia per la prima volta l'istanza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La chiave è utilizzata da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per crittografare dati riservati archiviati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Le chiavi pubblica e privata vengono create dal sistema operativo e sono utilizzate per proteggere la chiave simmetrica. Per ogni istanza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che contiene dati riservati in un database viene creata una coppia di chiavi pubblica e privata.  
  
## <a name="applications-for-sql-server-and-database-keys"></a>Applicazioni per chiavi del SQL Server e del database  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contiene due applicazioni principali per le chiavi: una *chiave master del servizio* (SMK) generata per un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e una *chiave master del database* (DMK) usata per un database.  
  
 La SMK viene generata automaticamente la prima volta che viene avviata e usata l'istanza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per crittografare la password, le credenziali o la chiave master del database di un server collegato. La SMK viene crittografata usando la chiave locale del computer che utilizza l'API Windows Data Protection (DPAPI). Il DPAPI usa una chiave derivata dalle credenziali Windows dell'account di servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e le credenziali del computer. La chiave master del servizio può essere decrittografata solo dall'account del servizio con cui è stata creata o da un'entità autorizzata ad accedere alle credenziali della macchina.  
  
 La chiave master del database è una chiave simmetrica utilizzata per proteggere le chiavi private dei certificati e le chiavi asimmetriche presenti nel database. Si può utilizzare anche per crittografare dati, ma ha limitazioni di lunghezza che la rendono meno pratica per i dati rispetto all'utilizzo di una chiave simmetrica.  
  
 Al momento della creazione, la chiave master viene crittografata con l'algoritmo Triple DES e una password specificata dall'utente. Per attivare la decrittografia automatica della chiave master, viene crittografata una copia della chiave utilizzando la SMK. Viene archiviata in entrambi i database dove è utilizzata e nel database `master` di sistema.  
  
 La copia della DMK archiviata nel database `master` di sistema viene aggiornata automaticamente ogni qualvolta la DMK è modificata. Tuttavia, questa impostazione predefinita può essere modificata utilizzando l'opzione `DROP ENCRYPTION BY SERVICE MASTER KEY` dell'istruzione `ALTER MASTER KEY`. Per aprire una DMK non crittografata con la chiave master del servizio, è necessario utilizzare l'istruzione `OPEN MASTER KEY` e una password.  
  
## <a name="managing-sql-server-and-database-keys"></a>Gestione delle chiavi del SQL Server e del database  
 La gestione delle chiavi di crittografia comprende la creazione di nuove chiavi di database, la creazione di un backup delle chiavi server e del database e informazioni su quando e come ripristinare, eliminare o modificare le chiavi.  
  
 Per la gestione delle chiavi simmetriche è possibile utilizzare gli strumenti inclusi in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per eseguire le operazioni seguenti:  
  
-   Backup di una copia delle chiavi del server e del database per poterle utilizzare per il recupero dell'installazione di un server di report o come parte di una migrazione pianificata.  
  
-   Ripristino di una chiave precedentemente salvata in un database. Consente a una nuova istanza del server l'accesso a dati esistenti che non erano stati crittografati in origine.  
  
-   Eliminazione dei dati crittografati in un database nel caso molto improbabile in cui non sia più possibile accedere a tali dati.  
  
-   Ricreazione delle chiavi e riesecuzione della crittografia dei dati nel caso molto improbabile in cui la chiave risulti compromessa. Come procedura di sicurezza consigliata, ricreare le chiavi periodicamente, ad esempio dopo qualche mese, per proteggere il server da attacchi informatici mirati alla decrittazione delle chiavi.  
  
-   Aggiunta o rimozione di un'istanza del server da una distribuzione del server con scalabilità orizzontale in cui più server condividono sia un unico database sia la chiave che consente la crittografia reversibile per quel database.  
  
## <a name="important-security-information"></a>Importanti informazioni relative alla sicurezza  
 L'accesso a oggetti protetti dalla chiave master del servizio richiede l'account di servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzato per creare la chiave o l'account del computer. In altre parole, il computer è legato al sistema sul quale la chiave è stata creata. È possibile modificare l'account del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] *o* l'account del computer senza perdere l'accesso alla chiave. Tuttavia, se si modificano entrambi, si perderà l'accesso alla chiave master del servizio. Se si verifica tale perdita senza disporre di uno di questi due elementi, non sarà possibile decrittografare i dati e gli oggetti crittografati usando la chiave originale.  
  
 Non è possibile ripristinare connessioni protette con la chiave master del servizio se non si dispone della stessa.  
  
 L'accesso a oggetti e dati protetti con la chiave master del database richiede solo la password utilizzata per proteggere la chiave.  
  
> [!CAUTION]  
>  Se si perde ogni accesso alle chiavi descritte in precedenza, si perderà l'accesso agli oggetti, alle connessioni e ai dati protetti da quelle chiavi. È possibile ripristinare la chiave master del servizio, come viene descritto nei collegamenti qui riportati, oppure è possibile ritornare al sistema di crittografa originale per recuperare l'accesso. Non è possibile recuperare l'accesso in altro modo.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Service Master Key](service-master-key.md)  
 Viene fornita una breve spiegazione della chiave master del servizio e delle procedure consigliate.  
  
 [Extensible Key Management &#40;EKM&#41;](extensible-key-management-ekm.md)  
 Viene illustrata la modalità di utilizzo dei sistemi di gestione delle chiavi di terze parti con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="related-tasks"></a>Attività correlate  
 [Backup della chiave master del servizio](back-up-the-service-master-key.md)  
  
 [Ripristino della chiave master del servizio](restore-the-service-master-key.md)  
  
 [Creazione della chiave master di un database](create-a-database-master-key.md)  
  
 [Backup della chiave master di un database](back-up-a-database-master-key.md)  
  
 [Ripristino di una chiave master del database](restore-a-database-master-key.md)  
  
 [Creare chiavi simmetriche identiche su due server](create-identical-symmetric-keys-on-two-servers.md)  
  
 [Extensible Key Management con l'insieme di credenziali delle chiavi di Azure &#40;SQL Server&#41;](extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 [Abilitare TDE usando EKM](enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)  
  
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql)  
  
 [Ripristino di una chiave master del database](restore-a-database-master-key.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Eliminare e ricreare chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Aggiungere e rimuovere le chiavi di crittografia per una distribuzione con scalabilità orizzontale &#40;Gestione configurazione SSRS&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [Transparent Data Encryption &#40;TDE&#41;](transparent-data-encryption.md)  
  
  
