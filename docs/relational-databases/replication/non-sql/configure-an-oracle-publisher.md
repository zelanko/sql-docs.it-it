---
title: Configurare un server di pubblicazione Oracle | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], configuring
ms.assetid: 240c8416-c8e5-4346-8433-07e0f779099f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b2b277707c8da44d141036c7e19055383c6c56a8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900011"
---
# <a name="configure-an-oracle-publisher"></a>Configurazione di un server di pubblicazione Oracle
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  La creazione di una pubblicazione nei server di pubblicazione Oracle avviene in maniera analoga al processo di creazione delle comuni pubblicazioni snapshot e transazionali, ma prima di poter effettivamente eseguire questo processo è necessario completare la procedura seguente (i primi quattro passaggi verranno descritti in dettaglio di seguito in questo argomento):  
  
1.  Creare un utente di amministrazione della replica nel database Oracle utilizzando l'apposito script.  
  
2.  Concedere direttamente (invece che con un ruolo) all'utente di amministrazione di Oracle creato nel passaggio 1 l'autorizzazione SELECT per ogni tabella pubblicata.  
  
3.  Installare il software client Oracle e il provider OLE DB nel server di distribuzione [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e quindi arrestare e riavviare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se il server di distribuzione viene eseguito su una piattaforma a 64 bit è necessario usare la versione a 64 bit del provider OLE DB Oracle.  
  
4.  Configurare il database Oracle come server di pubblicazione nel server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta gli scenari eterogenei seguenti per la replica transazionale e snapshot:  
  
-   Pubblicazione di dati da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  

-   Pubblicazione di dati da e verso Oracle con le limitazioni seguenti:  

  | |2016 o versioni precedenti |2017 o versioni successive |
  |-------|-------|--------|
  |Replica da Oracle |Supporta solo Oracle 10g o versioni precedenti |Supporta solo Oracle 10g o versioni precedenti |
  |Replica verso Oracle |Fino a Oracle 12c |Non supportate |

 La replica eterogenea a Sottoscrittori non SQL Server è deprecata. La pubblicazione Oracle è deprecata. Per spostare dati, creare soluzioni utilizzando Change Data Capture e [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  


 Per un elenco di oggetti che possono essere replicati da un database Oracle, vedere [Considerazioni e limitazioni relative alla progettazione dei server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
> [!NOTE]  
>  Per poter abilitare un server di pubblicazione o di distribuzione e creare una pubblicazione o una sottoscrizione Oracle da una pubblicazione Oracle, è necessario essere membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="creating-the-replication-administrative-user-schema-within-the-oracle-database"></a>Creazione di uno schema utente di amministrazione della replica all'interno del database Oracle  
 Gli agenti di replica si connettono al database Oracle e svolgono operazioni nel contesto di uno schema utente che deve essere appositamente creato. A questo schema devono essere concesse alcune autorizzazioni, elencate nella sezione successiva. A tale schema appartengono tutti gli oggetti creati dal processo di replica di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sul server di pubblicazione Oracle, ad eccezione del sinonimo pubblico **MSSQLSERVERDISTRIBUTOR**. Per ulteriori informazioni sugli oggetti creati nel database Oracle, vedere [Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md).  
  
> [!NOTE]  
>  Eliminando il sinonimo pubblico **MSSQLSERVERDISTRIBUTOR** e l’utente della replica Oracle configurato con l’opzione **CASCADE** vengono rimossi tutti gli oggetti di replica dalla pubblicazione Oracle.  
  
 È disponibile uno script di esempio che consente di agevolare la configurazione dello schema utente di replica Oracle. Dopo l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], lo script è disponibile nella directory *\<drive>* :\\\Programmi\Microsoft SQL Server\\ *\<InstanceName>* \MSSQL\Install\oracleadmin.sql. È inoltre descritto in [Script to Grant Oracle Permissions](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md).  
  
 Connettersi al database Oracle utilizzando un account con privilegi DBA ed eseguire lo script. Lo script richiede l'indicazione del nome utente e della password per lo schema utente di amministrazione della replica e dello spazio tabella in cui creare gli oggetti (lo spazio tabella deve essere già disponibile nel database Oracle). Per informazioni sull'impostazione di altri spazi tabella per gli oggetti, vedere [Gestire spazi di tabella Oracle](../../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md). Scegliere un nome utente e una password complessa e prenderne nota perché vanno specificati durante la configurazione del database Oracle come server di pubblicazione. È consigliabile utilizzare lo schema solo per gli oggetti necessari alla replica ed evitare di creare tabelle da pubblicare in questo schema.  
  
### <a name="creating-the-user-schema-manually"></a>Creazione manuale di uno schema utente  
 Se si crea manualmente uno schema utente di amministrazione della replica, è necessario concedere allo schema le autorizzazioni seguenti, in modo diretto o tramite un ruolo di database.  
  
-   CREATE PUBLIC SYNONYM e DROP PUBLIC SYNONYM  
  
-   CREATE PROCEDURE  
  
-   CREATE SEQUENCE  
  
-   CREATE SESSION  
  
 È inoltre necessario concedere direttamente le autorizzazioni seguenti all'utente (senza utilizzare un ruolo):  
  
-   CREATE ANY TRIGGER. È obbligatorio solo in caso di replica transazionale e snapshot.  
  
-   CREA TABELLA  
  
-   CREATE VIEW  
  
## <a name="installing-and-configuring-oracle-client-networking-software-on-the-sql-server-distributor"></a>Installazione e configurazione del software di rete client Oracle nel server di distribuzione SQL Server  
 È necessario installare e configurare il software di rete client Oracle e il provider OLE DB Oracle sul server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] affinché il server di distribuzione possa creare connessioni con il server di pubblicazione Oracle. Dopo aver installato il software, impostare le autorizzazioni appropriate per le cartelle in cui è installato il software e arrestare e riavviare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per garantire che tutte le impostazioni vengano aggiornate (le autorizzazioni verranno descritte di seguito nella sezione "Impostazione delle autorizzazioni per le directory").  
  
> [!NOTE]  
>  La versione del software di rete client Oracle deve essere aggiornata. È consigliabile installare l'ultima versione del software client. Per tale motivo, la versione del software client è spesso successiva a quella del software del database.  
  
 Il modo più diretto per installare e configurare il software di rete client consiste nell'utilizzare Oracle Universal Installer e Net Configuration Assistant dal disco del client Oracle.  
  
 In Oracle Universal Installer è necessario inserire le informazioni seguenti:  
  
|Informazioni|Descrizione|  
|-----------------|-----------------|  
|Oracle Home|Percorso della directory di installazione del software Oracle. Accettare il percorso predefinito (C:\oracle\ora90 o simile) o inserirne un altro. Per ulteriori informazioni su Oracle Home, vedere la sezione relativa alle considerazioni su Oracle Home più avanti in questo argomento.|  
|Oracle home name|Alias del percorso di Oracle Home.|  
|Installation type|In Oracle 10g, selezionare l'opzione di installazione **Administrator** .|  
  
 Dopo aver completato la procedura di Oracle Universal Installer, utilizzare Net Configuration Assistant per configurare la connettività di rete. È necessario indicare quattro informazioni per configurare la connettività di rete. L'amministratore del database Oracle definisce la configurazione di rete quando imposta il database e il listener e deve essere in grado di offrire queste informazioni se l'utente non le possiede. Eseguire le operazioni seguenti:  
  
|Azione|Descrizione|  
|------------|-----------------|  
|Identificazione del database|Per l'identificazione del database sono disponibili due modalità. La prima modalità utilizza il SID (Oracle System Identifier) ed è disponibile in ogni release di Oracle. La seconda utilizza il Service Name, disponibile a partire da Oracle 8.0. Entrambe le modalità utilizzano un valore configurato alla creazione del database ed è importante che la configurazione di rete del client utilizzi la stessa modalità di denominazione utilizzata dall'amministratore nella configurazione del listener per il database.|  
|Identificazione di un alias di rete per il database|È necessario specificare un alias di rete che verrà utilizzato per accedere al database Oracle. L'alias deve inoltre essere specificato quando si identifica il database Oracle come server di pubblicazione nel server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Si tratta in sostanza di un puntatore al Service Name o al SID remoto che è stato configurato quando è stato creato il database. Per l'alias di rete sono stati utilizzati diversi nomi nelle diverse release e nei diversi prodotti Oracle, tra cui Net Service Name e TNS Alias. SQL*Plus richiede questo alias come parametro "Host String" al momento dell'accesso.|  
|Selezione del protocollo di rete|Selezionare i protocolli appropriati che si desidera supportare. La maggioranza delle applicazioni utilizza il protocollo TCP.|  
|Inserimento dei dati host per identificare il listener del database|L'host è il nome o l'alias DNS del computer su cui viene eseguito il listener Oracle, in genere lo stesso computer contenente il database. Per alcuni protocolli è necessario indicare informazioni aggiuntive. Ad esempio, se si seleziona il protocollo TCP è necessario indicare la porta su cui il listener rimane in attesa di richieste di connessione al database di destinazione. La configurazione TCP predefinita utilizza la porta 1521.|  
  
### <a name="setting-directory-permissions"></a>Impostazione delle autorizzazioni per le directory  
 All'account utilizzato per eseguire il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sul server di distribuzione devono essere concesse autorizzazioni di lettura ed esecuzione per la directory e per tutte le relative sottodirectory in cui è installato il software di rete client Oracle.  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>Verifica della connettività tra il server di distribuzione SQL Server e il server di pubblicazione Oracle  
 Nei passaggi finali di Net Configuration Assistant può essere disponibile un'opzione che consente di testare la connessione al server di pubblicazione Oracle. Prima di verificare la connessione, verificare che l'istanza del database Oracle sia online e che il listener Oracle sia in esecuzione. Se la verifica non riesce, rivolgersi al DBA Oracle responsabile del database a cui si tenta di connettersi.  
  
 Dopo aver stabilito una connessione al server di pubblicazione Oracle, tentare di eseguire l'accesso al database utilizzando l'account e la password associati allo schema utente di amministrazione della replica creato. La procedura seguente deve essere eseguita utilizzando lo stesso account di Windows adoperato dal servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
1.  Fare clic sul pulsante **Start**e quindi scegliere **Esegui**.  
  
2.  Digitare `cmd` e fare clic su **OK**.  
  
3.  Al prompt dei comandi digitare:  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     Ad esempio: `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  Se la configurazione di rete è riuscita è possibile accedere e viene visualizzato il prompt `SQL`.  
  
5.  Se si verificano problemi durante la connessione al database Oracle, vedere la sezione relativa ai problemi di connessione del server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] all'istanza di database Oracle in [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).  
  
### <a name="considerations-for-oracle-home"></a>Considerazioni su Oracle Home  
 Oracle supporta l'installazione side-by-side di file binari dell'applicazione, ma la replica può utilizzare un solo set di file binari alla volta. Ogni set di file binari è associato a un Oracle Home; tali file si trovano nella directory %ORACLE_HOME%\bin. Quando la replica stabilisce le connessioni al server di pubblicazione Oracle è necessario verificare che venga utilizzato il set corretto di file binari, in particolare la versione più recente del software di rete client.  
  
 Accedere al server di distribuzione con gli account utilizzati dal servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e dal servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent e impostare le corrette variabili d'ambiente. La variabile %ORACLE_HOME% deve essere impostata in modo da fare riferimento al punto di installazione specificato quando è stato installato il software client di rete. %PATH% deve includere la directory %ORACLE_HOME% \bin come prima voce Oracle rilevata. Per informazioni sull'impostazione delle variabili d'ambiente, vedere la documentazione di Windows.  
  
## <a name="configuring-the-oracle-database-as-a-publisher-at-the-sql-server-distributor"></a>Configurazione del database Oracle come server di pubblicazione nel server di distribuzione SQL Server  
 Poiché i server di pubblicazione Oracle utilizzano sempre un server di distribuzione remoto, è necessario configurare un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] affinché funga da server di distribuzione per il server di pubblicazione Oracle (un server di pubblicazione Oracle può utilizzare un solo server di distribuzione, mentre un server di distribuzione può gestire più di un server di pubblicazione Oracle). Dopo aver configurato un server di distribuzione, identificare l'istanza di database Oracle come server di pubblicazione nel server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], Transact-SQL o RMO (Replication Management Objects). Per altre informazioni sulla configurazione di un database di distribuzione, vedere [Configurare la distribuzione](../../../relational-databases/replication/configure-distribution.md).  
  
> [!NOTE]  
>  Il nome del server di pubblicazione Oracle non può essere identico a quello del relativo server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o di alcun server di pubblicazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che utilizzi lo stesso server di distribuzione.  
  
 Quando si identifica il database Oracle come server di pubblicazione, è necessario scegliere un'opzione di pubblicazione Oracle: Complete o Oracle Gateway. Dopo aver identificato un server di pubblicazione, questa opzione può essere modificata solo eliminando e riconfigurando il server di pubblicazione. L'opzione Complete è progettata per offrire alle pubblicazioni snapshot e transazionali il set completo di funzionalità supportate per la pubblicazione Oracle. L'opzione Oracle Gateway prevede ottimizzazioni della progettazione specifiche per migliorare le prestazioni quando la replica funge da gateway tra i sistemi.  
  
 Dopo l'identificazione del server di pubblicazione Oracle nel server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , la replica crea un server collegato con nome identico a quello del servizio TNS del database Oracle. Tale server può essere utilizzato solo dalla replica. Se è necessario connettersi al server di pubblicazione Oracle tramite una connessione al server collegato, creare un altro nome di servizio TNS e quindi usare tale nome nella chiamata a [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 Per configurare un server di pubblicazione Oracle e creare una pubblicazione, vedere [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni amministrative per i server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/administrative-considerations-for-oracle-publishers.md)   
 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Glossario dei termini per la pubblicazione Oracle](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Panoramica della pubblicazione Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
