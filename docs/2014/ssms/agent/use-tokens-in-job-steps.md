---
title: Usare i token nei passaggi dei processi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server Agent]
- security [SQL Server Agent], enabling alert job step tokens
- SQL Server Agent jobs, job steps
- tokens [SQL Server]
- escape macros [SQL Server Agent]
ms.assetid: 105bbb66-0ade-4b46-b8e4-f849e5fc4d43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2036dd0624e8c2c6479c8ba039aa5646f374902d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211316"
---
# <a name="use-tokens-in-job-steps"></a>Utilizzo dei token nei passaggi dei processi
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent consente di usare token negli script per passaggi di processi [!INCLUDE[tsql](../../includes/tsql-md.md)] . L'utilizzo di token quando si scrivono passaggi di processo offre la stessa flessibilità assicurata dalle variabili quando si scrivono programmi software. Dopo aver inserito un token nello script di un passaggio di processo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sostituisce il token in fase di esecuzione, prima che il passaggio di processo venga eseguito dal sottosistema [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
> [!IMPORTANT]  
>  In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 la sintassi del token dei passaggi del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è stata modificata. Di conseguenza, è necessario inserire una macro di escape con tutti i token utilizzati nei passaggi di processo. In caso contrario, questi passaggi avranno esito negativo. L'utilizzo delle macro di escape e l'aggiornamento dei passaggi di processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che utilizzano token sono illustrati nelle sezioni "Informazioni sull'utilizzo dei token", "Token e macro di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent" e "Aggiornamento dei passaggi di processo per l'utilizzo di macro" riportate di seguito. È inoltre cambiata la sintassi di [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] che prevedeva l'utilizzo delle parentesi quadre per chiamare i token dei passaggi di processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, ad esempio "`[DATE]`". È ora necessario racchiudere tra parentesi i nomi dei token e inserire il simbolo di dollaro (`$`) all'inizio della sintassi del token, Ad esempio:  
>   
>  `$(ESCAPE_` *macro name* `(DATE))`  
  
## <a name="understanding-using-tokens"></a>Informazioni sull'utilizzo dei token  
  
> [!IMPORTANT]  
>  Qualsiasi utente di Windows con autorizzazioni di scrittura per il registro eventi di Windows è in grado di accedere ai passaggi di processo attivati dagli avvisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent o di WMI. Per evitare rischi per la sicurezza, i token di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che possono essere utilizzati in processi attivati dagli avvisi sono disabilitati per impostazione predefinita. Questi token sono: **a-DBN**, **a-SVR**, **a-Err**, **a-SEV**, **a-MSG**. e **WMI (*`property`*)**. Si noti che in questa versione l'utilizzo dei token è esteso a tutti gli avvisi.  
>   
>  Se si desidera utilizzare questi token, verificare innanzitutto che solo i membri di gruppi di sicurezza di Windows trusted, ad esempio il gruppo Administrators, dispongano delle autorizzazioni di scrittura per il registro eventi del computer in cui è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A questo punto, fare clic con il pulsante destro del mouse su **SQL Server Agent** in Esplora oggetti, scegliere **Proprietà**e nella pagina **Sistema avvisi** selezionare **Sostituisci token per tutte le risposte del processo ad avvisi** per abilitare questi token.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent i token vengono sostituiti da valori stringa letterali esatti con un'operazione semplice ed efficiente. Tutti i token effettuano una distinzione tra maiuscole e minuscole. È necessario prendere in considerazione tale comportamento nei passaggi di processo e indicare correttamente i token da utilizzare oppure convertire la stringa di sostituzione nel tipo di dati corretto.  
  
 Ad esempio, è possibile utilizzare l'istruzione seguente per inserire il nome del database in un passaggio di processo:  
  
 `PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
 In questo esempio la macro **ESCAPE_SQUOTE** viene inserita con il token **A-DBN** . In fase di esecuzione il token **A-DBN** verrà sostituito con il nome del database appropriato. Tramite la macro di escape è possibile utilizzare caratteri di escape per eventuali virgolette singole inavvertitamente passate nella stringa di sostituzione del token. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] In Agent una virgoletta singola verrà sostituita con due virgolette singole nella stringa finale.  
  
 Se ad esempio la stringa passata per sostituire il token è `AdventureWorks2012'SELECT @@VERSION --`, il comando eseguito dal passaggio di processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sarà il seguente:  
  
 `PRINT N'Current database name is AdventureWorks2012''SELECT @@VERSION --' ;`  
  
 In questo caso, l'istruzione inserita `SELECT @@VERSION`non verrà eseguita. Al contrario, la virgoletta singola aggiuntiva indurrà il server ad analizzare l'istruzione inserita come stringa. Se la stringa di sostituzione del token non contiene una virgoletta singola, per nessun carattere verranno utilizzati caratteri di escape e il passaggio di processo contenente il token verrà eseguito come previsto.  
  
 Per eseguire il debug dell'utilizzo dei token nei passaggi di processo, utilizzare istruzioni PRINT come `PRINT N'$(ESCAPE_SQUOTE(SQLDIR))'` e salvare l'output del passaggio di processo in un file o in una tabella. Usare la pagina **Avanzate** della finestra di dialogo **Proprietà passaggio processo** per specificare un file o una tabella per l'output del passaggio di processo.  
  
## <a name="sql-server-agent-tokens-and-macros"></a>Token e macro di SQL Server Agent  
 Nelle tabelle seguenti vengono elencati e illustrati i token e le macro supportati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
### <a name="sql-server-agent-tokens"></a>Token di SQL Server Agent  
  
|token|Descrizione|  
|-----------|-----------------|  
|**(A-DBN)**|nome del database. Se il processo viene eseguito da un avviso, il valore del nome del database sostituisce automaticamente il token nel passaggio di processo.|  
|**(A-SVR)**|Nome del server. Se il processo viene eseguito da un avviso, il valore del nome del server sostituisce automaticamente il token nel passaggio di processo.|  
|**(A-ERR)**|Numero di errore. Se il processo viene eseguito da un avviso, il valore del numero di errore sostituisce automaticamente il token nel passaggio di processo.|  
|**(A-SEV)**|Gravità dell'errore. Se il processo viene eseguito da un avviso, il valore della gravità dell'errore sostituisce automaticamente il token nel passaggio di processo.|  
|**(A-MSG)**|Testo del messaggio. Se il processo viene eseguito da un avviso, il valore del testo del messaggio sostituisce automaticamente il token nel passaggio di processo.|  
|**Data**|Data corrente nel formato AAAAMMGG.|  
|**(INST)**|Nome dell'istanza. Il nome di un'istanza predefinita di questo token sarà MSSQLSERVER.|  
|**JobID**|ID del processo.|  
|**(MACH)**|Nome del computer.|  
|**(MSSA)**|Nome del servizio SQLServerAgent master.|  
|**(OSCMD)**|Prefisso per il programma usato per l'esecuzione dei passaggi di processo **CmdExec** .|  
|**(SQLDIR)**|Directory in cui è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per impostazione predefinita corrisponde a C:\Programmi\Microsoft SQL Server\MSSQL.|  
|**(SQLLOGDIR)**|Token di sostituzione per il percorso della cartella del log degli errori di SQL Server, ad esempio $(ESCAPE_SQUOTE(SQLLOGDIR)).|  
|**(STEPCT)**|Numero di esecuzioni del passaggio, escluse le esecuzioni non completate. Può essere utilizzato dal comando del passaggio per imporre l'interruzione di un ciclo a più passaggi.|  
|**(STEPID)**|ID del passaggio.|  
|**(SRVR)**|Nome del computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un'istanza denominata, questo token include il nome dell'istanza.|  
|**TEMPO**|Ora corrente nel formato HHMMSS.|  
|**(STRTTM)**|Ora nel formato HHMMSS in cui è stata avviata l'esecuzione del processo.|  
|**(STRTDT)**|Data nel formato AAAAMMGG in cui è stata avviata l'esecuzione del processo.|  
|**(WMI(** *property* **))**|Per i processi eseguiti in risposta ad avvisi WMI, indica il valore della proprietà specificata da *property*. Ad esempio, `$(WMI(DatabaseName))` specifica il valore della proprietà **DatabaseName** per l'evento WMI che ha provocato l'esecuzione dell'avviso.|  
  
### <a name="sql-server-agent-escape-macros"></a>Macro di escape di SQL Server Agent  
  
|Macro di escape|Descrizione|  
|-------------------|-----------------|  
|**$(ESCAPE_SQUOTE(** *nome_token* **))**|Utilizza caratteri di escape per virgolette singole (') nella stringa di sostituzione del token. Sostituisce una virgoletta singola con due virgolette singole.|  
|**$(ESCAPE_DQUOTE(** *nome_token* **))**|Utilizza caratteri di escape per virgolette doppie (") nella stringa di sostituzione del token. Sostituisce una virgoletta doppia con due virgolette doppie.|  
|**$(ESCAPE_RBRACKET(** *nome_token* **))**|Utilizza caratteri di escape per parentesi chiuse (]) nella stringa di sostituzione del token. Sostituisce una parentesi chiusa con due parentesi chiuse.|  
|**$(ESCAPE_NONE(** *nome_token* **))**|Sostituisce il token senza utilizzare caratteri di escape per i caratteri della stringa. Questa macro viene utilizzata per assicurare la compatibilità con le versioni precedenti in ambienti in cui si presuppone che le stringhe di sostituzione dei token provengano esclusivamente da utenti trusted. Per ulteriori informazioni, vedere "Aggiornamento dei passaggi di processo per l'utilizzo di macro" più avanti in questo argomento.|  
  
## <a name="updating-job-steps-to-use-macros"></a>Aggiornamento dei passaggi di processo per l'utilizzo di macro  
 In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1, i passaggi di processo che contengono token senza macro di escape avranno esito negativo e restituiranno un messaggio di errore in cui è indicato che il passaggio di processo contiene uno o più token che devono essere aggiornati con una macro prima che il processo possa essere eseguito.  
  
 Nell'articolo 915845 della [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base: [I processi di SQL Server Agent che usano token hanno esito negativo in SQL Server 2005 Service Pack 1](https://support.microsoft.com/kb/915845)viene specificato uno script che può essere usato per aggiornare tutti i passaggi di processo che usano token con la macro **ESCAPE_NONE** . Dopo aver usato questo script, è consigliabile esaminare al più presto i passaggi di processo che usano token e sostituire la macro **ESCAPE_NONE** con una macro di escape appropriata per il contesto del passaggio di processo.  
  
 Nella tabella seguente viene indicata la modalità di gestione della sostituzione del token in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agente. Per attivare o disattivare la sostituzione dei token relativi agli avvisi, fare clic con il pulsante destro del mouse su **SQL Server Agent** in Esplora oggetti, scegliere **Proprietà**e selezionare o deselezionare la casella di controllo **Sostituisci token per tutte le risposte del processo ad avvisi** nella pagina **Sistema avvisi** .  
  
|Sintassi dei token|Sostituzione dei token relativi agli avvisi attivata|Sostituzione dei token relativi agli avvisi disattivata|  
|------------------|--------------------------------|---------------------------------|  
|La macro ESCAPE è stata utilizzata|Tutti i token presenti nei processi sono stati sostituiti correttamente.|I token attivati da avvisi non vengono sostituiti. Questi token sono **a-DBN**, **a-SVR**, **a-Err**, **a-SEV**, **a-MSG**e **WMI (*`property`*)**. Altri token statici sono stati sostituiti correttamente.|  
|La macro ESCAPE non è stata utilizzata|Tutti i processi contenenti token hanno esito negativo.|Tutti i processi contenenti token hanno esito negativo.|  
  
## <a name="token-syntax-update-examples"></a>Esempi di aggiornamento della sintassi dei token  
  
### <a name="a-using-tokens-in-non-nested-strings"></a>A. Utilizzo di token in stringhe non nidificate  
 Nell'esempio seguente viene illustrato come aggiornare uno script semplice non nidificato con la macro di escape appropriata. Prima di eseguire lo script di aggiornamento, lo script del passaggio di processo seguente utilizza un token per inserire il nome del database appropriato:  
  
 `PRINT N'Current database name is $(A-DBN)' ;`  
  
 Dopo aver eseguito lo script di aggiornamento, una macro `ESCAPE_NONE` viene inserita prima del token `A-DBN` . Poiché le virgolette singole vengono utilizzate per delimitare la stringa di stampa, è necessario aggiornare il passaggio di processo inserendo la macro `ESCAPE_SQUOTE` nel modo seguente:  
  
 `PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
### <a name="b-using-tokens-in-nested-strings"></a>B. Utilizzo di token in stringhe nidificate  
 Negli script dei passaggi di processo in cui i token vengono utilizzati in istruzioni o stringhe nidificate, è necessario riscrivere le istruzioni nidificate come più istruzioni prima di inserire le macro di escape appropriate.  
  
 Si consideri, ad esempio, il passaggio di processo seguente che non è stato aggiornato con una macro di escape e nel quale viene utilizzato il token `A-MSG` :  
  
 `PRINT N'Print ''$(A-MSG)''' ;`  
  
 Dopo aver eseguito lo script di aggiornamento, una macro `ESCAPE_NONE` viene inserita con il token. In questo caso, tuttavia, è necessario riscrivere lo script senza utilizzare la nidificazione nel modo seguente e inserire la macro `ESCAPE_SQUOTE` per utilizzare correttamente caratteri di escape per i delimitatori che potrebbero essere passati nella stringa di sostituzione del token:  
  
 `DECLARE @msgString nvarchar(max)`  
  
 `SET @msgString = '$(ESCAPE_SQUOTE(A-MSG))'`  
  
 `SET @msgString = QUOTENAME(@msgString,'''')`  
  
 `PRINT N'Print ' + @msgString ;`  
  
 Si noti inoltre che in questo esempio la funzione QUOTENAME imposta il carattere utilizzato per le virgolette.  
  
### <a name="c-using-tokens-with-the-escape_none-macro"></a>C. Utilizzo di token con la macro ESCAPE_NONE  
 L'esempio seguente fa parte di uno script in cui `job_id` viene recuperato dalla tabella `sysjobs` e in cui il token `JOBID` viene utilizzato per popolare la variabile `@JobID` dichiarata in precedenza nello script come tipo di dati binario. Poiché non è necessario alcun delimitatore per i tipi di dati binari, la macro `ESCAPE_NONE` viene utilizzata con il token `JOBID` . Non è necessario aggiornare questo passaggio di processo dopo aver eseguito lo script di aggiornamento.  
  
 `SELECT * FROM msdb.dbo.sysjobs`  
  
 `WHERE @JobID = CONVERT(uniqueidentifier, $(ESCAPE_NONE(JOBID))) ;`  
  
## <a name="see-also"></a>Vedi anche  
 [Implementare processi](implement-jobs.md)   
 [Gestire passaggi di processo](manage-job-steps.md)  
  
  
