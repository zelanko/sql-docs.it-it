---
description: Sottoscrittori Oracle
title: Sottoscrittori Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- data types [SQL Server replication], non-SQL Server Subscribers
- Oracle Subscribers [SQL Server replication]
- non-SQL Server Subscribers, Oracle
- heterogeneous Subscribers, Oracle
- mapping data types [SQL Server replication]
ms.assetid: 591c0313-82ce-4689-9fc1-73752ff122cf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3e7b6abc6b235950fef107a870e53d827dee6f5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455603"
---
# <a name="oracle-subscribers"></a>Sottoscrittori Oracle
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  A partire da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta le sottoscrizioni push a Oracle tramite il provider Oracle OLE DB fornito da Oracle.  
  
## <a name="configuring-an-oracle-subscriber"></a>Configurazione di un Sottoscrittore Oracle  
 Per configurare un Sottoscrittore Oracle, eseguire la procedura seguente:  
  
1.  Installare e configurare il software client Oracle di rete e il provider OLE DB appropriato sul server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in modo che questo possa connettersi al Sottoscrittore Oracle. Il software client Oracle di rete deve essere dell'ultima versione disponibile. È consigliabile installare l'ultima versione del software client. Per tale motivo, la versione del software client è spesso successiva a quella del software del database. Il modo più diretto per installare e configurare il software consiste nell'utilizzare Oracle Universal Installer presente nel disco di Oracle Client. In Oracle Universal Installer, è necessario inserire le informazioni seguenti:  
  
    |Informazioni|Descrizione|  
    |-----------------|-----------------|  
    |Oracle Home|Percorso della directory di installazione del software Oracle. Accettare il percorso predefinito (C:\oracle\ora90 o simile) o inserirne un altro. Per ulteriori informazioni su Oracle Home, vedere la sezione relativa alle considerazioni su Oracle Home più avanti in questo argomento.|  
    |Oracle home name|Alias del percorso di Oracle Home.|  
    |Installation type|In Oracle 10g, selezionare l'opzione di installazione **Runtime** o **Administrator** .|  
  
2.  Creare un nome TNS per il Sottoscrittore. TNS (Transparent Network Substrate) è un livello di comunicazione utilizzato dai database Oracle. Il nome del servizio TNS è il nome con cui un'istanza di database Oracle viene riconosciuta in una rete. Il nome del servizio TNS viene assegnato durante la configurazione della connettività per il database Oracle. La replica utilizza il TNS Service Name per identificare il Sottoscrittore e per stabilire le connessioni.  
  
     Dopo aver completato la procedura di Oracle Universal Installer, utilizzare Net Configuration Assistant per configurare la connettività di rete. È necessario indicare quattro informazioni per configurare la connettività di rete. L'amministratore del database Oracle definisce la configurazione di rete quando imposta il database e il listener e deve essere in grado di offrire queste informazioni se l'utente non le possiede. Eseguire le operazioni seguenti:  
  
    |Azione|Descrizione|  
    |------------|-----------------|  
    |Identificazione del database|Per l'identificazione del database sono disponibili due modalità. La prima modalità utilizza il SID (Oracle System Identifier) ed è disponibile in ogni release di Oracle. La seconda utilizza il Service Name, disponibile a partire da Oracle 8.0. Entrambe le modalità utilizzano un valore configurato alla creazione del database ed è importante che la configurazione di rete del client utilizzi la stessa modalità di denominazione utilizzata dall'amministratore nella configurazione del listener per il database.|  
    |Identificazione di un alias di rete per il database|È necessario specificare un alias di rete che verrà utilizzato per accedere al database Oracle. Si tratta in sostanza di un puntatore al Service Name o al SID remoto che è stato configurato quando è stato creato il database. Per l'alias di rete sono stati utilizzati diversi nomi nelle diverse release e nei diversi prodotti Oracle, tra cui Net Service Name e TNS Alias. SQL*Plus richiede questo alias come parametro "Host String" al momento dell'accesso.|  
    |Selezione del protocollo di rete|Selezionare i protocolli appropriati che si desidera supportare. La maggioranza delle applicazioni utilizza il protocollo TCP.|  
    |Inserimento dei dati host per identificare il listener del database|L'host è il nome o l'alias DNS del computer su cui viene eseguito il listener Oracle, in genere lo stesso computer contenente il database. Per alcuni protocolli è necessario indicare informazioni aggiuntive. Ad esempio, se si seleziona il protocollo TCP è necessario indicare la porta su cui il listener rimane in attesa di richieste di connessione al database di destinazione. La configurazione TCP predefinita utilizza la porta 1521.|  
  
3.  Creare uno snapshot o una pubblicazione transazionale, abilitarlo per i Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , quindi creare una sottoscrizione push per il Sottoscrittore. Per altre informazioni, vedere [Creazione di una sottoscrizione per un Sottoscrittore non SQL Server](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  

### <a name="setting-directory-permissions"></a>Impostazione delle autorizzazioni di directory  
 All'account con cui viene eseguito il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] disponibile nel server di distribuzione devono essere concesse le autorizzazioni di lettura ed esecuzione per la directory e tutte le sottodirectory in cui è installato il software client Oracle di rete.  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>Verifica della connettività tra il server di distribuzione SQL Server e il server di pubblicazione Oracle  
 In una delle fasi conclusive di Net Configuration Assistant potrebbe essere disponibile l'opzione di verifica della connessione al Sottoscrittore Oracle. Prima di verificare la connessione, verificare che l'istanza del database Oracle sia online e che il listener Oracle sia in esecuzione. Se la verifica non riesce, rivolgersi al DBA Oracle responsabile del database a cui si tenta di connettersi.  
  
 Dopo essere riusciti a stabilire la connessione con il Sottoscrittore Oracle, tentare di accedere al database utilizzando l'account e la password configurati per l'agente di distribuzione per la sottoscrizione:  
  
1.  Fare clic sul pulsante **Start**e quindi scegliere **Esegui**.  
  
2.  Digitare `cmd` e fare clic su **OK**.  
  
3.  Al prompt dei comandi digitare:  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     Ad esempio: `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  Se la configurazione di rete è riuscita, sarà possibile accedere e verrà visualizzato il prompt `SQL` .  
  
### <a name="considerations-for-oracle-home"></a>Considerazioni su Oracle Home  
 Oracle supporta l'installazione side-by-side di file binari dell'applicazione, ma la replica può utilizzare un solo set di file binari alla volta. Ogni set di file binari è associato a un Oracle Home; tali file si trovano nella directory %ORACLE_HOME%\bin. È necessario verificare che quando la replica effettua connessioni al Sottoscrittore Oracle venga utilizzato il set di file binari corretto, in particolare, l'ultima versione del software client di rete.  
  
 Accedere al server di distribuzione con gli account utilizzati dal servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e dal servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent e impostare le corrette variabili d'ambiente. La variabile %ORACLE_HOME% deve essere impostata in modo da fare riferimento al punto di installazione specificato quando è stato installato il software client di rete. %PATH% deve includere la directory %ORACLE_HOME% \bin come prima voce Oracle rilevata. Per informazioni sull'impostazione delle variabili d'ambiente, vedere la documentazione di Windows.  
  
> [!NOTE]  
>  Se sul server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono presenti più Oracle Home, verificare che l'agente di distribuzione utilizzi il provider OLE DB Oracle più recente. In alcuni casi, Oracle non aggiorna il provider OLE DB per impostazione predefinita quando vengono aggiornati i componenti del client sul server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Disinstallare il vecchio provider OLE DB e installare l'ultimo provider OLE DB. Per ulteriori informazioni sull'installazione e sulla disinstallazione del provider, vedere la documentazione di Oracle.  
  
## <a name="considerations-for-oracle-subscribers"></a>Considerazioni sui Sottoscrittori Oracle  
 Oltre alle considerazioni trattate nell'argomento [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md), è necessario considerare i seguenti problemi relativi alla replica nei Sottoscrittori Oracle:  
  
-   Oracle considera sia le stringhe vuote sia i valori NULL come NULL. Questo è importante se una colonna di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene definita come NOT NULL e si replica tale colonna in un Sottoscrittore Oracle. Per evitare errori quando si applicano le modifiche al Sottoscrittore Oracle, è necessario eseguire una delle operazioni seguenti:  
  
    -   Verificare che le stringhe vuote non vengano inserite nella tabella pubblicata come valori di colonna.  
  
    -   Usare il parametro **-SkipErrors** per l'agente di distribuzione se è accettabile ricevere una notifica degli errori nel log della cronologia dell'agente di distribuzione e continuare l'elaborazione. Specificare il codice errore Oracle 1400 (**-SkipErrors1400**).  
  
    -   Modificare lo script di creazione tabelle generato, rimuovendo l'attributo NOT NULL da qualsiasi colonna di tipo carattere a cui possano essere associate stringhe vuote e fornire lo script modificato come script di creazione personalizzato per l'articolo utilizzando il parametro @creation_script di [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
-   I Sottoscrittori Oracle supportano un'opzione di schema 0x4071. Per altre informazioni sulle opzioni di schema, vedere [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
## <a name="mapping-data-types-from-sql-server-to-oracle"></a>Mapping di tipi di dati da SQL Server ad Oracle  
 Nella tabella seguente vengono mostrati i mapping dei tipi di dati utilizzati per la replica di dati in un Sottoscrittore in cui è eseguito Oracle.  
  
|Tipo di dati di SQL Server|Tipo di dati Oracle|  
|--------------------------|----------------------|  
|**bigint**|NUMBER(19,0)|  
|**binary(1-2000)**|RAW(1-2000)|  
|**binary(2001-8000)**|BLOB|  
|**bit**|NUMBER(1)|  
|**char(1-2000)**|CHAR(1-2000)|  
|**char(2001-4000)**|VARCHAR2(2001-4000)|  
|**char(4001-8000)**|CLOB|  
|**date**|DATE|  
|**datetime**|DATE|  
|**datetime2(0-7)**|TIMESTAMP(7) per Oracle 9 e Oracle 10; VARCHAR(27) per Oracle 8|  
|**datetimeoffset(0-7)**|TIMESTAMP(7) WITH TIME ZONE per Oracle 9 e Oracle 10; VARCHAR(34) per Oracle 8|  
|**decimal(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**float(53)**|FLOAT|  
|**float**|FLOAT|  
|**geography**|BLOB|  
|**geometry**|BLOB|  
|**hierarchyid**|BLOB|  
|**image**|BLOB|  
|**int**|NUMBER(10,0)|  
|**money**|NUMBER(19,4)|  
|**nchar(1-1000)**|CHAR(1-1000)|  
|**nchar(1001-4000)**|NCLOB|  
|**ntext**|NCLOB|  
|**numeric(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**nvarchar(1-1000)**|VARCHAR2(1-2000)|  
|**nvarchar(1001-4000)**|NCLOB|  
|**nvarchar(max)**|NCLOB|  
|**real**|REAL|  
|**smalldatetime**|DATE|  
|**smallint**|NUMBER(5,0)|  
|**smallmoney**|NUMBER(10,4)|  
|**sql_variant**|N/D|  
|**sysname**|VARCHAR2(128)|  
|**text**|CLOB|  
|**time(0-7)**|VARCHAR(16)|  
|**timestamp**|RAW(8)|  
|**tinyint**|NUMBER(3,0)|  
|**uniqueidentifier**|CHAR(38)|  
|**varbinary(1-2000)**|RAW(1-2000)|  
|**varbinary(2001-8000)**|BLOB|  
|**varchar(1-4000)**|VARCHAR2(1-4000)|  
|**varchar(4001-8000)**|CLOB|  
|**varbinary(max)**|BLOB|  
|**ntext**|CLOB|  
|**xml**|NCLOB|  
  
## <a name="see-also"></a>Vedere anche  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Sottoscrizione delle pubblicazioni](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
