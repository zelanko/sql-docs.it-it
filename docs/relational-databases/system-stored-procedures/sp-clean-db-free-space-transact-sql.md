---
title: sp_clean_db_free_space (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_clean_db_free_space_TSQL
- sp_clean_db_free_space
dev_langs:
- TSQL
helpviewer_keywords:
- sp_clean_db_free_space
- ghost records
ms.assetid: faa96f7e-be92-47b1-8bc5-4dbba5331655
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1622f7cd1d14e83d76ef9cebc716b2743e288395
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771294"
---
# <a name="sp_clean_db_free_space-transact-sql"></a>sp_clean_db_free_space (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Rimuove le informazioni residue lasciate nelle pagine del database a causa delle routine di modifica dei dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. sp_clean_db_free_space pulisce tutte le pagine in tutti i file del database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_clean_db_free_space   
[ @dbname ] = 'database_name'   
[ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @dbname =]'*database_name*'  
 Nome del database da pulire. *dbname* è di **tipo sysname** e non può essere null.  
  
 [ @cleaning_delay =]'*delay_in_seconds*'  
 Specifica un intervallo di ritardo tra le pulizie delle pagine per ridurre l'impatto sul sistema di I/O. *delay_in_seconds* è di **tipo int** e il valore predefinito è 0.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="remarks"></a>Osservazioni  
 Le operazioni di aggiornamento o le operazioni di eliminazione da una tabella che provocano lo spostamento di una riga consentono di liberare immediatamente spazio in una pagina poiché rimuovono i riferimenti alla riga specifica. In alcune circostanze, tuttavia, la riga può rimanere fisicamente nella pagina di dati come record fantasma. I record fantasma vengono rimossi periodicamente da un processo in background. Questi dati residui non vengono restituiti dal [!INCLUDE[ssDE](../../includes/ssde-md.md)] in risposta alle query. In ambienti in cui la sicurezza fisica dei file di dati o di backup non sia sufficiente, è tuttavia possibile utilizzare sp_clean_db_free_space per eliminare tali record fantasma.  
  
 La quantità di tempo necessaria per eseguire sp_clean_db_free_space dipende dalle dimensioni del file, dallo spazio libero disponibile e dalla capacità del disco. Poiché l'esecuzione di sp_clean_db_free_space può influire in modo significativo sulle attività di I/O, è consigliabile eseguire questa procedura in orario diverso da quello lavorativo.  
  
 Prima di eseguire sp_clean_db_free_space, è opportuno creare un backup completo del database.  
  
 Il [sp_clean_db_file_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md) correlato stored procedure può pulire un singolo file.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo del database db_owner.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono eliminate tutte le informazioni residue dal database `AdventureWorks2012`.  
  
```  
USE master;  
GO  
EXEC sp_clean_db_free_space   
@dbname = N'AdventureWorks2012' ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di motore di database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)
 <br>[Guida al processo di pulizia fantasma](../ghost-record-cleanup-process-guide.md) 
  
  
