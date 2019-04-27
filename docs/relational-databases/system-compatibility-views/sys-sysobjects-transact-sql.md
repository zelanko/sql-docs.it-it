---
title: sys.sysobjects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysobjects_TSQL
- sysobjects
- sysobjects_TSQL
- sys.sysobjects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysobjects compatibility view
- sysobjects system table
ms.assetid: 44fdc387-67b0-4139-8bf5-ed26cf640cd1
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e822f034ff4af30fc2d8c6992544b65aaea865e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632307"
---
# <a name="syssysobjects-transact-sql"></a>sys.sysobjects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contiene una riga per ogni oggetto creato all'interno di un database, ad esempio un vincolo, un valore predefinito, un log, una regola o una stored procedure.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|Nome oggetto|  
|id|**int**|Numero di identificazione dell'oggetto|  
|xtype|**char(2)**|Tipo di oggetto. Può trattarsi di uno dei tipi di oggetti seguenti:<br /><br /> AF = funzione di aggregazione (CLR)<br /><br /> C = vincolo CHECK<br /><br /> D = vincolo predefinito o DEFAULT<br /><br /> F = vincolo FOREIGN KEY<br /><br /> L = Log<br /><br /> FN = funzione scalare<br /><br /> FS = funzione scalare di assembly (CLR)<br /><br /> FT = funzione valutata a livello di tabella assembly (CLR)<br /><br /> IF = funzione della tabella inline<br /><br /> IT = tabella interna<br /><br /> P = stored procedure<br /><br /> PC = stored procedure di assembly (CLR)<br /><br /> PK = vincolo PRIMARY KEY (il tipo è K)<br /><br /> RF = stored procedure del filtro di replica<br /><br /> S = tabella di sistema<br /><br /> SN = sinonimo<br /><br /> SQ = coda di servizio<br /><br /> TA = trigger DML assembly (CLR)<br /><br /> TF = funzione tabella<br /><br /> TR = trigger DML SQL<br /><br /> TT = tipo tabella<br /><br /> U = tabella utente<br /><br /> UQ = vincolo UNIQUE (il tipo è K)<br /><br /> V = vista<br /><br /> X = stored procedure estesa|  
|uid|**smallint**|ID dello schema del proprietario dell'oggetto. Per i database aggiornati da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'ID dello schema corrisponde all'ID utente del proprietario. Causa un errore di overflow o restituisce NULL se il numero di utenti e ruoli è maggiore di 32.767.<br /><br /> **\*\* Importanti \* \***  se si usa uno dei seguenti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istruzioni DDL, è necessario usare il [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) anziché Sys. sysobjects vista del catalogo.<br /><br /> CREATE &#124; ALTER &#124; DROP USER<br /><br /> CREATE &#124; ALTER &#124; DROP ROLE<br /><br /> CREARE &AMP;#124; ALTER &AMP;#124; DROP APPLICATION ROLE<br /><br /> CREATE SCHEMA<br /><br /> ALTER AUTHORIZATION ON OBJECT|  
|info|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|base_schema_ver|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|replinfo|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|parent_obj|**int**|Numero di identificazione dell'oggetto padre. Ad esempio, l'ID della tabella se si tratta di un trigger o di un vincolo.|  
|crdate|**datetime**|Data di creazione dell'oggetto.|  
|ftcatid|**smallint**|Identificatore del catalogo full-text per tutte le tabelle utente registrate per l'indicizzazione full-text. È 0 per le tabelle utente non registrate.|  
|schema_ver|**int**|Numero di versione incrementato in corrispondenza della modifica dello schema di una tabella. Restituisce sempre 0.|  
|stats_schema_ver|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|Tipo|**char(2)**|Tipo di oggetto. Il valore può essere uno dei seguenti:<br /><br /> AF = funzione di aggregazione (CLR)<br /><br /> C = vincolo CHECK<br /><br /> D = vincolo predefinito o DEFAULT<br /><br /> F = vincolo FOREIGN KEY<br /><br /> FN = funzione scalare<br /><br /> FS = funzione scalare di assembly (CLR)<br /><br /> FT = funzione valutata a livello di tabella assembly (CLR)IF = funzione della tabella inline<br /><br /> IT = tabella interna<br /><br /> K = vincolo PRIMARY KEY o UNIQUE<br /><br /> L = Log<br /><br /> P = stored procedure<br /><br /> PC = stored procedure di assembly (CLR)<br /><br /> R = regola<br /><br /> RF = stored procedure del filtro di replica<br /><br /> S = tabella di sistema<br /><br /> SN = sinonimo<br /><br /> SQ = coda di servizio<br /><br /> TA = trigger DML assembly (CLR)<br /><br /> TF = funzione tabella<br /><br /> TR = trigger DML SQL<br /><br /> TT = tipo tabella<br /><br /> U = tabella utente<br /><br /> V = vista<br /><br /> X = stored procedure estesa|  
|userstat|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|sysstat|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|indexdel|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|refdate|**datetime**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|version|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|deltrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|instrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|updtrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|seltrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|category|**int**|Utilizzato per pubblicazioni, vincoli e colonne Identity.|  
|cache|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
