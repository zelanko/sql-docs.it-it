---
title: Attività Trasferisci stored procedure master | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfermasterspstask.f1
- sql13.dts.designer.transferstoredprocedurestask.general.f1
- sql13.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cee2dfed374c3f479e32b8d81602eff924287356
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71293854"
---
# <a name="transfer-master-stored-procedures-task"></a>Attività Trasferisci stored procedure master

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  L'attività Trasferisci stored procedure master trasferisce una o più stored procedure definite dall'utente tra i database **master** di istanze diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per trasferire una stored procedure dal database **master** , è necessario che il proprietario stored della procedure sia un dbo.  
  
 È possibile configurare l'attività Trasferisci stored procedure master per il trasferimento di tutte le stored procedure o delle stored procedure specificate. Questa attività non esegue la copia delle stored procedure di sistema.  
  
 È possibile che le stored procedure master da trasferire siano già presenti nella destinazione. È tuttavia possibile configurare l'attività Trasferisci stored procedure master per la gestione di eventuali stored procedure esistenti nei modi seguenti:  
  
-   Le stored procedure esistenti vengono sovrascritte.  
  
-   In presenza di stored procedure duplicate l'attività ha esito positivo.  
  
-   Le stored procedure duplicate vengono ignorate.  
  
 In fase di esecuzione l'attività Trasferisci stored procedure master si connette al server di origine e al server di destinazione utilizzando due gestioni connessioni SMO. Le gestioni connessioni SMO vengono configurate separatamente dall'attività Trasferisci stored procedure master, che tuttavia vi fa riferimento. Le gestioni connessioni SMO specificano il server e la modalità di autenticazione da utilizzare per l'accesso al server. Per altre informazioni, vedere [Gestione connessione file](../../integration-services/connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-stored-procedures-between-instances-of-sql-server"></a>Trasferimento di stored procedure tra istanze di SQL Server  
 L'attività Trasferisci stored procedure master supporta un'origine e una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventi  
 L'attività genera un evento informativo in cui è indicato il numero di stored procedure trasferite. Genera inoltre un evento di avviso quando una stored procedure viene sovrascritta.  
  
 Non viene riportato lo stato incrementale del trasferimento, ma solo il completamento 0% e 100%.  
  
## <a name="execution-value"></a>Valore di esecuzione  
 Il valore di esecuzione, definito nella proprietà **ExecutionValue** dell'attività, restituisce il numero di stored procedure trasferite. Tramite l'assegnazione di una variabile definita dall'utente alla proprietà **ExecValueVariable** dell'attività, le informazioni sul trasferimento di stored procedure master possono essere rese disponibili ad altri oggetti del pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Voci di log  
 L'attività Trasferisci stored procedure master include le voci di log personalizzate seguenti:  
  
-   TransferStoredProceduresTaskStartTransferringObjects  Indica che il trasferimento è iniziato. La voce di log include l'ora di inizio.  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  Indica che il trasferimento è stato completato. La voce di log include l'ora di fine.  
  
 Inoltre, una voce di log per l'evento **OnInformation** indica il numero di stored procedure che sono state trasferite e viene scritta una voce di log per l'evento **OnWarning** per ogni stored procedure sovrascritta nella destinazione.  
  
## <a name="security-and-permissions"></a>Sicurezza e autorizzazioni  
 L'utente deve disporre dell'autorizzazione per la visualizzazione dell'elenco di stored procedure nel database **master** dell'origine ed essere un membro del ruolo del server amministratore di sistema o disporre dell'autorizzazione per la creazione di stored procedure nel database **master** del server di destinazione.  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>Configurazione dell'attività Trasferisci stored procedure master  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Pagina Espressioni](../../integration-services/expressions/expressions-page.md)  
  
 Per informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>Configurazione dell'attività Trasferisci stored procedure master a livello di codice  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-master-stored-procedures-task-editor-general-page"></a>Editor attività Trasferisci stored procedure master (pagina Generale)
  Usare la pagina **Generale** della finestra di dialogo **Editor attività Trasferisci stored procedure master** per assegnare un nome e una descrizione all'attività Trasferisci stored procedure master.  
  
> [!NOTE]  
>  L'attività consente solo il trasferimento di stored procedure appartenenti a **dbo** da un database **master** del server di origine a un database **master** del server di destinazione. Per poter creare stored procedure nel server di destinazione, gli utenti devono disporre dell'autorizzazione CREATE PROCEDURE nel database **master** del server di destinazione o essere membri del ruolo predefinito del server **sysadmin** nel server di destinazione.  
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare un nome univoco per l'attività Trasferisci stored procedure master. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Trasferisci stored procedure master.  
  
## <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>Editor attività Trasferisci stored procedure master (pagina Stored procedure)
  Usare la pagina **Stored procedure** della finestra di dialogo **Editor attività Trasferisci stored procedure master** per specificare le proprietà per la copia di una o più stored procedure definite dall'utente dal database **master** di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un database **master** di un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  L'attività consente solo il trasferimento di stored procedure appartenenti a **dbo** da un database **master** del server di origine a un database **master** del server di destinazione. Per poter creare stored procedure nel server di destinazione, gli utenti devono disporre dell'autorizzazione CREATE PROCEDURE nel database **master** del server di destinazione o essere membri del ruolo predefinito del server **sysadmin** nel server di destinazione.  
  
### <a name="options"></a>Opzioni  
 **SourceConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **\<Nuova connessione...>** per creare una nuova connessione al server di origine.  
  
 **DestinationConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **Nuova connessione...>\<** per creare una nuova connessione al server di destinazione.  
  
 **IfObjectExists**  
 Selezionare la modalità con cui l'attività deve gestire le stored procedure definite dall'utente che hanno lo stesso nome di stored procedure già esistenti nel database **master** del server di destinazione.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**FailTask**|L'attività viene interrotta se nel database **master** del server di destinazione esistono già stored procedure con lo stesso nome.|  
|**Overwrite**|L'attività sovrascrive le stored procedure con lo stesso nome presenti nel database **master** del server di destinazione.|  
|**Skip**|L'attività ignora le stored procedure con lo stesso nome presenti nel database **master** del server di destinazione.|  
  
 **TransferAllStoredProcedures**  
 Selezionare un valore per indicare se nel server di destinazione debbano essere copiate tutte le stored procedure definite dall'utente nel database **master** del server di origine.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**True**|Copia tutte le stored procedure definite dall'utente nel database **master** .|  
|**False**|Copia solo le stored procedure specificate.|  
  
 **StoredProceduresList**  
 Selezionare le stored procedure definite dall'utente nel database **master** del server di origine da copiare nel database **master** del server di destinazione. Questa opzione è disponibile solo quando la proprietà **TransferAllStoredProcedures** è impostata su **False**.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Trasferisci oggetti di SQL Server](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Attività di Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flusso di controllo](../../integration-services/control-flow/control-flow.md)  
  
  
