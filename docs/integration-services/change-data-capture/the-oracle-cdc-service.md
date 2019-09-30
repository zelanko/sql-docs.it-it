---
title: Servizio Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 47759ddc-358d-405b-acb9-189ada76ea6d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a11a67f64a40aa5fe08d375a9f11fa186c568b1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298604"
---
# <a name="the-oracle-cdc-service"></a>Servizio Oracle CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Il servizio Oracle CDC è un servizio di Windows in cui viene eseguito il programma xdbcdcsvc.exe. È possibile configurare il servizio Oracle CDC per eseguire più servizi di Windows nello stesso computer, ciascuno con un nome del servizio Windows diverso. La creazione di più servizi Windows Oracle CDC in un solo computer viene spesso effettuata per migliorare la separazione tra gli stessi o quando ciascun servizio richiede l'utilizzo di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diversa.  
  
 Un servizio Oracle CDC viene creato utilizzando Oracle CDC Service Configuration Console o definito tramite l'interfaccia della riga di comando incorporata nel programma xdbcdcsvc.exe. In entrambi i casi, ogni servizio Oracle CDC creato è associato a una sola istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , che può essere cluster o con mirroring con l'impostazione **AlwaysOn** , mentre le informazioni di connessione (stringa di connessione e credenziali di accesso) sono parte della configurazione del servizio.  
  
 Quando viene avviato, un servizio Oracle CDC tenta di connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con cui è associato, ottiene l'elenco di istanze di Oracle CDC da gestire ed esegue una convalida dell'ambiente iniziale. Gli errori durante l'avvio del servizio ed eventuali informazioni di avvio/arresto vengono sempre scritti nel registro eventi applicazioni di Windows. Quando si stabilisce una connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tutti gli errori e i messaggi informativi vengono scritti nella tabella **dbo.xdbcdc_trace** nel database MSXDBCDC dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Uno dei controlli effettuati durante l'avvio consiste nel verificare che nessun altro servizio Oracle CDC con lo stesso nome sia attualmente in esecuzione. Se un servizio con lo stesso nome è attualmente connesso da un altro computer, il servizio Oracle CDC entra in un ciclo di attesa, aspettando la disconnessione dell'altro servizio prima di procedere con la gestione dell'attività Oracle CDC.  
  
 Dopo il superamento di tutte le verifiche di avvio, il servizio Oracle CDC controlla la tabella **dbo.xdbcdc_databases** nel database MSXDBCDC per l'eventuale presenza di istanze di Oracle CDC abilitate. Per ogni istanza di Oracle CDC abilitata, il servizio avvia un sottoprocesso per gestire tale istanza di Oracle CDC.  
  
 All'avvio, un'istanza di Oracle CDC accede al database di SQL Server CDC con lo stesso nome dell'istanza di CDC e recupera lo stato dall'esecuzione precedente. Verifica inoltre che l'esecuzione proceda correttamente. Riprende quindi l'elaborazione delle modifiche, la lettura dei log delle transazioni Oracle e la scrittura delle modifiche nel database CDC.  
  
 Il servizio Oracle CDC monitorizza periodicamente la tabella **dbo.xdbcdc_tables** nel database MSXDBCDC per determinare se sono state apportate modifiche alla configurazione delle istanze di Oracle CDC. Se viene riscontrata una modifica, viene inviata una notifica dal servizio Oracle CDC all'istanza di Oracle CDC per richiedere la verifica delle modifiche della configurazione. La maggior parte delle modifiche della configurazione, ad esempio l'aggiunta e la rimozione di istanze di acquisizione, può essere applicata mentre l'istanza di Oracle CDC è abilitata, altre ne richiedono il riavvio.  
  
 Quando si utilizza Oracle CDC Designer Console, le modifiche vengono rilevate automaticamente. Quando si aggiorna direttamente la configurazione di Oracle CDC tramite SQL, è necessario chiamare la procedura riportata di seguito affinché la modifica della configurazione venga rilevata dal servizio Oracle CDC:  
  
```sql
DECLARE @dbname nvarchar(128) = 'HRcdc'  
EXECUTE [MSXDBCDC].[dbo].[xdbcdc_update_config_version] @dbname  
GO  
  
```  
  
 Tramite il processo dell'istanza di Oracle CDC, lo stato viene aggiornato nella tabella di sistema **cdc.xdbcdc_state** e le informazioni sull'errore vengono scritte nella tabella **cdc.xdbcdc_trace** . La tabella **xdbcdc_state** è utile per monitorare lo stato dell'istanza di Oracle CDC. Include lo stato aggiornato, vari contatori (ad esempio numero di modifiche lette da Oracle, numero di modifiche scritte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], numero di transazioni di cui è stato eseguito il commit scritte e numero corrente di transazioni in transito) e indicazione della latenza.  
  
 La configurazione dell'istanza di Oracle CDC viene salvata nella tabella **cdc.xdbcdc_config** , la tabella con cui interagisce Oracle CDC Designer Console. Poiché l'intera configurazione di un'istanza di Oracle CDC è presente nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione e nei database CDC, è possibile creare script di distribuzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per un'istanza di Oracle CDC. Questo risultato viene raggiunto utilizzando Oracle CDC Service Configuration Console e Oracle CDC Designer Console.  
  
## <a name="security-considerations"></a>Considerazioni sulla sicurezza  
 Di seguito vengono descritti i requisiti relativi alla sicurezza necessari per utilizzare il servizio CDC per Oracle.  
  
### <a name="protection-of-source-oracle-data"></a>Protezione dei dati Oracle di origine  
 Il servizio Oracle CDC non richiede l'accesso ai dati di origine Oracle ed è protetto assicurando che tramite le credenziali di log mining non venga fornita l'autorizzazione SELECT per le tabelle Oracle del cliente.  
  
### <a name="protection-of-source-oracle-change-data"></a>Protezione dei dati delle modifiche Oracle di origine  
 Il servizio Oracle CDC viene fornito con credenziali di log mining mediante cui vengono acquisite le modifiche apportate a qualsiasi tabella nel database Oracle. I dati delle modifiche non dispongono delle autorizzazioni di accesso granulari come le tabelle normali, pertanto per accedere a tali dati vengono ignorati i controlli di accesso ai dati predefiniti di Oracle.  
  
 Le tabelle Oracle di origine acquisite dispongono di tabelle mirror vuote con lo stesso nome di schema e di tabella nel database CDC. I dati acquisiti vengono archiviati nelle istanze di acquisizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e offrono la stessa protezione delle modifiche acquisite dal database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per accedere ai dati delle modifiche associati a un'istanza di acquisizione, l'utente deve disporre dell'autorizzazione SELECT per l'accesso a tutte le colonne acquisite della tabella mirror associata. Se, inoltre, al momento della creazione dell'istanza di acquisizione viene specificato un ruolo di controllo, il chiamante deve essere anche un membro del ruolo di controllo specificato. Le altre funzioni generali di Change Data Capture per l'accesso ai metadati sono accessibili a tutti gli utenti del database tramite il ruolo PUBLIC, sebbene l'accesso ai metadati restituiti sia inoltre in genere controllato utilizzando l'accesso SELECT alle tabelle di origine sottostanti e tramite l'appartenenza a qualsiasi ruolo di controllo definito.  
  
 Questo significa che gli utenti con ruolo predefinito del server **sysadmin** o ruolo predefinito del database **db_owner** dispongono per impostazione predefinita dell'accesso completo ai dati acquisiti ed è possibile concedere ulteriore accesso tramite ruoli di controllo o concedendo l'accesso SELECT alle colonne acquisite.  
  
### <a name="protection-of-source-oracle-log-mining-credentials"></a>Protezione delle credenziali di log mining Oracle di origine  
 La configurazione del servizio Oracle CDC, archiviato nel database CDC (nella tabella cdc.xdbcdc_config), include il nome utente di log mining e la password associata.  
  
 La password di log mining viene archiviata crittografata per mezzo di una chiave asimmetrica con il nome `xdbcdc_asym_key` fisso creato automaticamente con il comando seguente:  
  
```sql
USE [<cdc-database-name>]  
CREATE ASYMMETRIC KEY xdbcdc_asym_key  
    WITH ALGORITHM = RSA_1024  
    ENCRYPTION BY PASSWORD = '<cdc-database-name><asym-key-password>'  
  
```  
  
 Se viene utilizzato un algoritmo diverso, è possibile eliminare questa chiave e crearne una nuova con lo stesso nome e crittografata con la stessa password.  
  
 La password della chiave asimmetrica è la password master salvata nel Registro di sistema nel percorso **HKLM\Software\Microsoft\XDBCDCSVC\\<nome-servizio>** . Tale chiave è accessibile solo agli amministratori locali e all'account del servizio di Windows Oracle CDC. La chiave contiene un valore binario crittografato **AsymmetricKeyPassword** in cui è archiviata la password della chiave asimmetrica. L'accesso a questa chiave del Registro di sistema è necessario per accedere alle credenziali di log mining Oracle.  
  
 Per utilizzare la clausola ENCRYPTION BY PASSWORD, è necessario che la password soddisfi i criteri password Windows per il computer in cui viene eseguita l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A tale scopo, selezionare la password della chiave asimmetrica in base a questi criteri.  
  
 Se la password della chiave asimmetrica viene persa, è necessario specificare nuovamente le credenziali di log mining per ciascuna delle istanze di Oracle CDC nuovamente nella finestra di progettazione del servizio Oracle CDC.  
  
 La chiave asimmetrica viene creata automaticamente nel database CDC quando viene rilevata un'istanza di Oracle che non dispone di tale chiave asimmetrica o quando la chiave esiste ma la password non corrisponde.  
  
### <a name="oracle-cdc-service-windows-service-account"></a>Account del servizio di Windows del servizio Oracle CDC  
 L'account del servizio utilizzato con il servizio di Windows Oracle CDC non richiede privilegi aggiuntivi. Questo account deve essere in grado di utilizzare sia l'API di Oracle Native Client sia l'API ODBC di SQL Server Native Client. Deve essere inoltre in grado di accedere alla chiave di configurazione del servizio nel Registro di sistema; la console di configurazione del servizio CDC configura a tale scopo l'elenco di controllo di accesso (ACL).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Supporto a disponibilità elevata](../../integration-services/change-data-capture/high-availability-support.md)  
  
-   [Autorizzazioni necessarie per la connessione a SQL per il servizio CDC](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
-   [Ruoli utente](../../integration-services/change-data-capture/user-roles.md)  
  
-   [Utilizzo del servizio Oracle CDC](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di gestione di un servizio CDC locale](../../integration-services/change-data-capture/how-to-manage-a-local-cdc-service.md)   
 [Gestire un servizio Oracle CDC](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md)  
  
  
