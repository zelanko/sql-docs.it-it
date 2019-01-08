---
title: Non più utilizzate funzionalità del motore di Database in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- VIA protocol
- unsupported features [SQL Server]
- SQL Mail
- discontinued functionality [SQL Server]
- RESTORE WITH DBO_ONLY
- BACKUP WITH PASSWORD
- user instances enabled
- BACKUP WITH MEDIAPASSWORD
- AWE
- SQL-DMO
- '*= and =*'
- 80 compatibility levels
- COMPUTE BY
- user instance timeout
- sp_dropalias
- COMPUTE
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 27eb70cb687553b11fefae423a7544609836c5c8
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357027"
---
# <a name="discontinued-database-engine-functionality-in-sql-server-2014"></a>Funzionalità del Motore di database non più utilizzate in SQL Server 2014
  In questo argomento vengono descritte le funzionalità di [!INCLUDE[ssDE](../includes/ssde-md.md)] che non sono più disponibili in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a>Funzionalità non più disponibili in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Nella tabella seguente vengono elencate le funzionalità che sono state rimosse in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
|Category|Funzionalità non più disponibile|Sostituzione|  
|--------------|--------------------------|-----------------|  
|Livello di compatibilità|Livello di compatibilità 90|I database devono essere impostati almeno sul livello di compatibilità 100. Quando un database con un livello di compatibilità minore di 100 viene aggiornato a [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], durante l'operazione il livello di compatibilità del database viene impostato su 100.|  
  
## <a name="discontinued-features-in-includesssql11includessssql11-mdmd"></a>Funzionalità non più disponibili in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 Nella tabella seguente vengono elencate le funzionalità che sono state rimosse in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
|Category|Funzionalità non più disponibile|Sostituzione|  
|--------------|--------------------------|-----------------|  
|Backup e ripristino|**BACKUP {DATABASE &#124; LOG} WITH PASSWORD** e **BACKUP {DATABASE &#124; LOG} WITH MEDIAPASSWORD** non sono più disponibili. **RESTORE {DATABASE &#124; LOG} con [MEDIA] PASSWORD**continua a essere deprecata.|None|  
|Backup e ripristino|**RESTORE {DATABASE &AMP;#124; LOG}... WITH DBO_ONLY**|**RESTORE {DATABASE &AMP;#124; LOG}...... CON RESTRICTED_USER**|  
|Livello di compatibilità|livello di compatibilità 80|I database devono essere impostati almeno sul livello di compatibilità 90.|  
|Opzioni di configurazione|`sp_configure 'user instance timeout'` e `'user instances enabled'`|Utilizzare la funzionalità di database locale. Per altre informazioni, vedere [utilità SqlLocalDB](../tools/sqllocaldb-utility.md)|  
|Protocolli di connessione|Il supporto per il protocollo VIA è obsoleto.|In alternativa, utilizzare TCP.|  
|Oggetti di database|Clausola `WITH APPEND` sui trigger|Ricreare l'intero trigger.|  
|Opzioni di database|`sp_dboption`|`ALTER DATABASE`|  
|Posta elettronica|SQL Mail|Usare la posta elettronica database. Per altre informazioni, vedere [posta elettronica Database](../relational-databases/database-mail/database-mail.md) e [Use Database Mail Instead of SQL Mail](../relational-databases/policy-based-management/use-database-mail-instead-of-sql-mail.md).|  
|Gestione della memoria|Estensioni AWE (Address Windowing Extensions) a 32 bit e supporto per l'aggiunta della memoria a caldo a 32 bit.|Utilizzare un sistema operativo a 64 bit.|  
|Metadati|`DATABASEPROPERTY`|`DATABASEPROPERTYEX`|  
|Programmabilità|SQL Server DMO (SQL-Distributed Management Objects)|Oggetti SMO (SQL Server Management Objects)|  
|Hint per la query|Hint `FASTFIRSTROW`|`OPTION (FAST` *n* `)`.|  
|Server remoti|La possibilità per gli utenti di creare nuovi server remoti tramite `sp_addserver` non è più utilizzata. Rimane disponibile `sp_addserver` con l'opzione 'locale'. È possibile utilizzare i server remoti mantenuti durante l'aggiornamento o creati dalla replica.|Sostituire i server remoti utilizzando server collegati.|  
|Sicurezza|`sp_dropalias`|Sostituire gli alias con una combinazione di account utente e ruoli del database. Usare `sp_dropalias` per rimuovere gli alias in database aggiornati.|  
|Sicurezza|Il parametro della versione di **PWDCOMPARE** che rappresenta un valore di un account di accesso antecedente a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 non è più disponibile.|None|  
|Programmazione con Service Broker in SMO|Il **Microsoft.SqlServer.Management.Smo.Broker.BrokerPriority** classe non implementa il **Microsoft.SqlServer.Management.Smo.IObjectPermission** interfaccia.||  
|Opzioni SET|`SET DISABLE_DEF_CNST_CHK`|Nessuna.|  
|Tabelle di sistema|sys.database_principal_aliases|Usare ruoli anziché alias.|  
|Transact-SQL|Il parametro `RAISERROR` nel formato `RAISERROR integer 'string'` non è più utilizzato.|Riscrivere l'istruzione utilizzando l'oggetto corrente **RAISERROR**  sintassi.|  
|Sintassi Transact-SQL|`COMPUTE / COMPUTE BY`|Utilizzare `ROLLUP`.|  
|Sintassi Transact-SQL|Sfrutta **\* =** e **=\***|Utilizzare la sintassi di join ANSI. Per altre informazioni, vedere [da (Transact-SQL).](https://msdn.microsoft.com/library/ms177634\(SQL.105\).aspx)|  
|XEvents|databases_data_file_size_changed, databases_log_file_size_changed<br /><br /> eventdatabases_log_file_used_size_changed<br /><br /> locks_lock_timeouts_greater_than_0<br /><br /> locks_lock_timeouts|Sostituito dal database_file_size_change event, database_file_size_change<br /><br /> database_file_size_change event<br /><br /> lock_timeout_greater_than_0<br /><br /> lock_timeout|  
  
 **Modifiche XEvent aggiuntive**  
  
 **resource_monitor_ring_buffer_record**:  
  
-   Campi rimossi: single_pages_kb, multiple_pages_kb  
  
-   Campi aggiunti: target_kb, pages_kb  
  
 **memory_node_oom_ring_buffer_recorded**:  
  
-   Campi rimossi: single_pages_kb, multiple_pages_kb  
  
-   Campi aggiunti: target_kb, pages_kb  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità del Motore di database deprecate in SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
