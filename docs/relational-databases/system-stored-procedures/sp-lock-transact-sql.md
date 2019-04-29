---
title: sp_lock (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_lock_TSQL
- sp_lock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_lock
ms.assetid: 9eaa0ec2-2ad9-457c-ae48-8da92a03dcb0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8d917f71d7cf7a36bb5d2c50b0cddd7893102a7e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62960085"
---
# <a name="splock-transact-sql"></a>sp_lock (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza informazioni relative ai blocchi.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Per ottenere informazioni sui blocchi nel [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], usare il [DM tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md) vista a gestione dinamica.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_lock [ [ @spid1 = ] 'session ID1' ] [ , [@spid2 = ] 'session ID2' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @spid1 = ] 'session ID1'` È un [!INCLUDE[ssDE](../../includes/ssde-md.md)] numero di ID di sessione **Sys. dm _** per il quale si desidera ottenere informazioni sui blocchi. *sessione ID1* viene **int** con un valore predefinito NULL. Eseguire **sp_who** per ottenere informazioni relative alla sessione. Se *sessione ID1* non viene specificato, vengono visualizzate informazioni su tutti i blocchi.  
  
`[ @spid2 = ] 'session ID2'` Un'altra [!INCLUDE[ssDE](../../includes/ssde-md.md)] numero di ID di sessione **Sys. dm _** che potrebbero essere bloccati nello stesso momento come *sessione ID1* e che l'utente desidera ottenere informazioni. *sessione ID2* viene **int** con un valore predefinito NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 Il **sp_lock** set di risultati contiene una riga per ogni blocco mantenuto attivo dalle sessioni specificate nel **@spid1** e **@spid2** parametri. Se nessuno di essi **@spid1** né **@spid2** è specificato, il set di risultati i blocchi per tutte le sessioni attualmente attiva nell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**spid**|**smallint**|Numero di ID di sessione di [!INCLUDE[ssDE](../../includes/ssde-md.md)] per il processo che richiede il blocco.|  
|**dbid**|**smallint**|Numero di identificazione del database in cui il blocco è attivato. Per identificare il database, è possibile utilizzare la funzione DB_NAME().|  
|**ObjId**|**int**|Numero di identificazione dell'oggetto per cui il blocco è attivato. Per identificare l'oggetto, è possibile utilizzare la funzione OBJECT_NAME() nel database correlato. Il valore 99 rappresenta un caso speciale e indica un blocco su una delle pagine di sistema utilizzate per registrare l'allocazione delle pagine di un database.|  
|**IndId**|**smallint**|Numero di identificazione dell'indice per cui il blocco è mantenuto attivo.|  
|**Tipo**|**nchar(4)**|Tipo di blocco:<br /><br /> RID = Blocco su una sola riga di una tabella identificata da un identificatore di riga (RID).<br /><br /> KEY = Blocco all'interno di un indice che protegge un intervallo di chiavi in transazioni serializzabili.<br /><br /> PAG = Blocco su una pagina di dati o di indice.<br /><br /> EXT = Blocco su un extent.<br /><br /> TAB = Blocco su un'intera tabella, inclusi tutti i dati e gli indici.<br /><br /> DB = Blocco su un database.<br /><br /> FIL = Blocco su un file di database.<br /><br /> APP = Blocco su una risorsa specifica di un'applicazione.<br /><br /> MD = Blocco su metadati o informazioni del catalogo.<br /><br /> HBT = Blocco su un heap o un indice albero B. Queste informazioni non sono complete in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> AU = Blocco su un'unità di allocazione. Queste informazioni non sono complete in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Risorsa**|**nchar(32)**|Valore che identifica la risorsa bloccata. Il formato del valore dipende dal tipo di risorsa identificato nella **tipo** colonna:<br /><br /> **Tipo** valore: **Risorsa** valore<br /><br /> RID: Un identificatore nel formato IDfile: numeropagina: rid, dove IDfile identifica il file contenente la pagina, numeropagina identifica la pagina contenente la riga e rid identifica la riga specifica nella pagina. fileid corrisponde la **file_id** colonna il **Sys. database_files** vista del catalogo.<br /><br /> CHIAVE: Un numero esadecimale utilizzato internamente dal [!INCLUDE[ssDE](../../includes/ssde-md.md)].<br /><br /> PAG: Numero di formato IDfile: numeropagina, dove IDfile identifica il file contenente la pagina e numeropagina identifica la pagina.<br /><br /> EXT: Numero che identifica la prima pagina nell'extent. Il numero è nel formato idfile:numeropagina.<br /><br /> TAB: Non vengono fornite informazioni perché la tabella è già identificata nella **ObjId** colonna.<br /><br /> DB: Non vengono fornite informazioni perché il database è già identificato nella **dbid** colonna.<br /><br /> FIL: L'identificatore del file, che corrisponde il **file_id** colonna il **Sys. database_files** vista del catalogo.<br /><br /> APP: Identificatore univoco per la risorsa di applicazione bloccata. Nel formato DbPrincipleId:\<primi due a 16 caratteri della stringa di risorsa >\<valore hash >.<br /><br /> MD: varia in base al tipo di risorsa. Per altre informazioni, vedere la descrizione del **resource_description** colonna nelle [DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).<br /><br /> HBT: Non vengono fornite informazioni. Usare la **DM tran_locks** invece la vista a gestione dinamica.<br /><br /> AU: Non vengono fornite informazioni. Usare la **DM tran_locks** invece la vista a gestione dinamica.|  
|**Mode**|**nvarchar(8)**|Modalità di blocco richiesta. I possibili valori sono i seguenti:<br /><br /> NULL = Non è concesso l'accesso alla risorsa. Funge da segnaposto.<br /><br /> Sch-S = Stabilità dello schema. Impedisce che un elemento dello schema, ad esempio una tabella o un indice, venga eliminato mentre in una sessione viene mantenuto attivo un blocco di stabilità dello schema su tale elemento.<br /><br /> Sch-M = Modifica dello schema. Deve essere impostato in tutte le sessioni in cui si desidera modificare lo schema della risorsa specificata. Assicura che nessun'altra sessione faccia riferimento all'oggetto specificato.<br /><br /> S = Condiviso. La sessione attiva dispone dell'accesso condiviso alla risorsa.<br /><br /> U = Aggiornamento. Indica un blocco di aggiornamento acquisito su risorse che potrebbero essere aggiornate. Viene utilizzato per evitare una forma comune di deadlock che si verifica quando in più sessioni vengono bloccate risorse che potrebbero essere aggiornate in un momento successivo.<br /><br /> X = Esclusivo. La sessione attiva dispone dell'accesso esclusivo alla risorsa.<br /><br /> IS = Preventivo condiviso. Indica l'intenzione di impostare blocchi condivisi (S) su alcune risorse subordinate nella gerarchia dei blocchi.<br /><br /> IU = Preventivo aggiornamento. Indica l'intenzione di impostare blocchi di aggiornamento (U) su alcune risorse subordinate nella gerarchia dei blocchi.<br /><br /> IX = Preventivo esclusivo. Indica l'intenzione di impostare blocchi esclusivi (X) su alcune risorse subordinate nella gerarchia dei blocchi.<br /><br /> SIU = Condiviso preventivo aggiornamento. Indica l'accesso condiviso a una risorsa con l'intenzione di acquisire blocchi di aggiornamento su risorse subordinate nella gerarchia dei blocchi.<br /><br /> SIX = Condiviso preventivo esclusivo. Indica l'accesso condiviso a una risorsa con l'intenzione di acquisire blocchi esclusivi su risorse subordinate nella gerarchia dei blocchi.<br /><br /> UIX = Aggiornamento preventivo esclusivo. Indica un blocco di aggiornamento attivato su una risorsa con l'intenzione di acquisire blocchi esclusivi su risorse subordinate nella gerarchia dei blocchi.<br /><br /> BU = Aggiornamento bulk. Utilizzato dalle operazioni bulk.<br /><br /> RangeS_S = Blocco condiviso intervalli di chiavi e risorsa. Indica un'analisi di intervallo serializzabile.<br /><br /> RangeS_U = Blocco condiviso intervalli di chiavi e aggiornamento risorsa. Indica un'analisi di aggiornamento serializzabile.<br /><br /> RangeI_N = Blocco inserimento intervalli di chiavi e risorsa Null. Utilizzato per verificare gli intervalli prima di inserire una nuova chiave in un indice.<br /><br /> RangeI_S = Blocco conversione intervalli di chiavi. Creato da una sovrapposizione dei blocchi RangeI_N e S.<br /><br /> RangeI_U = Blocco conversione intervallo di chiavi creato da una sovrapposizione di blocchi RangeI_N e U.<br /><br /> RangeI_X = Blocco conversione intervallo di chiavi creato da una sovrapposizione di blocchi RangeI_N e X.<br /><br /> RangeX_S = Blocco conversione intervallo di chiavi creato da una sovrapposizione di blocchi RangeI_N e RangeS_S.<br /><br /> RangeX_U = Blocco conversione intervallo di chiavi creato da una sovrapposizione di blocchi RangeI_N e RangeS_U.<br /><br /> RangeX_X = Blocco esclusivo intervalli di chiavi e risorsa. Si tratta di un blocco di conversione utilizzato quando viene aggiornata una chiave in un intervallo.|  
|**Stato**|**nvarchar(5)**|Stato della richiesta di blocco:<br /><br /> CNVRT: Il blocco viene convertito da un'altra modalità, ma la conversione è bloccata da un altro processo che mantiene attivo un blocco con una modalità in conflitto.<br /><br /> GRANT: Il blocco è stato ottenuto.<br /><br /> WAIT: Il blocco è bloccato da un altro processo che mantiene attivo un blocco con una modalità in conflitto.|  
  
## <a name="remarks"></a>Note  
 Gli utenti possono controllare il blocco delle operazioni di lettura mediante:  
  
-   L'utilizzo di SET TRANSACTION ISOLATION LEVEL per specificare il livello di blocco per una sessione. Per la sintassi e le restrizioni, vedere [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
-   L'utilizzo di hint di tabella di blocco per specificare il livello di blocco per un singolo riferimento di una tabella in una clausola FROM. Per la sintassi e le restrizioni, vedere [hint per la tabella &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Tutte le transazioni distribuite non associate a una sessione sono transazioni orfane. In [!INCLUDE[ssDE](../../includes/ssde-md.md)] a tutte le transazioni distribuite orfane viene assegnato il valore SPID -2, in modo da semplificare l'identificazione delle transazioni distribuite che causano un blocco. Per altre informazioni, vedere [Usare transazioni contrassegnate per recuperare coerentemente i database correlati &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-all-locks"></a>A. Elenco di tutti i blocchi  
 Nell'esempio seguente vengono visualizzate informazioni su tutti i blocchi attualmente mantenuti attivi in un'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
```  
USE master;  
GO  
EXEC sp_lock;  
GO  
```  
  
### <a name="b-listing-a-lock-from-a-single-server-process"></a>B. Visualizzazione di un blocco di un processo a server singolo  
 Nell'esempio seguente vengono visualizzate informazioni sull'ID di processo `53`, inclusi i blocchi.  
  
```  
USE master;  
GO  
EXEC sp_lock 53;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.dm_os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)  
  
  
