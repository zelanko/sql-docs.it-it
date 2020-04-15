---
title: sp_setapprole (Transact-SQL) Documenti Microsoft
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
ms.openlocfilehash: b158c4571deadadeaee23ffa6e46eb48a8c8446e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299604"
---
# <a name="sp_setapprole-transact-sql"></a>sp_setapprole (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Attiva le autorizzazioni associate a un ruolo applicazione nel database corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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

`[ @rolename = ] 'role'`È il nome del ruolo applicazione definito nel database corrente. *role* è **di tipo sysname**, senza alcun valore predefinito. *ruolo* deve esistere nel database corrente.  
  
`[ @password = ] { encrypt N'password' }`È la password necessaria per attivare il ruolo applicazione. *password* è **di tipo sysname**, senza alcun valore predefinito. *password* può essere offuscata utilizzando la funzione **di crittografia** ODBC. Quando si utilizza la funzione **di crittografia,** la password deve essere convertita in una stringa Unicode inserendo **N** prima delle prime virgolette.  
  
 L'opzione di crittografia non è supportata nelle connessioni che utilizzano **SqlClient**.  
  
> [!IMPORTANT]  
> La funzione **di crittografia** ODBC non fornisce la crittografia. È consigliabile evitare l'utilizzo di questa funzione per proteggere le password trasmesse in rete. Se queste informazioni verranno trasmesse attraverso una rete, utilizzare TLS o IPSec.
  
 **@encrypt"nessuno"**  
 Indica che non è richiesto l'utilizzo di tecniche di offuscamento. La password viene passata a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come testo normale. Questa è la modalità predefinita.  
  
 **@encrypt'odbc'**  
 Specifica che ODBC ofilzerà la password **encrypt** utilizzando la funzione di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]crittografia ODBC prima di inviare la password all'oggetto . È possibile specificare questa opzione solo se si utilizza un client ODBC o il provider OLE DB per SQL Server.  
  
`[ @fCreateCookie = ] true | false`Specifica se deve essere creato un cookie. **true** viene convertito in modo implicito in 1. **false** viene convertito in modo implicito in 0.  
  
`[ @cookie = ] @cookie OUTPUT`Specifica un parametro di output per contenere il cookie. Il cookie viene generato solo se il valore di ** \@fCreateCookie** è **true**. **varbinary(8000)**  
  
> [!NOTE]  
> Il parametro **OUTPUT** del cookie per **sp_setapprole** è attualmente documentato come **varbinary(8000)** che rappresenta la lunghezza massima corretta. Tuttavia, l'implementazione corrente restituisce **varbinary(50)**. Le applicazioni devono continuare a riservare **varbinary(8000)** in modo che l'applicazione continui a funzionare correttamente se le dimensioni del cookie restituiscono aumentino in una versione futura.
  
## <a name="return-code-values"></a>Valori del codice restituito

 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Osservazioni

 Dopo l'attivazione di un ruolo applicazione utilizzando **sp_setapprole**, il ruolo rimane attivo finché l'utente non si disconnette dal server o **esegue sp_unsetapprole**. **sp_setapprole** possono essere eseguite [!INCLUDE[tsql](../../includes/tsql-md.md)] solo da istruzioni dirette. **sp_setapprole** non può essere eseguito all'interno di un'altra stored procedure o all'interno di una transazione definita dall'utente.  
  
 Per una panoramica dei ruoli applicazione, vedere [Ruoli applicazione](../../relational-databases/security/authentication-access/application-roles.md).  
  
> [!IMPORTANT]  
> Per proteggere la password del ruolo applicazione quando viene trasmessa attraverso una rete, è necessario utilizzare sempre una connessione crittografata quando si abilita un ruolo applicazione.
> L'opzione [!INCLUDE[msCoName](../../includes/msconame-md.md)] **di crittografia** ODBC non è supportata da **SqlClient**. Se è necessario archiviare credenziali, crittografarle con le funzioni CryptoAPI. La *password* del parametro viene archiviata come hash unidirezionale. Per mantenere la compatibilità con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i criteri di complessità delle password non vengono applicati da **sp_addapprole**. Per applicare i criteri di complessità delle password, utilizzare [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md).  
  
## <a name="permissions"></a>Autorizzazioni

Richiede l'appartenenza **al pubblico** e la conoscenza della password per il ruolo.  
  
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

 Le stored procedure di sistema &#40;le stored procedure di sicurezza di [Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) &#40;[Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md) [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md) DROP ROLE &#40;&#41;[Transact-SQLsql](../../t-sql/statements/drop-application-role-transact-sql.md) [sp_unsetapprole sp_unsetapprole &#40;Transact-&#41;SQLSqlSQL](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)
