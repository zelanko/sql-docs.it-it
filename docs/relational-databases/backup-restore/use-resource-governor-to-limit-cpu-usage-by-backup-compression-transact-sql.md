---
title: 'Limitare il carico della CPU: usare Resource Governor per la compressione dei backup'
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup compression [SQL Server], Resource Governor
- backup compression [SQL Server], CPU usage
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- Resource Governor, backup compression
ms.assetid: 01796551-578d-4425-9b9e-d87210f7ba72
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 73fd6d47d3108fbfc46e1d1a6189ac21892a3eb9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "75245407"
---
# <a name="use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql"></a>Utilizzo di Resource Governor per limitare l'utilizzo della CPU da parte della compressione dei backup (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Per impostazione predefinita, l'esecuzione di backup mediante la compressione aumenta in modo significativo l'utilizzo della CPU e la CPU aggiuntiva utilizzata dal processo di compressione può avere un impatto negativo sulle operazioni simultanee. È necessario quindi creare un backup compresso con priorità bassa in una sessione con utilizzo della CPU limitato da[Resource Governor](../../relational-databases/resource-governor/resource-governor.md) nel caso in cui si verifichi una contesa di CPU. In questo argomento viene presentato uno scenario che classifica le sessioni di un particolare utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguendone mapping a un gruppo del carico di lavoro di Resource Governor che limita l'utilizzo della CPU in tali casi.  
  
> [!IMPORTANT]  
>  In uno scenario di Resource Governor specifico la classificazione della sessione potrebbe essere basata su un nome utente, un nome di applicazione o qualsiasi altro elemento in grado di differenziare una connessione. Per ulteriori informazioni, vedere [Resource Governor Classifier Function](../../relational-databases/resource-governor/resource-governor-classifier-function.md) e [Resource Governor Workload Group](../../relational-databases/resource-governor/resource-governor-workload-group.md).  
  
##  <a name="this-topic-contains-the-following-set-of-scenarios-which-are-presented-in-sequence"></a><a name="Top"></a> In questo argomento è contenuto il set seguente di scenari, che vengono presentati in sequenza:  
  
1.  [Impostazione di un account di accesso e di un utente per operazioni con priorità bassa](#setup_login_and_user)  
  
2.  [Configurazione di Resource Governor per limitare l'utilizzo di CPU](#configure_RG)  
  
3.  [Verifica della classificazione della sessione corrente (Transact-SQL)](#verifying)  
  
4.  [Compressione di backup utilizzando una sessione con utilizzo della CPU limitato](#creating_compressed_backup)  
  
##  <a name="setting-up-a-login-and-user-for-low-priority-operations"></a><a name="setup_login_and_user"></a> Impostazione di un account di accesso e di un utente per operazioni con priorità bassa  
 Per lo scenario presentato in questo argomento sono necessari un account di accesso e un utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con priorità bassa. Il nome utente verrà utilizzato per classificare sessioni in esecuzione con l'account di accesso e per indirizzarle a un gruppo del carico di lavoro di Resource Governor che limita l'utilizzo della CPU.  
  
 Nella procedura seguente vengono descritte le operazioni necessarie per impostare un account di accesso e un utente. Viene quindi illustrato l'esempio [!INCLUDE[tsql](../../includes/tsql-md.md)] "Esempio A: Impostazione di un account di accesso e di un utente (Transact-SQL)".  
  
### <a name="to-set-up-a-login-and-database-user-for-classifying-sessions"></a>Per impostare un account di accesso e un utente del database per classificare sessioni  
  
1.  Definire un account di accesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la creazione di backup compressi con priorità bassa.  
  
     **Per creare un account di accesso**  
  
    -   [Creare un account di accesso](../../relational-databases/security/authentication-access/create-a-login.md)  
  
    -   [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
2.  Facoltativamente, concedere l'autorizzazione VIEW SERVER STATE a tale account di accesso.  
  
    -   [GRANT - autorizzazioni per oggetti di sistema &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)  
  
     Per altre informazioni, vedere [GRANT - autorizzazioni per entità di database &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md).  
  
3.  Creare un utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per tale account di accesso.  
  
     **Per creare un utente**  
  
    -   [Creazione di un utente di database](../../relational-databases/security/authentication-access/create-a-database-user.md)  
  
    -   [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
4.  Per consentire alle sessioni relative agli account di accesso e all'utente creati di eseguire il backup di un database specifico, aggiungere l'utente al ruolo db_backupoperator del database. Effettuare questa operazione per ogni database di cui l'utente eseguirà il backup. Facoltativamente, aggiungere l'utente agli altri ruoli predefiniti del database.  
  
     **Per aggiungere un utente a un ruolo predefinito del database**  
  
    -   [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
     Per altre informazioni, vedere [GRANT - autorizzazioni per entità di database &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md).  
  
### <a name="example-a-setting-up-a-login-and-user-transact-sql"></a>Esempio A: Impostazione di un account di accesso e di un utente (Transact-SQL)  
 L'esempio seguente è rilevante solo se si sceglie di creare un nuovo account di accesso e un nuovo utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire backup con priorità bassa. In alternativa, è possibile utilizzare un account di accesso e un utente esistenti, se appropriati.  
  
> [!IMPORTANT]  
>  L'esempio seguente usa un accesso e un nome utente di esempio, *domain_name*`\MAX_CPU`. Sostituire questi nomi con quelli dell'account di accesso e dell'utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che si intende utilizzare nella creazione dei backup compressi con priorità bassa.  
  
 Questo esempio crea un accesso per l'account di Windows *domain_name*`\MAX_CPU` e concede l'autorizzazione VIEW SERVER STATE all'accesso. che consente di verificare la classificazione di Resource Governor delle sessioni dell'account di accesso. L'esempio crea quindi un utente per *domain_name*`\MAX_CPU` e lo aggiunge al ruolo predefinito del database db_backupoperator per il database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . Tale nome utente verrà utilizzato dalla funzione di classificazione di Resource Governor.  
  
```sql  
-- Create a SQL Server login for low-priority operations  
USE master;  
CREATE LOGIN [domain_name\MAX_CPU] FROM WINDOWS;  
GRANT VIEW SERVER STATE TO [domain_name\MAX_CPU];  
GO  
-- Create a SQL Server user in AdventureWorks2012 for this login  
USE AdventureWorks2012;  
CREATE USER [domain_name\MAX_CPU] FOR LOGIN [domain_name\MAX_CPU];  
EXEC sp_addrolemember 'db_backupoperator', 'domain_name\MAX_CPU';  
GO  
  
```  
  
 [&#91;Torna all'inizio&#93;](#Top)  
  
##  <a name="configuring-resource-governor-to-limit-cpu-usage"></a><a name="configure_RG"></a> Configurazione di Resource Governor per limitare l'utilizzo di CPU  
  
> [!NOTE]  
>  Verificare che Resource Governor sia abilitato. Per altre informazioni, vedere [Abilitare Resource Governor](../../relational-databases/resource-governor/enable-resource-governor.md).  
  
 In questo scenario di Resource Governor la configurazione include i passaggi di base seguenti:  
  
1.  Creazione e configurazione di un pool di risorse di Resource Governor che limita il valore massimo della larghezza di banda media della CPU assegnata alle richieste nel pool di risorse quando si verifica una contesa di CPU.  
  
2.  Creazione e configurazione di un gruppo del carico di lavoro di Resource Governor che utilizza tale pool.  
  
3.  Creazione di una *funzione di classificazione*, ovvero di una funzione definita dall'utente i cui valori restituiti vengono usati da Resource Governor per classificare le sessioni in modo da indirizzarle al gruppo di carico di lavoro appropriato.  
  
4.  Registrazione della funzione di classificazione con Resource Governor.  
  
5.  Applicazione delle modifiche alla configurazione in memoria di Resource Governor.  
  
> [!NOTE]  
>  Per informazioni sui pool di risorse, i gruppi di carico di lavoro e la classificazione di Resource Governor, vedere [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
 Le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] per questi passaggi vengono descritte nella procedura "Per configurare Resource Governor per limitare l'utilizzo della CPU", al termine della quale viene illustrato un esempio [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 **Per configurare Resource Governor (SQL Server Management Studio)**  
  
-   [Configurare Resource Governor usando un modello](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)  
  
-   [Creare un pool di risorse](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
-   [Creare un gruppo di carico di lavoro](../../relational-databases/resource-governor/create-a-workload-group.md)  
  
### <a name="to-configure-resource-governor-for-limiting-cpu-usage-transact-sql"></a>Per configurare Resource Governor per limitare l'utilizzo della CPU (Transact-SQL)  
  
1.  Eseguire un'istruzione [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md) per creare un pool di risorse. Nell'esempio relativo a questa procedura viene utilizzata la sintassi seguente:  
  
     *CREATE RESOURCE POOL nome_pool* WITH ( MAX_CPU_PERCENT = *valore* );  
  
     *Value* è un integer compreso tra 1 e 100 che indica la percentuale del valore massimo della larghezza di banda media della CPU. Il valore appropriato dipende dall'ambiente. A scopo illustrativo, nell'esempio in questo argomento viene utilizzato il valore 20% (MAX_CPU_PERCENT = 20).  
  
2.  Eseguire un'istruzione [CREATE WORKLOAD GROUP](../../t-sql/statements/create-workload-group-transact-sql.md) per creare un gruppo di carico di lavoro per le operazioni con priorità bassa per cui si vuole controllare l'utilizzo della CPU. Nell'esempio relativo a questa procedura viene utilizzata la sintassi seguente:  
  
     CREATE WORKLOAD GROUP *nome_gruppo* USING *nome_pool*;  
  
3.  Eseguire un'istruzione [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) per creare una funzione di classificazione che esegue il mapping del gruppo di carico di lavoro creato nel passaggio precedente all'utente relativo all'account di accesso con priorità bassa. Nell'esempio relativo a questa procedura viene utilizzata la sintassi seguente:  
  
     CREATE FUNCTION [*nome_schema*.]*nome_funzione*() RETURNS sysname  
  
     WITH SCHEMABINDING  
  
     AS  
  
     BEGIN  
  
     DECLARE @workload_group_name AS *sysname*  
  
     IF (SUSER_NAME() = '*utente_accesso_bassa_priorità*')  
  
     SET @workload_group_name = '*nome_gruppo_carico_di_lavoro*'  
  
     RETURN @workload_group_name  
  
     END  
  
     Per informazioni sui componenti di questa istruzione CREATE FUNCTION, vedere i seguenti argomenti:  
  
    -   [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
    -   [SUSER_SNAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md)  
  
        > [!IMPORTANT]  
        >  SUSER_NAME è solo una delle numerose funzioni di sistema che possono essere utilizzate in una funzione di classificazione. Per altre informazioni, vedere [Creare e testare una funzione di classificazione definita dall'utente](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md).  
  
    -   [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md).  
  
4.  Eseguire un'istruzione [ALTER RESOURCE GOVERNOR](../../t-sql/statements/alter-resource-governor-transact-sql.md) per registrare la funzione di classificazione con Resource Governor. Nell'esempio relativo a questa procedura viene utilizzata la sintassi seguente:  
  
     ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = *nome_schema*.*nome_funzione*);  
  
5.  Eseguire una seconda istruzione ALTER RESOURCE GOVERNOR per applicare le modifiche alla configurazione in memoria di Resource Governor, come descritto di seguito:  
  
    ```  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    ```  
  
### <a name="example-b-configuring-resource-governor-transact-sql"></a>Esempio B: Configurazione di Resource Governor (Transact-SQL)  
 Nell'esempio seguente vengono effettuati i passaggi seguenti all'interno di un'unica transazione:  
  
1.  Creazione del pool di risorse `pMAX_CPU_PERCENT_20` .  
  
2.  Creazione del gruppo del carico di lavoro `gMAX_CPU_PERCENT_20` .  
  
3.  Creazione della funzione di classificazione `rgclassifier_MAX_CPU()` che utilizza il nome utente creato nell'esempio precedente.  
  
4.  Registrazione della funzione di classificazione con Resource Governor.  
  
 Dopo l'esecuzione del commit della transazione, nell'esempio vengono applicate le modifiche di configurazione richieste nell'istruzione ALTER WORKLOAD GROUP o ALTER RESOURCE POOL.  
  
> [!IMPORTANT]  
>  Nell'esempio seguente viene usato il nome dell'utente di esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creato in "Esempio A: Impostazione di un accesso e di un utente (Transact-SQL)", *nome_dominio*`\MAX_CPU`. Sostituire questo nome con quello dell'utente relativo all'account di accesso che si intende utilizzare per la creazione di backup compressi con priorità bassa.  
  
```sql  
-- Configure Resource Governor.  
BEGIN TRAN  
USE master;  
-- Create a resource pool that sets the MAX_CPU_PERCENT to 20%.   
CREATE RESOURCE POOL pMAX_CPU_PERCENT_20  
   WITH  
      (MAX_CPU_PERCENT = 20);  
GO  
-- Create a workload group to use this pool.   
CREATE WORKLOAD GROUP gMAX_CPU_PERCENT_20  
USING pMAX_CPU_PERCENT_20;  
GO  
-- Create a classification function.  
-- Note that any request that does not get classified goes into   
-- the 'Default' group.  
CREATE FUNCTION dbo.rgclassifier_MAX_CPU() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
    DECLARE @workload_group_name AS sysname  
      IF (SUSER_NAME() = 'domain_name\MAX_CPU')  
          SET @workload_group_name = 'gMAX_CPU_PERCENT_20'  
    RETURN @workload_group_name  
END;  
GO  
  
-- Register the classifier function with Resource Governor.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION= dbo.rgclassifier_MAX_CPU);  
COMMIT TRAN;  
GO  
-- Start Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
 [&#91;Torna all'inizio&#93;](#Top)  
  
##  <a name="verifying-the-classification-of-the-current-session-transact-sql"></a><a name="verifying"></a> Verifica della classificazione della sessione corrente (Transact-SQL)  
 Facoltativamente, accedere come l'utente specificato nella funzione di classificazione e verificare la classificazione della sessione eseguendo l'istruzione [SELECT](../../t-sql/queries/select-transact-sql.md) seguente in Esplora oggetti:  
  
```sql  
USE master;  
SELECT sess.session_id, sess.login_name, sess.group_id, grps.name   
FROM sys.dm_exec_sessions AS sess   
JOIN sys.dm_resource_governor_workload_groups AS grps   
    ON sess.group_id = grps.group_id  
WHERE session_id > 50;  
GO  
```  
  
 Nella colonna **name** del riquadro dei risultati dovrebbero essere elencate una o più sessioni per il nome del gruppo di carico di lavoro specificato nella funzione di classificazione.  
  
> [!NOTE]  
>  Per informazioni sulle viste a gestione dinamica chiamate da questa istruzione SELECT, vedere [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) e [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md).  
  
 [&#91;Torna all'inizio&#93;](#Top)  
  
##  <a name="compressing-backups-using-a-session-with-limited-cpu"></a><a name="creating_compressed_backup"></a> Compressione di backup utilizzando una sessione con utilizzo della CPU limitato  
 Per creare un backup compresso in una sessione con un utilizzo massimo della CPU limitato, accedere come l'utente specificato nella funzione di classificazione. Nel comando di backup specificare WITH COMPRESSION ([!INCLUDE[tsql](../../includes/tsql-md.md)]) o selezionare **Comprimi backup** ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]). Per creare un backup compresso del database, vedere [Creazione di un backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
### <a name="example-c-creating-a-compressed-backup-transact-sql"></a>Esempio C: Creazione di un backup compresso (Transact-SQL)  
 Nell'esempio seguente [BACKUP](../../t-sql/statements/backup-transact-sql.md) viene creato un backup compresso completo del database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] nel nuovo file di backup formattato `Z:\SQLServerBackups\AdvWorksData.bak`.  
  
```sql  
--Run backup statement in the gBackup session.  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   MEDIADESCRIPTION='AdventureWorks2012 Compressed Data Backups'  
   DESCRIPTION='First database backup on AdventureWorks2012 Compressed Data Backups media set'  
   COMPRESSION;  
GO  
```  
  
 [&#91;Torna all'inizio&#93;](#Top)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e testare una funzione di classificazione definita dall'utente](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  
