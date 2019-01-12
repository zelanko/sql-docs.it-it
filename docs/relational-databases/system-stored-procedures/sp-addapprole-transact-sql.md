---
title: sp_addapprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addapprole_TSQL
- sp_addapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addapprole
ms.assetid: 24200295-9a54-4cab-9922-fb2e88632721
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 40e397bd63d8018d2043a1aced4824f48e4ddc9a
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54135871"
---
# <a name="spaddapprole-transact-sql"></a>sp_addapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un ruolo applicazione al database corrente.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Uso [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addapprole [ @rolename = ] 'role' , [ @password = ] 'password'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@rolename =** ] **'**_ruolo_**'**  
 Nome del nuovo ruolo applicazione. *ruolo* viene **sysname**, non prevede alcun valore predefinito. *ruolo* deve essere un identificatore valido e non può già esistere nel database corrente.  
  
 I nomi dei ruoli applicazione possono includere da 1 a 128 caratteri, compresi lettere, simboli e numeri. I nomi di ruolo non possono contenere una barra rovesciata (\\) né essere NULL o una stringa vuota (").  
  
 [  **@password =** ] **'**_password_**'**  
 Password richiesta per attivare il ruolo applicazione. *la password* viene **sysname**, non prevede alcun valore predefinito. *password* non può essere NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli utenti (e i ruoli) non si diversificano completamente dagli schemi. A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], gli schemi sono completamente distinti dai ruoli. Questa nuova architettura si riflette nel funzionamento dell'istruzione CREATE APPLICATION ROLE. Questa istruzione sostituisce **sp_addapprole**.  
  
 Per mantenere la compatibilità con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **sp_addapprole** eseguirà le operazioni seguenti:  
  
-   Se uno schema con lo stesso nome del ruolo applicazione non esiste, tale schema verrà creato. Il nuovo schema sarà di proprietà del ruolo applicazione e sarà lo schema predefinito del ruolo applicazione.  
  
-   Se invece uno schema con lo stesso nome del ruolo applicazione esiste già, la procedura verrà interrotta.  
  
-   La complessità delle password non viene controllata dal **sp_addapprole**. ma viene controllata dall'istruzione CREATE APPLICATION ROLE.  
  
 Il parametro *password* viene archiviato come hash unidirezionale.  
  
 Il **sp_addapprole** stored procedure non può essere eseguita dall'interno di una transazione definita dall'utente.  
  
> [!IMPORTANT]  
>  Microsoft ODBC **crittografare** opzione non è supportato da **SqlClient**. Se possibile, richiedere all'utente di immettere le credenziali del ruolo applicazione in fase di esecuzione. Evitare di archiviare le credenziali in un file. Se è necessario disporre di credenziali persistenti, crittografarle tramite le funzioni CryptoAPI.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER ANY APPLICATION ROLE nel database. Se uno schema con lo stesso nome e lo stesso proprietario del nuovo ruolo non esiste, è richiesta anche l'autorizzazione CREATE SCHEMA nel database.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente aggiunge il nuovo ruolo applicazione `SalesApp` con la password `x97898jLJfcooFUYLKm387gf3` al database corrente.  
  
```  
EXEC sp_addapprole 'SalesApp', 'x97898jLJfcooFUYLKm387gf3' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  
