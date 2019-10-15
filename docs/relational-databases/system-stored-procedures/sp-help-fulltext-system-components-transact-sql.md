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
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 98e360887d63db59e1e61bf5c52928e9626b0f39
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304888"
---
# <a name="sp_help_fulltext_system_components-transact-sql"></a>sp_help_fulltext_system_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Restituisce informazioni per i word breaker, il filtro e i gestori di protocollo registrati. **sp_help_fulltext_system_components** restituisce inoltre un elenco degli identificatori dei database e dei cataloghi full-text che hanno utilizzato il componente specificato.  
  
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
  
`[ @component_type = ] component_type` specifica il tipo di componente. *component_type* può essere uno dei seguenti:  
  
-   **wordbreaker**  
  
-   **filter**  
  
-   **gestore di protocollo**  
  
-   **fullpath**  
  
 Se viene specificato un percorso completo, è necessario specificare anche *param* con il percorso completo della dll del componente o viene restituito un messaggio di errore.  
  
`[ @param = ] param` a seconda del tipo di componente, questo è uno dei seguenti: un identificatore delle impostazioni locali (LCID), l'estensione di file con prefisso ".", il nome completo del componente del gestore di protocollo o il percorso completo della DLL del componente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Il set di risultati seguente viene restituito per i componenti di sistema.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**componenttype**|**sysname**|Tipo di componente. I tipi validi sono:<br /><br /> filter<br /><br /> protocol handler<br /><br /> wordbreaker|  
|**componentname**|**sysname**|Nome del componente.|  
|**clsid**|**uniqueidentifier**|Identificatore della classe del componente.|  
|**fullpath**|**nvarchar(256)**|Percorso della posizione del componente.<br /><br /> NULL = il chiamante non è un membro del ruolo predefinito del server **serveradmin** .|  
|**version**|**nvarchar(30)**|Versione del componente.|  
|**manufacturer**|**sysname**|Nome del produttore del componente.|  
  
 Il set di risultati seguente viene restituito solo se esistono uno o più cataloghi full-text che usano *component_type*.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**dbid**|**int**|ID del database.|  
|**ftcatid**|**int**|ID del catalogo full-text.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo **public** ; Tuttavia, gli utenti possono visualizzare solo le informazioni sui cataloghi full-text per i quali dispongono dell'autorizzazione VIEW DEFINITION. Solo i membri del ruolo predefinito del server **serveradmin** possono visualizzare i valori nella colonna **FullPath** .  
  
## <a name="remarks"></a>Note  
 Questo metodo è di particolare importanza durante la preparazione per un aggiornamento. Eseguire la stored procedure all'interno di un particolare database e utilizzare l'output per determinare se l'aggiornamento avrà effetti su un particolare catalogo.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-all-full-text-system-components"></a>R. Elenco di tutti i componenti di sistema full-text  
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
 Nell'esempio seguente viene elencato il word breaker per la lingua turca (LCID = 1055) se è stato installato nel sistema e registrato sull'istanza del servizio. In questo esempio vengono specificati i nomi dei parametri, **\@component_type** e **\@param**.  
  
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
 [Visualizzare o modificare i Word breaker e i filtri registrati](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)   
 [Configurazione e gestione di word breaker e stemmer per la ricerca](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurazione e gestione di filtri per la ricerca](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [Stored procedure &#40;per la ricerca full-text e la ricerca semantica Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
