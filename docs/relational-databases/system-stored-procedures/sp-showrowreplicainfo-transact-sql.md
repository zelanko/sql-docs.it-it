---
title: sp_showrowreplicainfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_showrowreplicainfo_TSQL
- sp_showrowreplicainfo
helpviewer_keywords:
- sp_showrowreplicainfo
ms.assetid: 6a9dbc1a-e1e1-40c4-97cb-8164a2288f76
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0d009b05fea2a2c587f97dc4b2416588932ad0bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62447989"
---
# <a name="spshowrowreplicainfo-transact-sql"></a>sp_showrowreplicainfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza informazioni su una riga di una tabella utilizzata come articolo in repliche di tipo merge. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_showrowreplicainfo [ [ @ownername = ] 'ownername' ]  
    [ , [ @tablename =] 'tablename' ]   
        , [ @rowguid =] rowguid   
    [ , [ @show = ] 'show' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @ownername = ] 'ownername'` È il nome del proprietario della tabella. *ownername* viene **sysname**, con un valore predefinito è NULL. Questo parametro risulta utile per differenziare le tabelle quando un database contiene più tabelle aventi lo stesso nome ma appartenenti a proprietari diversi.  
  
`[ @tablename = ] 'tablename'` È il nome della tabella che contiene la riga per il quale vengono restituite le informazioni. *TableName* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @rowguid = ] rowguid` È l'identificatore univoco della riga. *ROWGUID* viene **uniqueidentifier**, non prevede alcun valore predefinito.  
  
`[ @show = ] 'show'` Determina la quantità di informazioni da restituire nel set di risultati. *mostrare* viene **nvarchar(20)** con valore predefinito è BOTH. Se **riga**, viene restituiti solo le informazioni sulla versione di riga. Se **colonne**, viene restituiti solo le informazioni sulla versione di colonna. Se **entrambi**, di righe e vengono restituite informazioni di colonna.  
  
## <a name="result-sets-for-row-information"></a>Set di risultati per informazioni sulla riga  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|Nome del server che include il database in cui è stata immessa la voce sulla versione di riga.|  
|**db_name**|**sysname**|Nome del database in cui è stata immessa la voce.|  
|**db_nickname**|**binary(6)**|Nome alternativo del database in cui è stata immessa la voce.|  
|**version**|**int**|Versione della voce.|  
|**current_state**|**nvarchar(9)**|Restituisce informazioni sullo stato corrente della riga.<br /><br /> **y** -i dati di riga rappresentano lo stato corrente della riga.<br /><br /> **n** -dati di riga non rappresentano lo stato corrente della riga.<br /><br /> **\<n/a >** : non applicabile.<br /><br /> **\<sconosciuto >** -non è possibile determinare lo stato corrente.|  
|**rowversion_table**|**nchar(17)**|Indica se le versioni delle righe vengono archiviate nel [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) tabella o nella [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) tabella.|  
|**comment**|**nvarchar(255)**|Informazioni aggiuntive relative alla voce sulla versione di riga. Questo campo è in genere vuoto.|  
  
## <a name="result-sets-for-column-information"></a>Set di risultati per informazioni sulla colonna  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|Nome del server che include il database in cui è stata immessa la voce sulla versione di colonna.|  
|**db_name**|**sysname**|Nome del database in cui è stata immessa la voce.|  
|**db_nickname**|**binary(6)**|Nome alternativo del database in cui è stata immessa la voce.|  
|**version**|**int**|Versione della voce.|  
|**colname**|**sysname**|Nome della colonna di articolo rappresentata dalla voce sulla versione di colonna.|  
|**comment**|**nvarchar(255)**|Informazioni aggiuntive relative alla voce sulla versione di colonna. Questo campo è in genere vuoto.|  
  
## <a name="result-set-for-both"></a>Set di risultati per informazioni su riga e colonna  
 Se il valore **entrambe** scelto per *mostrano*, viene restituita sia la riga e colonna set di risultati.  
  
## <a name="remarks"></a>Note  
 **sp_showrowreplicainfo** viene utilizzata nella replica di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 **sp_showrowreplicainfo** può essere eseguita solo dai membri del **db_owner** ruolo predefinito del database nel database di pubblicazione o dai membri dell'elenco di accesso (PAL) nel database di pubblicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Rilevare e risolvere i conflitti tra repliche di tipo Merge](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
