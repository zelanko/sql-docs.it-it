---
description: Attività Trasferisci database
title: Attività Trasferisci database | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferdatabasetask.f1
- sql13.dts.designer.transferdatabasetask.general.f1
- sql13.dts.designer.transferdatabasetask.database.f1
- sql13.dts.designer.transferdatabasetask.sourcedbfiles.f1
- sql13.dts.designer.transferdatabasetask.destdbfiles.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3421b1c839504c01ecb256530cb579c18f043b86
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192799"
---
# <a name="transfer-database-task"></a>Attività Trasferisci database

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  L'attività Trasferisci database trasferisce un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tra due istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A differenza di altre attività che trasferiscono oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo eseguendone una copia, l'attività Trasferisci database può copiare o spostare un database. Tramite questa attività è inoltre possibile copiare un database all'interno dello stesso server.  
  
## <a name="offline-and-online-modes"></a>Modalità offline e online  
 Il database può essere trasferito in modalità online o offline. Nella modalità online il database rimane collegato e viene trasferito tramite SQL Management Object (SMO) per la copia degli oggetti di database. Nella modalità offline il database viene scollegato, i corrispondenti file vengono copiati o spostati e il database viene quindi collegato alla destinazione dopo essere stato trasferito correttamente. Se il database viene copiato, viene ricollegato automaticamente all'origine, quando la copia ha esito positivo. Nella modalità offline la copia del database viene eseguita più rapidamente, ma durante il trasferimento il database non è disponibile agli utenti.  
  
 Quando si utilizza la modalità offline, è necessario specificare le condivisioni file di rete del server di origine e di destinazione in cui si trovano i file di database. Se la cartella è condivisa e accessibile dall'utente, è possibile fare riferimento alla condivisione di rete in base alla sintassi \\\nomecomputer\Programmi\cartellapersonale\\. In caso contrario, è necessario adottare la sintassi \\\nomecomputer\c$\Programmi\cartellapersonale\\. Per poter utilizzare questa seconda sintassi, l'utente deve disporre dell'accesso in scrittura alle condivisioni di rete nell'origine e nella destinazione.  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>Trasferimento di database tra versioni di SQL Server  
 L'attività Trasferisci database consente di trasferire un database tra istanze di versioni diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventi  
 L'attività Trasferisci database non visualizza lo stato incrementale del trasferimento di messaggi di errore, ma solo il completamento 0% e 100%.  
  
## <a name="execution-value"></a>Valore di esecuzione  
 Il valore di esecuzione, definito nella proprietà **ExecutionValue** dell'attività, restituisce il valore 1, in quanto a differenza di altre attività di trasferimento, l'attività Trasferisci database può trasferire un solo database.  
  
 Tramite l'assegnazione di una variabile definita dall'utente alla proprietà **ExecValueVariable** dell'attività, le informazioni sul trasferimento dei messaggi di errore possono essere rese disponibili ad altri oggetti del pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](../integration-services-ssis-variables.md).  
  
## <a name="log-entries"></a>Voci di log  
 L'attività Trasferisci database include le voci di log personalizzate seguenti:  
  
-   SourceSQLServer    Indica il nome del server di origine.  
  
-   DestSQLServer    Indica il nome del server di destinazione.  
  
-   SourceDB    Indica il nome del database trasferito.  
  
 Viene scritta inoltre una voce di log per l'evento **OnInformation** quando il database di destinazione viene sovrascritto.  
  
## <a name="security-and-permissions"></a>Sicurezza e autorizzazioni  
 Per poter trasferire un database in modalità offline, l'utente che esegue il pacchetto deve essere membro del ruolo del server _sysadmin.  
  
 Per poter trasferire un database in modalità online, l'utente che esegue il pacchetto deve essere membro del ruolo del server sysadmin o il proprietario (dbo) del database selezionato.  
  
## <a name="configuration-of-the-transfer-database-task"></a>Configurazione dell'attività Trasferisci database  
 È possibile specificare se, in caso di trasferimento non riuscito, deve essere eseguito un altro tentativo di collegamento del database di origine.  
  
 È inoltre possibile configurare l'attività Trasferisci database in modo da consentire la sovrascrittura di un database di destinazione avente lo stesso nome.  
  
 Il database di origine può essere inoltre rinominato durante il processo di trasferimento. Se si desidera trasferire un database in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è presente un database avente lo stesso nome, per consentire il trasferimento è necessario rinominare il database di origine. È tuttavia necessario che anche i nomi dei file di database siano diversi. Se hanno lo stesso nome di altri file presenti nella destinazione, l'attività ha esito negativo.  
  
 Quando si copia un database, le dimensioni del database non possono essere inferiori alle dimensioni del database **model** sul server di destinazione. È possibile incrementare le dimensioni del database da copiare oppure ridurre le dimensioni di **model**.  
  
 In fase di esecuzione, l'attività Trasferisci database si connette ai server di origine e di destinazione utilizzando una o più gestioni connessioni SMO. Quando si crea la copia di un database nello stesso server, è richiesta una sola gestione connessione SMO. Le gestioni connessioni SMO vengono configurate separatamente dall'attività Trasferisci database, che tuttavia vi fa riferimento. Le gestioni connessioni SMO specificano il server e la modalità di autenticazione da utilizzare durante l'accesso dell'attività al server. Per altre informazioni, vedere [Gestione connessione file](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Pagina Espressioni](../../integration-services/expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>Configurazione a livello di codice dell'attività Trasferisci database  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
## <a name="transfer-database-task-editor-general-page"></a>Editor attività Trasferisci database (pagina Generale)
  Utilizzare la pagina **Generale** dell' **Editor attività Trasferisci database** per assegnare un nome all'attività Trasferisci database e descriverla. Questa attività consente di copiare o spostare un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tra due istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Tramite questa attività è inoltre possibile copiare un database all'interno dello stesso server.   
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare un nome univoco per l'attività Trasferisci database. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Trasferisci database.  
  
## <a name="transfer-database-task-editor-databases-page"></a>Editor attività Trasferisci database (pagina Database)
  Utilizzare la pagina **Database** della finestra di dialogo **Editor attività Trasferisci database** per specificare le proprietà relative ai database di origine e destinazione interessati dall'attività Trasferisci database. Questa attività consente di copiare o spostare un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tra due istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Tramite questa attività è inoltre possibile copiare un database all'interno dello stesso server.  
  
### <a name="options"></a>Opzioni  
 **SourceConnection**  
 Selezionare una gestione connessione SMO nell'elenco oppure fare clic su **\<New connection...>** per creare una nuova connessione al server di origine.  
  
 **DestinationConnection**  
 Selezionare una gestione connessione SMO nell'elenco oppure fare clic su **\<New connection...>** per creare una nuova connessione al server di destinazione.  
  
 **DestinationDatabaseName**  
 Specificare il nome del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel server di destinazione.  
  
 Per inserire automaticamente il nome del database di origine in questo campo, specificare innanzitutto **SourceConnection** e **SourceDatabaseName** .  
  
 Per rinominare il database nel server di destinazione, digitare il nuovo nome in questo campo.  
  
 **DestinationDatabaseFiles**  
 Indica i nomi e i percorsi dei file di database nel server di destinazione.  
  
 Per inserire automaticamente i nomi e i percorsi dei file del database di origine in questo campo, specificare innanzitutto **SourceConnection**, **SourceDatabaseName**e **SourceDatabaseFiles** .  
  
 Per rinominare i file di database o specificare i nuovi percorsi nel server di destinazione, inserire in questo campo le informazioni sul database di origine e quindi fare clic sul pulsante Sfoglia. Nella finestra di dialogo **File di database di destinazione** modificare **File di destinazione**, **Cartella di destinazione**o **Condivisione file di rete**.  
  
> [!NOTE]  
>  Se i file di database vengono individuati tramite il pulsante Sfoglia, il percorso dei file viene immesso usando l'annotazione dell'unità locale, ad esempio c:\\. È necessario sostituire questa annotazione con quella di condivisione di rete, includendo il nome del computer e il nome di condivisione. In caso di condivisione amministrativa predefinita, è necessario utilizzare l'annotazione $ e disporre di accesso amministrativo alla condivisione.  
  
 **DestinationOverwrite**  
 Indicare se il database nel server di destinazione può essere sovrascritto.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**True**|Sovrascrive il database del server di destinazione.|  
|**False**|Non sovrascrive il database del server di destinazione.|  
  
> [!CAUTION]  
>  Se si specifica **True** per la proprietà **DestinationOverwrite**, i dati inclusi nel database del server di destinazione verranno sovrascritti ed è possibile che si verifichi una perdita di dati. Per evitare che i dati vadano perduti, procedere a un backup del database del server di destinazione in un'altra posizione prima di eseguire l'attività Trasferisci database.  
  
 **Azione**  
 Indicare se l'attività eseguirà il comando **Copia** o **Sposta** il database nel server di destinazione.  
  
 **Metodo**  
 Indicare se l'attività deve essere eseguita quando il database nel server di origine è in modalità online o offline.  
  
 Per trasferire un database in modalità offline, l'utente che esegue il pacchetto deve essere un membro del ruolo predefinito del server **sysadmin** .  
  
 Per trasferire un database in modalità online, l'utente che esegue il pacchetto deve essere un membro del ruolo predefinito del server **sysadmin** o il proprietario (**dbo**) del database selezionato.  
  
 **SourceDatabaseName**  
 Selezionare il nome del database da copiare o spostare.  
  
 **SourceDatabaseFiles**  
 Fare clic sul pulsante Sfoglia per selezionare i file di database.  
  
 **ReattachSourceDatabase**  
 Indicare se l'attività tenterà di ricollegare il database di origine in caso di errore.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**True**|Ricollega il database di origine.|  
|**False**|Non ricollega il database di origine.|  

## <a name="source-database-files"></a>File di database di origine
  Utilizzare la finestra di dialogo **File di database di origine** per visualizzare i nomi e i percorsi dei file di database nel server di origine oppure per specificare il percorso di condivisione dei file in rete per l'attività Trasferisci database.   
  
 Per popolare questa finestra di dialogo con i nomi e i percorsi dei file di database nel server di origine, impostare innanzitutto le opzioni **SourceConnection** e **SourceDatabaseName** nelle pagine **Database** della finestra di dialogo **Editor attività Trasferisci database** .  
  
### <a name="options"></a>Opzioni  
 **File di origine**  
 Nomi dei file di database nel server di origine che verranno trasferiti. Il valore**File di origine** è di sola lettura.  
  
 **Cartella di origine**  
 Cartella nel server di origine in cui si trovano i file di database da trasferire. Il valore**Cartella di origine** è di sola lettura.  
  
 **Condivisione file di rete**  
 Cartella di rete condivisa nel server di origine da cui verranno trasferiti i file di database. Utilizzare **Condivisione file di rete** quando si trasferisce un database in modalità offline impostando l'opzione **DatabaseOffline** per **Metodo** nella pagina **Database** della finestra di dialogo **Editor attività Trasferisci database** .  
  
 Digitare il percorso della condivisione file di rete oppure fare clic sul pulsante Sfoglia **(...)** per individuarlo.  
  
 Quando si trasferisce un database in modalità offline, i rispettivi file vengono copiati nel percorso specificato in **Condivisione file di rete** nel server di origine prima di essere trasferiti al server di destinazione.  

## <a name="destination-database-files"></a>File di database di destinazione
  Utilizzare la finestra di dialogo **File di database di destinazione** per visualizzare o modificare i percorsi e i nomi dei file di database nel server di destinazione oppure per specificare un percorso di file di rete per l'attività Trasferisci database.  
  
 Per inserire automaticamente i percorsi e i nomi dei file di database del server di origine in questa finestra di dialogo, specificare innanzitutto le proprietà **SourceConnection**, **SourceDatabaseName**e **SourceDatabaseFiles** nella pagina **Database** della finestra di dialogo **Editor attività Trasferisci database** .  
  
### <a name="options"></a>Opzioni  
 **File di destinazione**  
 Nomi dei file di database trasferiti nel server di destinazione.  
  
 Immettere il nome del file o fare clic sul nome del file per modificarlo.  
  
 **Cartella di destinazione**  
 Cartella del server di destinazione in cui verranno trasferiti i file di database.  
  
 Immettere il percorso della cartella, fare clic su tale percorso per modificarlo oppure fare clic su Sfoglia per individuare la cartella del server di destinazione in cui trasferire i file di database.  
  
 **Condivisione file di rete**  
 Cartella di condivisione dei file di rete del server di destinazione in cui verranno trasferiti i file di database. Utilizzare **Condivisione file di rete** quando si trasferisce un database in modalità offline specificando **DatabaseOffline** per **Metodo** nella pagina **Database** della finestra di dialogo **Editor attività Trasferisci database** .  
  
 Immettere il percorso di condivisione dei file di rete o fare clic su Sfoglia per individuarlo.  
  
 Durante il trasferimento di un database in modalità offline, prima di essere trasferiti nella posizione **Cartella di destinazione** , i file di database vengono copiati nella cartella **Condivisione file di rete** .