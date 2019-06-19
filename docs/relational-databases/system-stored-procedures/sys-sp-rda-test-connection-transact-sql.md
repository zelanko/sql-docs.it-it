---
title: sys.sp_rda_test_connection (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_test_connection
- sys.sp_rda_test_connection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_test_connection stored procedure
ms.assetid: e2ba050c-d7e3-4f33-8281-c9b525b4edb4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cdf171c66c19d87ea4919eeb55dca65f14b89ebd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65982875"
---
# <a name="syssprdatestconnection-transact-sql"></a>sys.sp_rda_test_connection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Test della connessione da SQL Server per il server Azure remoto e segnala i problemi che potrebbero impedire la migrazione dei dati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
EXECUTE sys.sp_rda_test_connection  
   @database_name = N'db_name',   
   @server_address = N'azure_server_fully_qualified_address',  
   @azure_username = N'azure_username',   
   @azure_password = N'azure_password',  
   @credential_name = N'credential_name'  
  
```  
  
## <a name="arguments"></a>Argomenti  
 @database_name = N'*db_name*'  
 Il nome del database di SQL Server abilitati per Stretch. Questo parametro è facoltativo.  
  
 @server_address = N'*azure_server_fully_qualified_address*'  
 L'indirizzo completo del server di Azure.  
  
-   Se si specifica un valore per **@database_name** , ma il database specificato non è abilitata per l'estensione, quindi è necessario specificare un valore per **@server_address** .  
  
-   Se si specifica un valore per **@database_name** e il database specificato è abilitata per l'estensione, quindi non devi fornire un valore per **@server_address** . Se si specifica un valore per **@server_address** , la stored procedure viene ignorato e Usa il server di Azure già associate con il database abilitati per Stretch.  
  
 @azure_username = N'*azure_username*  
 Il nome utente per il server Azure remoto.  
  
 @azure_password = N'*azure_password*'  
 La password per il server Azure remoto.  
  
 @credential_name = N'*credential_name*'  
 Anziché fornire un nome utente e password, è possibile fornire il nome di una credenziale archiviata nel database abilitati per Stretch.  
  
## <a name="return-code-values"></a>Valori restituiti  
 In caso di **success**, sp_rda_test_connection restituito errore 14855 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_SUCCEEDED) con livello di gravità EX_INFO e restituire il codice ha esito positivo.  
  
 In caso di **errore**, sp_rda_test_connection restituito errore 14856 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_FAILED) con livello di gravità EX_USER e codice di restituzione di un errore.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|link_state|INT|Uno dei valori seguenti, che corrispondono ai valori per **link_state_desc**.<br /><br /> -   0<br />-   1<br />-   2<br />-   3<br />-   4|  
|link_state_desc|varchar(32)|Uno dei valori seguenti, che corrispondono agli ultimi valori per **link_state**.<br /><br /> -INTEGRO<br />     Il tra SQL Server e di Azure remoto server è integro.<br />-   ERROR_AZURE_FIREWALL<br />     Il firewall di Azure impedisce il collegamento tra SQL Server e il server Azure remoto.<br />-   ERROR_NO_CONNECTION<br />     SQL Server non è possibile stabilire una connessione al server Azure remoto.<br />-   ERROR_AUTH_FAILURE<br />     Errore di autenticazione impedisce il collegamento tra SQL Server e il server Azure remoto.<br />-ERRORE<br />     Un errore che non è un problema di autenticazione, un problema di connettività o un problema del firewall impedisce il collegamento tra SQL Server e il server Azure remoto.|  
|error_number|INT|Il numero dell'errore. Se non si verificano errori, questo campo è NULL.|  
|error_message|nvarchar(1024)|Messaggio di errore. Se non si verificano errori, questo campo è NULL.|  
  
## <a name="permissions"></a>Permissions  
 Richiede autorizzazioni db_owner.  
  
## <a name="examples"></a>Esempi  
  
### <a name="check-the-connection-from-sql-server-to-the-remote-azure-server"></a>Verificare la connessione da SQL Server e il server Azure remoto  
  
```sql  
EXECUTE sys.sp_rda_test_connection @database_name = N'<Stretch-enabled database>'  
GO  
  
```  
  
 I risultati mostrano che SQL Server non è possibile connettersi al server Azure remoto.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|2|ERROR_NO_CONNECTION|*\<numero di errore correlati alla connessione >*|*\<messaggio di errore correlati alla connessione >*|  
  
### <a name="check-the-azure-firewall"></a>Controllare il firewall di Azure  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 I risultati mostrano che il firewall di Azure impedisce il collegamento tra SQL Server e il server Azure remoto.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|1|ERROR_AZURE_FIREWALL|*\<numero di errore correlato al firewall >*|*\<messaggio di errore correlato al firewall >*|  
  
### <a name="check-authentication-credentials"></a>Verificare le credenziali di autenticazione  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 I risultati mostrano un errore di autenticazione che impedisce il collegamento tra SQL Server e il server Azure remoto.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|3|ERROR_AUTH_FAILURE|*\<numero di errore correlati all'autenticazione >*|*\<messaggio di errore correlati all'autenticazione >*|  
  
### <a name="check-the-status-of-the-remote-azure-server"></a>Controllare lo stato del server Azure remoto  
  
```sql  
USE <SQL Server database>  
GO  
EXECUTE sys.sp_rda_test_connection   
    @server_address = N'<server name>.database.windows.net',   
    @azure_username = N'<user name>',   
    @azure_password = N'<password>'  
GO  
  
```  
  
 I risultati mostrano che la connessione sia integra e che è possibile abilitare Stretch Database per il database specificato.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|0|HEALTHY|NULL|NULL|  
  
  
