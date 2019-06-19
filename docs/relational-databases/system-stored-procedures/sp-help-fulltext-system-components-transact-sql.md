---
title: sp_help_fulltext_system_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_components_TSQL
- sp_help_fulltext_components
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_system_components
ms.assetid: ac1fc7a0-7f46-4a12-8c5c-8d378226a8ce
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b8090ea1080fa7528d3a8297e14760190e8aadfe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65980250"
---
# <a name="sphelpfulltextsystemcomponents-transact-sql"></a>sp_help_fulltext_system_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Restituisce informazioni per i word breaker, il filtro e i gestori di protocollo registrati. **sp_help_fulltext_system_components** restituisce inoltre un elenco degli identificatori dei database e cataloghi full-text che hanno utilizzato il componente specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_fulltext_system_components   
         { 'all'| [ @component_type = ] 'component_type' }  
    , [ @param = ] 'param'  
```  
  
## <a name="arguments"></a>Argomenti  
 'all'  
 Restituisce informazioni per tutti i componenti full-text.  
  
`[ @component_type = ] component_type` Specifica il tipo di componente. *component_type* può essere uno dei seguenti:  
  
-   **wordbreaker**  
  
-   **filter**  
  
-   **gestore di protocollo**  
  
-   **fullpath**  
  
 Se viene specificato un percorso completo, *param* deve essere specificata anche con il percorso completo della DLL, del componente o un messaggio di errore viene restituito.  
  
`[ @param = ] param` A seconda del tipo di componente, questa è una delle operazioni seguenti: un identificatore delle impostazioni locali (LCID), l'estensione del file con "." prefisso, il nome completo del componente del gestore del protocollo o il percorso completo della DLL del componente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Il set di risultati seguente viene restituito per i componenti di sistema.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**componenttype**|**sysname**|Tipo di componente. I tipi validi sono:<br /><br /> filter<br /><br /> protocol handler<br /><br /> wordbreaker|  
|**componentname**|**sysname**|Nome del componente.|  
|**clsid**|**uniqueidentifier**|Identificatore della classe del componente.|  
|**fullpath**|**nvarchar(256)**|Percorso della posizione del componente.<br /><br /> NULL = il chiamante non è membro del **serveradmin** ruolo predefinito del server.|  
|**version**|**nvarchar(30)**|Versione del componente.|  
|**manufacturer**|**sysname**|Nome del produttore del componente.|  
  
 Il set di risultati seguente viene restituito solo se uno o più di un catalogo full-text esistente che usa *component_type*.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**dbid**|**int**|ID del database.|  
|**ftcatid**|**int**|ID del catalogo full-text.|  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **pubblica** ruolo; tuttavia, gli utenti possono solo visualizzare informazioni sui cataloghi full-text per cui dispongono dell'autorizzazione VIEW DEFINITION. Solo i membri del **serveradmin** ruolo predefinito del server è possibile visualizzare i valori nel **fullpath** colonna.  
  
## <a name="remarks"></a>Note  
 Questo metodo è di particolare importanza durante la preparazione per un aggiornamento. Eseguire la stored procedure all'interno di un particolare database e utilizzare l'output per determinare se l'aggiornamento avrà effetti su un particolare catalogo.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-all-full-text-system-components"></a>A. Elenco di tutti i componenti di sistema full-text  
 Nell'esempio seguente vengono elencati tutti i componenti di sistema full-text registrati sull'istanza server.  
  
```  
EXEC sp_help_fulltext_system_components 'all';  
GO  
```  
  
### <a name="b-listing-word-breakers"></a>B. Elenco di word breaker  
 Nell'esempio seguente vengono elencati tutti i word breaker registrati sull'istanza del servizio.  
  
```  
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```  
  
### <a name="c-determining-whether-a-specific-word-breaker-is-registered"></a>C. Determinazione della registrazione di un word breaker specifico  
 Nell'esempio seguente viene elencato il word breaker per la lingua turca (LCID = 1055) se è stato installato nel sistema e registrato sull'istanza del servizio. Questo esempio i nomi dei parametri, si specifica **@component_type** e **@param** .  
  
```  
EXEC sp_help_fulltext_system_components @component_type = 'wordbreaker', @param = 1055;  
GO  
```  
  
 Per impostazione predefinita, questo word breaker non è installato, pertanto il set di risultati è vuoto.  
  
### <a name="d-determining-whether-a-specific-filter-has-been-registered"></a>D. Determinazione della registrazione di un filtro specifico  
 Nell'esempio seguente viene elencato il filtro per il componente xdoc se è stato manualmente installato nel sistema e registrato sull'istanza del server.  
  
```  
EXEC sp_help_fulltext_system_components 'filter', '.xdoc';  
GO  
```  
  
 Per impostazione predefinita, questo filtro non è installato, pertanto il set di risultati è vuoto.  
  
### <a name="e-listing-a-specific-dll-file"></a>E. Elenco di un file dll specifico  
 Nell'esempio seguente viene elencato un file con estensione ddl specifico, `nlhtml.dll`, installato per impostazione predefinita.  
  
```  
EXEC sp_help_fulltext_system_components 'fullpath',   
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\nlhtml.dll';  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzazione o modifica di Word breaker e filtri registrati](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)   
 [Configurazione e gestione di word breaker e stemmer per la ricerca](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurazione e gestione di filtri per la ricerca](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [Ricerca full-Text e semantica Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
