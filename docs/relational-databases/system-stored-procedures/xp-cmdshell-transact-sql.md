---
title: xp_cmdshell (Transact-SQL) Documenti Microsoft
ms.custom: ''
ms.date: 03/30/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_cmdshell
- xp_cmdshell_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: 18935cf4-b320-4954-b6c1-e007fcefe358
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2ce32fc31373077418e77d31ce064d60e23f1b24
ms.sourcegitcommit: fc5b757bb27048a71bb39755648d5cefe25a8bc6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "80402695"
---
# <a name="xp_cmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Genera una shell dei comandi di Windows e passa una stringa per l'esecuzione. L'eventuale output viene restituito in forma di righe di testo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>Argomenti  
 **'** *command_string* **'**  
 Stringa che contiene un comando da passare al sistema operativo. *command_string* è **varchar(8000)** o **nvarchar(4000)**, senza alcun valore predefinito. *command_string* non può contenere più di un set di virgolette doppie. Se nei percorsi di file o nei nomi di programma a cui si fa riferimento in *command_string,* è necessaria una singola coppia di virgolette. In caso di problemi nell'utilizzo di spazi incorporati nelle stringhe, valutare l'utilizzo di nomi di file in formato FAT 8.3 come soluzione alternativa.  
  
 **no_output**  
 Parametro facoltativo che indica che non è richiesta la restituzione di output al client.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="result-sets"></a>Set di risultati  
 L'istruzione `xp_cmdshell` seguente restituisce un elenco dei file con estensione exe contenuti nella directory corrente.  
  
```  
EXEC xp_cmdshell 'dir *.exe';  
GO  
```  
  
 Le righe vengono restituite in una colonna **nvarchar(255).** Se viene utilizzata l'opzione **no_output,** verrà restituito solo quanto segue:  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>Osservazioni  
 Il processo di Windows generato da **xp_cmdshell** ha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli stessi diritti di sicurezza dell'account del servizio.  
  
 **xp_cmdshell** funziona in modo sincrono. ovvero il controllo viene restituito al chiamante solo dopo il completamento del comando della shell.  
  
 **xp_cmdshell** possono essere abilitate e disabilitate utilizzando la gestione basata su criteri o eseguendo **sp_configure**. Per ulteriori informazioni, consultate [Configurazione superficie di](../../relational-databases/security/surface-area-configuration.md) attacco e Opzione di configurazione xp_cmdshell [Server](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
> [!IMPORTANT]
>  Se **xp_cmdshell** viene eseguito all'interno di un batch e restituisce un errore, il batch avrà esito negativo.
  
## <a name="xp_cmdshell-proxy-account"></a>Account proxy per xp_cmdshell  
 Quando viene chiamato da un utente che non è membro del ruolo predefinito del server **sysadmin** , **xp_cmdshell** si connette a Windows utilizzando il nome account e la password archiviati nella credenziale denominata **"#xp_cmdshell_proxy_account "**. Se questa credenziale proxy non esiste, **xp_cmdshell** avrà esito negativo.  
  
 È possibile creare le credenziali dell'account proxy eseguendo **sp_xp_cmdshell_proxy_account**. Questa stored procedure accetta un nome utente e una password di Windows come argomenti. Il comando seguente, ad esempio, crea una credenziale proxy per l'utente di dominio di Windows `SHIPPING\KobeR` con la password di Windows `sdfh%dkc93vcMt0`.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 Per ulteriori informazioni, vedere [sp_xp_cmdshell_proxy_account &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 Poiché gli utenti malintenzionati a volte tentano di elevare i propri privilegi utilizzando **xp_cmdshell**, **xp_cmdshell** è disabilitato per impostazione predefinita. Utilizzare **sp_configure** o **la gestione basata su criteri** per abilitarla. Per altre informazioni, vedere [Opzione di configurazione del server xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
 Quando viene abilitata per la prima volta, **xp_cmdshell** richiede l'autorizzazione CONTROL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SERVER per l'esecuzione e il processo di Windows creato da **xp_cmdshell** ha lo stesso contesto di sicurezza dell'account del servizio. L'account [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del servizio ha spesso più autorizzazioni di quelle necessarie per il lavoro eseguito dal processo creato da **xp_cmdshell**. Per migliorare la sicurezza, l'accesso **ai xp_cmdshell** deve essere limitato agli utenti con privilegi elevati.  
  
 Per consentire agli utenti **xp_cmdshell**non amministratori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di utilizzare xp_cmdshell e consentire la creazione di processi figlio con il token di sicurezza di un account con privilegi inferiori, attenersi alla seguente procedura:  
  
1.  Creare e personalizzare un account utente locale di Windows o un account di dominio con i privilegi minimi richiesti dai processi.  
  
2.  Utilizzare la procedura di sistema **sp_xp_cmdshell_proxy_account** per configurare **xp_cmdshell** per l'utilizzo di tale account con privilegi minimi.  
  
    > [!NOTE]  
    >  È inoltre possibile configurare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] questo account proxy utilizzando facendo clic con il pulsante destro del mouse su **Proprietà** nel nome del server in Esplora oggetti e nella sezione Protezione della scheda **Protezione.** **Server proxy account**  
  
3.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], utilizzando il database `GRANT exec ON xp_cmdshell TO N'<some_user>';` master, eseguire l'istruzione per dare agli utenti specifici non amministratori di**sistema** la possibilità di eseguire **xp_cmdshell**. L'utente specificato deve esistere nel database master.  
  
 Ora gli utenti non amministratori possono avviare i processi del sistema operativo con **xp_cmdshell** e tali processi vengono eseguiti con le autorizzazioni dell'account proxy configurato. Gli utenti con autorizzazione CONTROL SERVER (membri del ruolo predefinito del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server **sysadmin)** continueranno a ricevere le autorizzazioni dell'account del servizio per i processi figlio avviati da **xp_cmdshell**.  
  
 Per determinare l'account di Windows utilizzato da **xp_cmdshell** all'avvio dei processi del sistema operativo, eseguire l'istruzione seguente:  
  
```  
xp_cmdshell 'whoami.exe'  
  
```  
  
 Per determinare il contesto di sicurezza per un altro accesso, eseguire gli elementi seguenti:  
  
```  
EXECUTE AS LOGIN = '<other_login>' ;  
GO  
xp_cmdshell 'whoami.exe' ;  
REVERT ;  
  
```  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-a-list-of-executable-files"></a>R. Restituzione di un elenco di file eseguibili  
 Nell'esempio seguente viene mostrato l'utilizzo della stored procedure estesa `xp_cmdshell` per eseguire un comando di directory.  
  
```  
EXEC master..xp_cmdshell 'dir *.exe'  
```  
  
### <a name="b-returning-no-output"></a>B. Esecuzione di un comando senza restituzione dell'output  
 Nell'esempio seguente viene mostrato l'utilizzo di `xp_cmdshell` per eseguire una stringa di comandi senza restituire alcun output al client.  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks', NO_OUTPUT;  
GO  
```  
  
### <a name="c-using-return-status"></a>C. Restituzione del codice di stato  
 Nell'esempio seguente, `xp_cmdshell` la stored procedure estesa suggerisce anche lo stato di restituzione. Il valore restituito viene archiviato nella variabile `@result`.  
  
```  
DECLARE @result int;  
EXEC @result = xp_cmdshell 'dir *.exe';  
IF (@result = 0)  
   PRINT 'Success'  
ELSE  
   PRINT 'Failure';  
```  
  
### <a name="d-writing-variable-contents-to-a-file"></a>D. Scrittura del contenuto di una variabile in un file  
 Nell'esempio seguente il contenuto della variabile `@var` viene scritto in un file denominato `var_out.txt` nella directory corrente del server.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'Hello world';  
SET @cmd = 'echo ' + @var + ' > var_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
### <a name="e-capturing-the-result-of-a-command-to-a-file"></a>E. Memorizzazione del risultato di un comando in un file  
 Nell'esempio seguente il contenuto della directory corrente viene scritto nel file `dir_out.txt` nella directory corrente del server.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'dir/p';  
SET @cmd = @var + ' > dir_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure estese generali &#40;&#41;Transact-SQLGeneral Extended Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Opzione di configurazione di xp_cmdshell Server](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [Configurazione superficie](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account &#40;transact-sqlSql&#41;SQL](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
