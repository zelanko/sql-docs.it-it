---
title: sp_trace_create (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_create_TSQL
- sp_trace_create
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_create
ms.assetid: f3a43597-4c5a-4520-bcab-becdbbf81d2e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7d698932bb7ef7e0fd37a0ced8ab536eeb0d5d68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096035"
---
# <a name="sptracecreate-transact-sql"></a>sp_trace_create (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea la definizione di una nuova traccia nello stato arrestato.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] In alternativa, usare Eventi estesi.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_trace_create [ @traceid = ] trace_id OUTPUT   
          , [ @options = ] option_value   
          , [ @tracefile = ] 'trace_file'   
     [ , [ @maxfilesize = ] max_file_size ]  
     [ , [ @stoptime = ] 'stop_time' ]  
     [ , [ @filecount = ] 'max_rollover_files' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @traceid = ] trace_id` È il numero assegnato dal [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alla nuova traccia. Qualsiasi input dell'utente verrà ignorato. *trace_id* viene **int**, con un valore predefinito è NULL. L'utente usa il *trace_id* valore da identificare, modificare e controllare la traccia definita dalla stored procedure.  
  
`[ @options = ] option_value` Specifica le opzioni impostate per la traccia. *option_value* viene **int**, non prevede alcun valore predefinito. Gli utenti possono impostare una combinazione di queste opzioni specificando la somma dei valori delle opzioni scelte. Ad esempio, per abilitare entrambe le opzioni TRACE_FILE_ROLLOVER e SHUTDOWN_ON_ERROR, specificare **6** per *option_value*.  
  
 Nella tabella seguente sono incluse le opzioni e le descrizioni, accompagnate dai relativi valori.  
  
|Nome opzione|Valore opzione|Descrizione|  
|-----------------|------------------|-----------------|  
|TRACE_FILE_ROLLOVER|**2**|Specifica che quando la *max_file_size* viene raggiunta, corrente file di traccia è chiuso e viene creato un nuovo file. in cui verranno scritti tutti i nuovi record. Il nome del nuovo file è uguale a quello del file precedente, ma è seguito da un numero intero a indicare la sequenza. Se, ad esempio, il nome del file di traccia originale è nomefile.trc, i successivi file di traccia verranno denominati nomefile_1.trc, nomefile_2.trc e così via.<br /><br /> Man mano che vengono creati nuovi file di traccia di rollover, viene incrementato in modo sequenziale il numero aggiunto nel nome del file.<br /><br /> SQL Server Usa il valore predefinito *max_file_size* (5 MB) se questa opzione viene specificata senza specificare un valore per *max_file_size*.|  
|SHUTDOWN_ON_ERROR|**4**|Specifica che se non è possibile scrivere nel file per un qualsiasi motivo, SQL Server viene arrestato. Questa opzione risulta utile quando si eseguono tracce di controllo della sicurezza.|  
|TRACE_PRODUCE_BLACKBOX|**8**|Specifica che il server salverà un record contenente gli ultimi 5 MB di informazioni di traccia generate dal server. TRACE_PRODUCE_BLACKBOX è incompatibile con tutte le altre opzioni.|  
  
`[ @tracefile = ] 'trace_file'` Specifica il percorso e nome del file a cui verrà scritta la traccia. *trace_file* viene **nvarchar(245)** non prevede alcun valore predefinito. *trace_file* può essere una directory locale (ad esempio N 'C:\MSSQL\Trace\trace.trc') o un percorso UNC di una condivisione o un percorso (N'\\\\*Servername*\\*nomecondivisione* \\ *Directory*\trace.trc').  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Aggiunge un **trc** estensione a tutti i nomi di file di traccia. Se l'opzione TRACE_FILE_ROLLOVER e un *max_file_size* vengono specificati, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un nuovo file di traccia quando il file di traccia originale aumenta le dimensioni massime. Il nuovo file con lo stesso nome di file originale, ma _*n* viene aggiunto per indicare la sequenza, a partire **1**. Ad esempio, se il primo file di traccia è denominato **nomefile. trc**, il secondo file di traccia è denominato **nomefile_1.trc**.  
  
 Se si utilizza l'opzione TRACE_FILE_ROLLOVER, si consiglia di non utilizzare caratteri di sottolineatura nel nome del file di traccia originale. Se vengono utilizzati caratteri di sottolineatura, si verifica il comportamento seguente:  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] non carica automaticamente o richiedere agli utenti di caricare i file di rollover (se una di queste opzioni di rollover dei file sono configurata).  
  
-   La funzione fn_trace_gettable non carica i file di rollover (quando specificata utilizzando il *number_files* argomento) in cui il nome file originale termina con un carattere di sottolineatura e un valore numerico. Ciò non vale per il carattere di sottolineatura e il numero che vengono aggiunti automaticamente all'esecuzione del rollover di un file.  
  
> [!NOTE]  
>  Come soluzione alternativa a entrambi questi comportamenti, è possibile rinominare i file in modo da rimuovere i caratteri di sottolineatura nel nome del file originale. Ad esempio, se il file originale è denominato **my_trace. trc**, e il file di rollover è denominato **my_trace_1.trc**, è possibile rinominare i file da **mytrace. trc** e**mytrace_1.trc** prima di aprire i file in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 *trace_file* non può essere specificato quando si usa l'opzione TRACE_PRODUCE_BLACKBOX.  
  
`[ @maxfilesize = ] max_file_size` Specifica che le dimensioni massime in megabyte (MB) un file di traccia possono raggiungere. *valore di max_file_size* viene **bigint**, con valore predefinito è **5**.  
  
 Se questo parametro viene specificato senza l'opzione TRACE_FILE_ROLLOVER, la traccia viene arrestata la registrazione al file quando lo spazio su disco utilizzato supera la quantità specificata da *max_file_size*.  
  
`[ @stoptime = ] 'stop_time'` Specifica la data e ora che la traccia verrà arrestata. *stop_time* viene **datetime**, con un valore predefinito è NULL. Se il valore è NULL, la traccia viene eseguita fino a quando non viene arrestata in modo manuale o fino all'arresto del server.  
  
 Se entrambe *stop_time* e *max_file_size* vengono specificati, e TRACE_FILE_ROLLOVER, non è specificato, la traccia alto quando viene raggiunta l'ora di arresto specificata o dimensioni massime del file. Se *stop_time*, *max_file_size*e vengono specificati TRACE_FILE_ROLLOVER, la traccia viene arrestata all'ora specificata, presupponendo che la traccia non è riempire l'unità.  
  
`[ @filecount = ] 'max_rollover_files'` Specifica il massimo numero di file di traccia da mantenere con lo stesso nome di file di base. *MAX_ROLLOVER_FILES* viene **int**, maggiore di uno. Questo parametro è valido solo se è specificata l'opzione TRACE_FILE_ROLLOVER. Quando *max_rollover_files* è specificato, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prova a mantenere no oltre *max_rollover_files* eliminando il file di traccia meno recente prima di aprire un nuovo file di traccia. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene tenuto traccia dell'età dei file di traccia aggiungendo un numero al nome del file di base.  
  
 Ad esempio, quando la *trace_file* parametro viene specificato come "c:\mytrace", un file con il nome "c:\mytrace_123.trc" è meno di un file con il nome "c:\mytrace_124.trc". Se *max_rollover_files* è impostato su 2, SQL Server eliminerà il file "c:\mytrace_123.trc" prima di creare il file di traccia "c:\mytrace_125.trc".  
  
 Si noti che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta di eliminare un file una sola volta e non può eliminare un file se questo è utilizzato da un altro processo. Se, pertanto, un'altra applicazione sta utilizzando i file di traccia mentre è in esecuzione la traccia, è possibile che tali file vengano lasciati nel file system da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valori restituiti  
 Nella tabella seguente vengono descritti i possibili valori di codice visualizzati al completamento della stored procedure.  
  
|Codice restituito|Descrizione|  
|-----------------|-----------------|  
|0|Nessun errore.|  
|1|Errore sconosciuto.|  
|10|Opzioni non valide. Restituito quando le opzioni specificate sono incompatibili.|  
|12|Creazione del file non riuscita.|  
|13|Memoria esaurita. Restituito quando la quantità di memoria disponibile non è sufficiente per eseguire l'azione specificata.|  
|14|Ora di arresto non valida. Restituito quando l'ora specificata è già trascorsa.|  
|15|Parametri non validi. Restituito quando l'utente specifica parametri incompatibili.|  
  
## <a name="remarks"></a>Note  
 **sp_trace_create** è un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stored procedure che esegue molte delle azioni eseguite dalle **xp_trace _\***  disponibili nelle versioni precedenti di SQL Server stored procedure estese. Uso **sp_trace_create** invece di:  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_setqueuecreateinfo**  
  
-   **xp_trace_setqueuedestination**  
  
 **sp_trace_create** crea solo una definizione di traccia. non per avviare o modificare una traccia.  
  
 I parametri di traccia SQL tutte le stored procedure (**sp_trace_xx**) sono fortemente tipizzati. Se questi parametri non vengono chiamati con i tipi di dati corretti per i parametri di input, come indicato nella descrizione dell'argomento, la stored procedure restituirà un errore.  
  
 Per la **sp_trace_create**, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account del servizio deve avere l'autorizzazione di scrittura per la cartella di file di traccia. Se l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è un amministratore nel computer in cui si trova il file di traccia, è necessario concedere esplicitamente l'autorizzazione di scrittura all'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  È possibile caricare automaticamente il file di traccia creato con **sp_trace_create** in una tabella tramite il **fn_trace_gettable** funzione di sistema. Per informazioni su come usare questa funzione di sistema, vedere [sys.fn_trace_gettable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md).  
  
 Per un esempio dell'uso di stored procedure relative alla traccia, vedere [Creare una traccia &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
 **TRACE_PRODUCE_BLACKBOX** presenta le caratteristiche seguenti:  
  
-   È costituito da una traccia di rollover. Il valore predefinito *conteggio_file* è 2, ma può essere sottoposto a override dall'utente utilizzando *filecount* opzione.  
  
-   Il valore predefinito *file_size* Analogamente alle altre tracce è 5 MB e può essere modificato.  
  
-   Non è possibile specificare alcun nome di file. Il file verrà salvato come: **N'%SQLDIR%\MSSQL\DATA\blackbox.trc'**  
  
-   Nella traccia saranno contenuti solo gli eventi seguenti e le relative colonne:  
  
    -   **Avvio RPC**  
  
    -   **Avvio batch**  
  
    -   **Eccezione**  
  
    -   **Attenzione**  
  
-   Non è possibile aggiungere o rimuovere eventi o colonne da questa traccia.  
  
-   Non è possibile specificare i filtri per questa traccia.  
  
## <a name="permissions"></a>Permissions  
 L'utente deve disporre delle autorizzazioni ALTER TRACE.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Traccia SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
