---
title: sp_addlinkedsrvlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlinkedsrvlogin_TSQL
- sp_addlinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlinkedsrvlogin
ms.assetid: eb69f303-1adf-4602-b6ab-f62e028ed9f6
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c34d7f326c10ceebb3ee3b97c72b583e13a78ff5
ms.sourcegitcommit: acb5de9f493238180d13baa302552fdcc30d83c0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/12/2019
ms.locfileid: "59542191"
---
# <a name="spaddlinkedsrvlogin-transact-sql"></a>sp_addlinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea o aggiorna un mapping tra un account di accesso nell'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e un account di sicurezza in un server remoto.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_addlinkedsrvlogin [ @rmtsrvname = ] 'rmtsrvname'   
     [ , [ @useself = ] { 'TRUE' | 'FALSE' | NULL } ]   
     [ , [ @locallogin = ] 'locallogin' ]   
     [ , [ @rmtuser = ] 'rmtuser' ]   
     [ , [ @rmtpassword = ] 'rmtpassword' ]   
```  
  
## <a name="arguments"></a>Argomenti  
 `[ @rmtsrvname = ] 'rmtsrvname'`  
 Nome di un server collegato a cui viene applicato il mapping dell'account di accesso. *rmtsrvname* viene **sysname**, non prevede alcun valore predefinito.  
  
 `[ @useself = ] { 'TRUE' | 'FALSE' | NULL }'`  
 Determina se la connessione a *rmtsrvname* per rappresentare gli accessi locali o inviando esplicitamente un account di accesso e una password. Il tipo di dati viene **varchar (** 8 **)**, con un valore predefinito è TRUE.  
  
 Il valore TRUE specifica che gli account di accesso usare le proprie credenziali per connettersi al *rmtsrvname*, con la *rmtuser* e *rmtpassword* argomenti vengano ignorati. FALSE specifica che il *rmtuser* e *rmtpassword* argomenti vengono utilizzati per connettersi al *rmtsrvname* per l'oggetto specificato *locallogin* . Se *rmtuser* e *rmtpassword* sono anche impostato su NULL, nessun account di accesso o la password viene usato per connettersi al server collegato.  
  
 `[ @locallogin = ] 'locallogin'`  
 Account di accesso per il server locale. *locallogin* viene **sysname**, con un valore predefinito è NULL. NULL indica che questa voce viene applicata a tutti gli accessi locali che si connettono a *rmtsrvname*. Se non è NULL, *locallogin* può essere un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso o un account di accesso di Windows. È necessario che l'account di accesso di Windows disponga dell'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ottenuto tramite concessione diretta o in seguito all'appartenenza a un gruppo di Windows che dispone dell'accesso.  
  
 `[ @rmtuser = ] 'rmtuser'`  
 Account di accesso remoto utilizzato per connettersi al *rmtsrvname* quando @useself è FALSE. Quando il server remoto è un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non usa l'autenticazione di Windows *rmtuser* è un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso. *rmtuser* viene **sysname**, con un valore predefinito è NULL.  
  
 `[ @rmtpassword = ] 'rmtpassword'`  
 È la password associata *rmtuser*. *rmtpassword* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 Quando un utente accede al server locale ed esegue una query distribuita che accede a una tabella del server collegato, il server locale deve accedere al server collegato per parte dell'utente che desidera accedere a tale tabella. Per specificare le credenziali dell'account di accesso utilizzate nel server locale per l'accesso al server collegato, utilizzare la procedura sp_addlinkedsrvlogin.  
  
> [!NOTE]  
>  Per creare piani di query ottimali quando si utilizza una tabella in un server collegato, è necessario che Query Processor ottenga le statistiche di distribuzione dei dati dal server collegato. Gli utenti con autorizzazioni limitate per qualsiasi colonna della tabella potrebbero non disporre delle autorizzazioni sufficienti per ottenere tutte le statistiche utili, nonché ricevere un piano di query meno efficiente e riscontrare un peggioramento delle prestazioni. Se il server collegato è un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], per ottenere tutte le statistiche disponibili, l'utente deve essere il proprietario della tabella oppure un membro del ruolo predefinito del server sysadmin o del ruolo predefinito del database db_owner o db_ddladmin sul server collegato. In SQL Server 2012 SP1 le restrizioni delle autorizzazioni vengono modificate per ottenere le statistiche e gli utenti con l'autorizzazione SELECT possono accedere alle statistiche disponibili tramite DBCC SHOW_STATISTICS. Per altre informazioni, vedere la sezione autorizzazioni [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).  
  
 Un mapping predefinito tra tutti gli account di accesso del server locale e gli account di accesso remoti del server collegato viene creato automaticamente tramite la procedura sp_addlinkedserver. In base al mapping predefinito, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono utilizzate le credenziali dell'account di accesso locale dell'utente durante la connessione al server collegato. Ciò equivale all'esecuzione della procedura sp_addlinkedsrvlogin con @useself impostata su **true** per il server collegato, senza specificare un nome utente locale. Utilizzare la procedura sp_addlinkedsrvlogin solo per modificare il mapping predefinito o per aggiungere nuovi mapping per account di accesso locali specifici. Per eliminare il mapping predefinito o qualsiasi altro mapping, utilizzare la procedura sp_droplinkedsrvlogin.  
  
 Anziché utilizzare la procedura sp_addlinkedsrvlogin per creare un mapping predefinito agli account di accesso, per la connessione a un server collegato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può utilizzare automaticamente le credenziali di sicurezza di Windows (nome di accesso e password di Windows) di un utente che invia la query se sussistono le seguenti condizioni:  
  
-   Un utente si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in base all'autenticazione di Windows.  
  
-   È disponibile la delega dell'account di sicurezza nel client e nel server di origine.  
  
-   Il provider supporta l'autenticazione di Windows, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]eseguito in Windows.  
  
> [!NOTE]  
>  Non è necessario abilitare la delega per scenari a hop singolo ma è necessario abilitarla per gli scenari a più hop.  
  
 Dopo che l'autenticazione è stata eseguita dal server collegato in base ai mapping definiti con la procedura sp_addlinkedsrvlogin eseguita nell'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], le autorizzazioni per singoli oggetti nel database remoto sono determinate dal server collegato, non dal server locale.  
  
 Non è possibile eseguire la procedura sp_addlinkedsrvlogin all'interno di una transazione definita dall'utente.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER ANY LOGIN nel server.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-connecting-all-local-logins-to-the-linked-server-by-using-their-own-user-credentials"></a>A. Connessione di tutti gli account di accesso locali al server collegato utilizzando le relative credenziali  
 Nell'esempio seguente viene creato un mapping per assicurare che tutti gli account di accesso del server locale si connettano al server collegato `Accounts` utilizzando le proprie credenziali.  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts';  
```  
  
 e  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'true';  
```  
  
> [!NOTE]  
>  Se ci sono mapping espliciti creati per account di accesso individuali, essi hanno la precedenza su ogni eventuale mapping globale per quel server collegato.  
  
### <a name="b-connecting-a-specific-login-to-the-linked-server-by-using-different-user-credentials"></a>B. Connessione di un account di accesso specifico al server collegato utilizzando credenziali utente diverse  
 Nell'esempio seguente viene creato un mapping per assicurare che l'utente di Windows `Domain\Mary` si connetta al server collegato `Accounts` tramite l'account `MaryP` e la password `d89q3w4u`.  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'false', 'Domain\Mary', 'MaryP', 'd89q3w4u';  
```  
  
> [!IMPORTANT]  
>  In questo esempio non viene utilizzata l'autenticazione di Windows. Le password verranno trasmesse senza essere crittografate. Le password possono essere visibili nelle definizioni delle origini dei dati e negli script salvati su disco, in copie di backup e in file di log. Non utilizzare mai una password di amministratore per questo tipo di connessioni. Per ulteriori informazioni sulla sicurezza specifiche al proprio ambiente, consultare l'amministratore di rete.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di server collegati &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
