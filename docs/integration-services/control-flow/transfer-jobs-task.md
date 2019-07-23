---
title: Attività Trasferisci processi | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferjobstask.f1
- sql13.dts.designer.transferjobstask.general.f1
- sql13.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3ae127844a2ffba0a988c23636f487673d737b2c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68011148"
---
# <a name="transfer-jobs-task"></a>Attività Trasferisci processi

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  L'attività Trasferisci processi trasferisce uno o più processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent tra istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 È possibile configurare l'attività per il trasferimento di tutti i processi o dei processi specificati. È inoltre possibile indicare se i processi trasferiti devono essere attivati o meno nella destinazione.  
  
 I processi da trasferire potrebbero essere già presenti nella destinazione. È possibile configurare l'attività Trasferisci processi per la gestione dei processi duplicati nei modi seguenti:  
  
-   I processi duplicati vengono sovrascritti.  
  
-   In presenza di processi duplicati l'attività ha esito negativo.  
  
-   I processi duplicati vengono ignorati.  
  
 In fase di esecuzione l'attività Trasferisci processi si connette al server di origine e al server di destinazione utilizzando una o più gestioni connessioni SMO. Le gestioni connessioni SMO vengono configurate separatamente dall'attività Trasferisci processi, che tuttavia vi fa riferimento. Le gestioni connessioni SMO specificano il server e la modalità di autenticazione da adottare per l'accesso al server. Per altre informazioni, vedere [Gestione connessione file](../../integration-services/connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>Trasferimento di processi tra istanze di SQL Server  
 L'attività Trasferisci processi supporta un'origine e una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Non esiste alcuna limitazione relativamente alla versione da utilizzare come origine o destinazione.  
  
## <a name="events"></a>Eventi  
 L'attività Trasferisci processi genera un evento informativo in cui è indicato il numero di processi trasferiti. Genera inoltre un evento di avviso quando un processo viene sovrascritto. Non viene riportato lo stato incrementale del trasferimento, ma solo il completamento 0% e 100%.  
  
## <a name="execution-value"></a>Valore di esecuzione  
 Il valore di esecuzione, definito nella proprietà **ExecutionValue** dell'attività, restituisce il numero di processi trasferiti. Tramite l'assegnazione di una variabile definita dall'utente alla proprietà **ExecValueVariable** dell'attività, le informazioni sul trasferimento dei processi possono essere rese disponibili ad altri oggetti del pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Voci di log  
 L'attività Trasferisci processi include le voci di log personalizzate seguenti:  
  
-   TransferJobsTaskStarTransferringObjects   Indica che il trasferimento è iniziato. La voce di log include l'ora di inizio.  
  
-   TransferJobsTaskFinishedTransferringObjects    Indica che il trasferimento è stato completato. La voce di log include l'ora di fine.  
  
 Inoltre, una voce di log per l'evento **OnInformation** indica il numero di processi che sono stati trasferiti. Viene scritta una voce di log per l'evento **OnWarning** per ogni processo sovrascritto nella destinazione.  
  
## <a name="security-and-permissions"></a>Sicurezza e autorizzazioni  
 Per poter trasferire processi, l'utente deve essere un membro del ruolo predefinito del server sysadmin o di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nel database msdb, sia nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di origine che in quella di destinazione.  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>Configurazione dell'attività Trasferisci processi  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Pagina Espressioni](../../integration-services/expressions/expressions-page.md)  
  
 Per informazioni sull'impostazione di queste proprietà a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-jobs-task-editor-general-page"></a>Editor attività Trasferisci processi (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo **Editor attività Trasferisci processi** per assegnare un nome e una descrizione all'attività Trasferisci processi.  
  
> [!NOTE]  
>  Solo i membri del ruolo predefinito del server **sysadmin** o di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nel server di destinazione sono autorizzati alla creazione di processi in tale server. Per accedere ai processi nel server di origine, gli utenti devono essere membri almeno del ruolo predefinito del database **SQLAgentUserRole** nel server di origine. Per altre informazioni sui ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e sulle relative autorizzazioni, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare un nome univoco per l'attività Trasferisci processi. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Trasferisci processi.  
  
## <a name="transfer-jobs-task-editor-jobs-page"></a>Editor attività Trasferisci processi (pagina Processi)
  Utilizzare la pagina **Processi** della finestra di dialogo **Editor attività Trasferisci processi** per specificare le proprietà relative alla copia di uno o più processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent tra due istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Per accedere ai processi nel server di origine, l'utente deve essere un membro almeno del ruolo predefinito del database **SQLAgentUserRole** nel server. Per creare processi nel server di destinazione, l'utente deve essere un membro del ruolo predefinito del server **sysadmin** o di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per altre informazioni sui ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e sulle relative autorizzazioni, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
### <a name="options"></a>Opzioni  
 **SourceConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **\<Nuova connessione...>** per creare una nuova connessione al server di origine.  
  
 **DestinationConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **Nuova connessione...>\<** per creare una nuova connessione al server di destinazione.  
  
 **TransferAllJobs**  
 Indicare se l'attività deve copiare dal server di origine nel server di destinazione tutti i processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent o solo quelli specificati.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**True**|Copia tutti i processi.|  
|**False**|Copia solo i processi specificati.|  
  
 **JobsList**  
 Fare clic sul pulsante con i puntini di sospensione **(...)** per selezionare i processi da copiare. È necessario selezionare almeno un processo.  
  
> [!NOTE]  
>  Prima di selezionare i processi da copiare, specificare la proprietà **SourceConnection** .  
  
 Quando la proprietà **TransferAllJobs** è impostata su **True** , l'opzione **JobsList**non è disponibile.  
  
 **IfObjectExists**  
 Indicare la modalità con cui l'attività deve gestire i processi che hanno lo stesso nome di processi già esistenti nel server di destinazione.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**FailTask**|L'attività viene interrotta se nel server di destinazione esistono processi con lo stesso nome.|  
|**Overwrite**|L'attività sovrascrive i processi con lo stesso nome che si trovano nel server di destinazione.|  
|**Skip**|L'attività ignora i processi con lo stesso nome che si trovano nel server di destinazione.|  
  
 **EnableJobsAtDestination**  
 Specificare se i processi copiati nel server di destinazione devono essere attivati.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**True**|Attiva i processi nel server di destinazione.|  
|**False**|Disabilita i processi nel server di destinazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flusso di controllo](../../integration-services/control-flow/control-flow.md)  
  
  
