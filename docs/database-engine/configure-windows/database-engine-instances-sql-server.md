---
title: Istanza del motore di database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: af9ae643-9866-4014-b36f-11ab556a773e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2d5f89f5e3aa801386642bfb75470cef15db6e96
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68012049"
---
# <a name="database-engine-instances-sql-server"></a>Istanza del motore di database (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] è una copia del file eseguibile **sqlservr.exe** che viene eseguita come un servizio del sistema operativo. Ogni istanza gestisce diversi database di sistema e uno o più database utente. Ciascun computer può eseguire più istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Le applicazioni si connettono all'istanza per eseguire attività in un database gestito dall'istanza.  
  
## <a name="instances"></a>Istanze  
 Un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] funziona come un servizio che gestisce ogni richiesta dell'applicazione per utilizzare i dati in qualsiasi database gestito da quell'istanza. È la destinazione delle richieste di connessione (accessi) da parte delle applicazioni. La connessione attraversa una connessione di rete se l'applicazione e l'istanza si trovano in computer separati. Se l'applicazione e l'istanza sono nello stesso computer, la connessione di SQL Server può essere eseguita come una connessione di rete o una connessione in memoria. Una volta completata una connessione, un'applicazione invia le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] attraverso la connessione all'istanza. L'istanza risolve le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] in operazioni rispetto ai dati e agli oggetti nei database e, se le autorizzazioni necessarie sono state concesse alle credenziali di accesso, esegue l'attività. Qualsiasi dato recuperato viene restituito all'applicazione, insieme a qualsiasi messaggio, come ad esempio errori.  
  
 È possibile eseguire più istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] sullo stesso computer. Un'istanza può essere l'istanza predefinita. L'istanza predefinita non ha nome. Se una richiesta di connessione specifica solo il nome del computer, viene effettuata la connessione all'istanza predefinita. Un'istanza denominata è un'istanza di cui si specifica il nome al momento della relativa installazione. Una richiesta di connessione deve specificare il nome del computer e il nome dell'istanza affinché sia stabilita la connessione all'istanza. Non c'è nessun requisito per installare un'istanza predefinita; tutte le istanze in esecuzione su un computer possono essere istanze denominate.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritto come configurare le proprietà di un'istanza. Configurare impostazioni predefinite quali percorsi del file e formati della data o il modo in cui l'istanza utilizza le risorse del sistema operativo, ad esempio memoria o thread.|[Configurare le istanze del motore di database &#40;SQL Server&#41;](../../database-engine/configure-windows/configure-database-engine-instances-sql-server.md)|  
|Viene descritto come gestire le regole di confronto di un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Le regole di confronto definiscono i modelli di bit utilizzati per la rappresentazione dei carattere e i comportamenti associati come l'ordinamento o la distinzione tra caratteri maiuscoli e minuscoli o accentati e non accentati nelle operazioni di confronto.|[Regole di confronto e supporto Unicode](../../relational-databases/collations/collation-and-unicode-support.md)|  
|Viene descritto come configurare le definizioni del server collegato, consentendo alle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] di essere eseguite in un'istanza per utilizzare dati archiviati in origini dati OLE DB separate.|[Server collegati &#40;Motore di database&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)|  
|Viene descritto come creare un trigger LOGON, specificando le azioni da intraprendere dopo la convalida di un tentativo di accesso, ma prima che siano utilizzate le risorse all'interno dell'istanza. I trigger LOGON supportano azioni quali registrazione dell'attività di connessione o limitazione dell'accesso basata sulla logica, oltre all'autenticazione delle credenziali eseguita da Windows e SQL Server.|[Trigger LOGON](../../relational-databases/triggers/logon-triggers.md)|  
|Viene descritto come gestire il servizio associato a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Sono incluse azioni quali avviare e arrestare il servizio o configurare opzioni di avvio.|[Gestire il servizio Motore di database](../../database-engine/configure-windows/manage-the-database-engine-services.md)|  
|Viene descritto come eseguire le attività di configurazione di rete del server, quali l'abilitazione di protocolli, la modifica della porta o della pipe utilizzata da un protocollo, la configurazione della crittografia, la configurazione del servizio SQL Server Browser, l'eventuale esposizione del Motore di database di SQL Server nella rete e la registrazione del nome SPN.|[Configurazione di rete del server](../../database-engine/configure-windows/server-network-configuration.md)|  
|Viene descritto come eseguire le attività di configurazione della rete client quali la configurazione dei protocolli client e la creazione o l'eliminazione di un alias di server.|[Configurazione di rete dei client](../../database-engine/configure-windows/client-network-configuration.md)|  
|Vengono descritti gli editor [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] che possono essere utilizzati per la progettazione, il debug e l'esecuzione di script quali script [!INCLUDE[tsql](../../includes/tsql-md.md)] . Viene descritta anche la procedura per codificare script di Windows PowerShell da utilizzare con componenti di SQL Server.|[Script del motore di database](../../relational-databases/scripting/database-engine-scripting.md)|  
|Viene descritto come utilizzare piani di manutenzione per specificare un flusso di lavoro di attività di comune amministrazione per un'istanza. I flussi di lavoro includono attività quali backup di database e aggiornamento di statistiche per migliorare le prestazioni.|[Piani di manutenzione](../../relational-databases/maintenance-plans/maintenance-plans.md)|  
|Viene descritto come utilizzare Resource Governor per gestire il consumo delle risorse e i carichi di lavoro specificando i limiti per la quantità di CPU e memoria che le richieste dell'applicazione possono utilizzare.|[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)|  
|Viene descritto come le applicazioni di database possono utilizzare la posta elettronica del database per inviare messaggi di posta elettronica dal [!INCLUDE[ssDE](../../includes/ssde-md.md)].|[Posta elettronica database](../../relational-databases/database-mail/database-mail.md)|  
|Viene descritto come utilizzare eventi estesi per acquisire dati relativi alle prestazioni, può essere utilizzato per compilare riferimenti per le prestazioni o diagnosticare problemi di prestazione. Gli eventi estesi sono un sistema leggero, estremamente scalabile per la raccolta di dati relativi alle prestazioni.|[Eventi estesi](../../relational-databases/extended-events/extended-events.md)|  
|Viene descritto come utilizzare Traccia SQL per compilare un sistema personalizzato al fine di acquisire e registrare eventi nel [!INCLUDE[ssDE](../../includes/ssde-md.md)].|[Traccia SQL](../../relational-databases/sql-trace/sql-trace.md)|  
|Viene descritto come utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler per acquisire tracce di richieste dell'applicazione che entrano a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. È possibile riprodurre queste tracce in un secondo momento per attività quali test delle prestazioni o diagnosi dei problemi.|[SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)|  
|Vengono descritte le funzionalità Change Data Capture e Rilevamento delle modifiche e viene indicato come utilizzare queste funzionalità per tener traccia delle modifiche ai dati in un database.|[Rilevare le modifiche ai dati &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)|  
|Viene descritto come utilizzare il visualizzatore di file di log per trovare e visualizzare errori e messaggi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nei vari log, come ad esempio la cronologia processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , i log di SQL Server e i registri eventi di Windows.|[Visualizzatore file di log](../../relational-databases/logs/log-file-viewer.md)|  
|Viene descritto come utilizzare l'Ottimizzazione guidata del [!INCLUDE[ssDE](../../includes/ssde-md.md)] per analizzare database e creare requisiti per risolvere potenziali problemi di prestazione.|[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)|  
|Viene descritto come gli amministratori del database di produzione possono stabilire una connessione diagnostica con le istanze quando non sono accettate connessioni standard.|[Connessione di diagnostica per gli amministratori di database](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)|  
|Viene descritto come utilizzare la funzionalità server remoti deprecati per abilitare l'accesso da un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] a un'altra. Il meccanismo preferito per questa funzionalità è un server collegato.|[Server remoti](../../database-engine/configure-windows/remote-servers.md)|  
|Vengono illustrate le funzionalità di Service Broker per applicazioni di messaggistica e accodamento e viene fatto riferimento alla documentazione di Service Broker.|[Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)|  
|Viene descritto come utilizzare l'estensione del pool di buffer per fornire l'integrazione diretta della RAM non volatile ( unità SSD) al pool di buffer del motore di database per migliorare la velocità effettiva di I/O in maniera significativa.|[File di estensione del pool di buffer](../../database-engine/configure-windows/buffer-pool-extension.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazione sqlservr](../../tools/sqlservr-application.md)   
 [Caratteristiche del database](../../relational-databases/database-features.md)   
 [Caratteristiche del motore di database tra istanze](../../relational-databases/database-engine-cross-instance-features.md)  
  
  
