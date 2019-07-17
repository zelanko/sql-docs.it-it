---
title: sp_setapprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/12/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_setapprole
- sp_setapprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setapprole
ms.assetid: cf0901c0-5f90-42d4-9d5b-8772c904062d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 44e7b670ef5f16b6df861e939f9b8b2d9ace8dd5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104424"
---
# <a name="spsetapprole-transact-sql"></a>sp_setapprole (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Attiva le autorizzazioni associate a un ruolo applicazione nel database corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  

```sql
sp_setapprole [ @rolename = ] 'role',  
    [ @password = ] { encrypt N'password' }
      |  
        'password' [ , [ @encrypt = ] { 'none' | 'odbc' } ]  
        [ , [ @fCreateCookie = ] true | false ]  
    [ , [ @cookie = ] @cookie OUTPUT ]  
```

## <a name="arguments"></a>Argomenti

`[ @rolename = ] 'role'` È il nome del ruolo applicazione definito nel database corrente. *ruolo* viene **sysname**, non prevede alcun valore predefinito. *ruolo* deve esistere nel database corrente.  
  
`[ @password = ] { encrypt N'password' }` È la password necessaria per attivare il ruolo applicazione. *la password* viene **sysname**, non prevede alcun valore predefinito. *la password* è possibile offuscare usando ODBC **crittografare** (funzione). Quando si usa la **crittografare** funzione, la password deve essere convertita in una stringa Unicode inserendo **N** prima della virgoletta.  
  
 L'opzione crittografia non è supportato per le connessioni che usano **SqlClient**.  
  
> [!IMPORTANT]  
> ODBC **crittografare** funzione non supporta la crittografia. È consigliabile evitare l'utilizzo di questa funzione per proteggere le password trasmesse in rete. Per informazioni da trasmettere in rete, utilizzare i protocolli SSL o IPSec.
  
 **@encrypt = 'none'**  
 Indica che non è richiesto l'utilizzo di tecniche di offuscamento. La password viene passata a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come testo normale. Questa è l'impostazione predefinita.  
  
 **@encrypt= 'odbc'**  
 Specifica che ODBC eseguirà l'offuscamento della password usando ODBC **crittografare** funzione prima di inviare la password per il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. È possibile specificare questa opzione solo se si utilizza un client ODBC o il provider OLE DB per SQL Server.  
  
`[ @fCreateCookie = ] true | false` Specifica se un cookie deve essere creato. **true** viene implicitamente convertito in 1. **false** viene implicitamente convertito in 0.  
  
`[ @cookie = ] @cookie OUTPUT` Specifica un parametro di output per il cookie. Il cookie viene generato solo se il valore di **@fCreateCookie** viene **true**. **varbinary(8000)**  
  
> [!NOTE]  
> Il parametro **OUTPUT** del cookie per **sp_setapprole** è attualmente documentato come **varbinary(8000)** che rappresenta la lunghezza massima corretta. Tuttavia, l'implementazione corrente restituisce **varbinary(50)** . Le applicazioni devono continuare a riservare **varbinary(8000** in modo che l'applicazione continua a funzionare correttamente se il cookie di restituisce le dimensioni aumentano in una versione futura.
  
## <a name="return-code-values"></a>Valori restituiti

 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note

 Dopo un'applicazione l'attivazione di ruolo usando **sp_setapprole**, tale ruolo rimane attivo fino a quando l'utente si disconnette dal server o all'esecuzione **sp_unsetapprole**. **sp_setapprole** può essere eseguita solo da direct [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzioni. **sp_setapprole** non può essere eseguita all'interno di un'altra stored procedure o una transazione definita dall'utente.  
  
 Per una panoramica dei ruoli applicazione, vedere [i ruoli applicazione](../../relational-databases/security/authentication-access/application-roles.md).  
  
> [!IMPORTANT]  
> Per proteggere la password del ruolo dell'applicazione durante la trasmissione attraverso una rete, è consigliabile usare sempre una connessione crittografata quando si abilita un ruolo applicazione.
> Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC **crittografare** opzione non è supportato da **SqlClient**. Se è necessario archiviare credenziali, crittografarle con le funzioni CryptoAPI. Il parametro *password* viene archiviato come hash unidirezionale. Per mantenere la compatibilità con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i criteri di complessità delle password non viene applicato dal **sp_addapprole**. Per applicare criteri di complessità delle password, usare [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissions

Richiede l'appartenenza al **pubblica** e conoscere la password per il ruolo.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-activating-an-application-role-without-the-encrypt-option"></a>R. Attivazione di un ruolo applicazione senza l'opzione encrypt

 Nell'esempio seguente viene attivato il ruolo applicazione `SalesAppRole` con la password non crittografata `AsDeF00MbXX`, creato con autorizzazioni specifiche per l'applicazione utilizzata dall'utente corrente.

```sql
EXEC sys.sp_setapprole 'SalesApprole', 'AsDeF00MbXX';  
GO
```

### <a name="b-activating-an-application-role-with-a-cookie-and-then-reverting-to-the-original-context"></a>B. Attivazione di un ruolo applicazione con un cookie e ripristino del contesto originale

 Nell'esempio seguente viene attivato il ruolo applicazione `Sales11` con la password `fdsd896#gfdbfdkjgh700mM` e viene creato un cookie. Nell'esempio viene restituito il nome dell'utente corrente e quindi viene ripristinato il contesto originale tramite l'esecuzione di `sp_unsetapprole`.  

```sql
DECLARE @cookie varbinary(8000);  
EXEC sys.sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sys.sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.
GO
```

## <a name="see-also"></a>Vedere anche

 [Stored procedure di sistema &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) [Stored procedure di sicurezza &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md) [CREATE APPLICATION ROLE &#40;Transact-SQL&#41; ](../../t-sql/statements/create-application-role-transact-sql.md) [DROP APPLICATION ROLE &#40;Transact-SQL&#41; ](../../t-sql/statements/drop-application-role-transact-sql.md) [sp_unsetapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)
