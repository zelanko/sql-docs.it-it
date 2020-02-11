---
title: Funzionalità di motore di database sospese in SQL Server 2014 | Microsoft Docs
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
ms.openlocfilehash: 2ebb9b4e3db7cf8f7a19fd582dceb0b19f5c47d0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67463459"
---
# <a name="discontinued-database-engine-functionality-in-sql-server-2014"></a>Funzionalità del Motore di database non più utilizzate in SQL Server 2014
  In questo argomento vengono descritte le funzionalità di [!INCLUDE[ssDE](../includes/ssde-md.md)] che non sono più disponibili in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="SQL14"></a>Funzionalità non più disponibili in[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Nella tabella seguente vengono elencate le funzionalità che sono state rimosse in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
|Category|Funzionalità non più disponibile|Sostituzione|  
|--------------|--------------------------|-----------------|  
|Livello di compatibilità|Livello di compatibilità 90|I database devono essere impostati almeno sul livello di compatibilità 100. Quando un database con un livello di compatibilità minore di 100 viene aggiornato a [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], durante l'operazione il livello di compatibilità del database viene impostato su 100.|  
  
## <a name="Denali"></a>Funzionalità non più disponibili in[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 Nella tabella seguente vengono elencate le funzionalità che sono state rimosse in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
|Category|Funzionalità non più disponibile|Sostituzione|  
|--------------|--------------------------|-----------------|  
|Backup e ripristino|Il **backup {database &#124; log} con password** e **backup {database &#124; log} con MEDIAPASSWORD** non è più disponibile. **RESTORE {DATABASE &#124; log} con [media] password**continua a essere deprecata.|nessuno|  
|Backup e ripristino|**RIPRISTINA {DATABASE &#124; LOG}... CON DBO_ONLY**|**RIPRISTINA {DATABASE &#124; LOG}...... CON RESTRICTED_USER**|  
|Livello di compatibilità|livello di compatibilità 80|I database devono essere impostati almeno sul livello di compatibilità 90.|  
|Opzioni di configurazione|`sp_configure 'user instance timeout'` e `'user instances enabled'`|Utilizzare la funzionalità di database locale. Per ulteriori informazioni, vedere [Utilità SqlLocalDB](../tools/sqllocaldb-utility.md)|  
|Protocolli di connessione|Il supporto per il protocollo VIA è obsoleto.|In alternativa, utilizzare TCP.|  
|Oggetti di database|Clausola `WITH APPEND` sui trigger|Ricreare l'intero trigger.|  
|Opzioni di database|`sp_dboption`|`ALTER DATABASE`|  
|Mail|SQL Mail|Usare la posta elettronica database. Per ulteriori informazioni, vedere [posta elettronica database](../relational-databases/database-mail/database-mail.md) e [utilizzare posta elettronica database anziché SQL Mail](../relational-databases/policy-based-management/use-database-mail-instead-of-sql-mail.md).|  
|Gestione della memoria|Estensioni AWE (Address Windowing Extensions) a 32 bit e supporto per l'aggiunta della memoria a caldo a 32 bit.|Utilizzare un sistema operativo a 64 bit.|  
|Metadati|`DATABASEPROPERTY`|`DATABASEPROPERTYEX`|  
|Programmabilità|SQL Server DMO (SQL-Distributed Management Objects)|Oggetti SMO (SQL Server Management Objects)|  
|Hint per la query|`FASTFIRSTROW`Suggerimento|`OPTION (FAST`*n* `)`.|  
|Server remoti|La possibilità per gli utenti di creare nuovi server remoti tramite `sp_addserver` non è più utilizzata. Rimane disponibile `sp_addserver` con l'opzione 'locale'. È possibile utilizzare i server remoti mantenuti durante l'aggiornamento o creati dalla replica.|Sostituire i server remoti utilizzando server collegati.|  
|Security|`sp_dropalias`|Sostituire gli alias con una combinazione di account utente e ruoli del database. Usare `sp_dropalias` per rimuovere gli alias in database aggiornati.|  
|Security|Il parametro della versione di **PWDCOMPARE** che rappresenta un valore di un account [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] di accesso precedente a 2000 non è più disponibile.|nessuno|  
|Programmazione con Service Broker in SMO|La classe **Microsoft. SqlServer. Management. Smo. Broker. BrokerPriority** non implementa più l'interfaccia **Microsoft. SqlServer. Management. Smo. IObjectPermission** .||  
|Opzioni SET|`SET DISABLE_DEF_CNST_CHK`|No.|  
|Tabelle di sistema|sys.database_principal_aliases|Usare ruoli anziché alias.|  
|Transact-SQL|Il parametro `RAISERROR` nel formato `RAISERROR integer 'string'` non è più utilizzato.|Riscrivere l'istruzione utilizzando la sintassi **RAISERROR (...)** corrente.|  
|Sintassi Transact-SQL|`COMPUTE / COMPUTE BY`|Utilizzare `ROLLUP`.|  
|Sintassi Transact-SQL|Utilizzo di ** \* ** e **=&#42;**|Utilizzare la sintassi di join ANSI. Per ulteriori informazioni, vedere [from (Transact-SQL).](https://msdn.microsoft.com/library/ms177634\(SQL.105\).aspx)|  
|XEvents|databases_data_file_size_changed, databases_log_file_size_changed<br /><br /> eventdatabases_log_file_used_size_changed<br /><br /> locks_lock_timeouts_greater_than_0<br /><br /> locks_lock_timeouts|Sostituito da database_file_size_change event, database_file_size_change<br /><br /> database_file_size_change event<br /><br /> lock_timeout_greater_than_0<br /><br /> lock_timeout|  
  
 **Modifiche XEvent aggiuntive**  
  
 **resource_monitor_ring_buffer_record**:  
  
-   Campi rimossi: single_pages_kb, multiple_pages_kb  
  
-   Campi aggiunti: target_kb, pages_kb  
  
 **memory_node_oom_ring_buffer_recorded**:  
  
-   Campi rimossi: single_pages_kb, multiple_pages_kb  
  
-   Campi aggiunti: target_kb, pages_kb  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità del Motore di database deprecate in SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)  
  
  
