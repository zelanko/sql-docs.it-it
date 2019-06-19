---
title: sp_help (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help
- sp_help_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help
ms.assetid: 913cd5d4-39a3-4a4b-a926-75ed32878884
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f5e514307e1427cea0ea1bb4d75e7bf0806fd516
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63017756"
---
# <a name="sphelp-transact-sql"></a>sp_help (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Vengono fornite informazioni sull'oggetto di database (tutti gli oggetti elencati nel **Sys. sysobjects** vista di compatibilità), un tipo di dati definito dall'utente o un tipo di dati.  
  
 
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help [ [ @objname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @objname = ] 'name'` È il nome di qualsiasi oggetto, in **sysobjects** o digitare qualsiasi dato definito dall'utente il **systypes** tabella. *nome* viene **nvarchar (** 776 **)** , con un valore predefinito è NULL. I nomi di database non sono validi.  I nomi in due o tre parti devono essere delimitati, ad esempio 'Person.AddressType' o [Person.AddressType].   
   
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 I set di risultati restituiti variano a seconda che *nome* è specificata, quando viene specificato e quale oggetto di database.  
  
1.  Se **sp_help** viene eseguita senza alcun argomento, vengono restituite le informazioni di riepilogo degli oggetti di tutti i tipi presenti nel database corrente.  
  
    |Nome colonna|Tipo di dati|Descrizione|  
    |-----------------|---------------|-----------------|  
    |**Name**|**nvarchar(** 128 **)**|Nome oggetto|  
    |**Proprietario**|**nvarchar(** 128 **)**|Proprietario dell'oggetto. Si tratta dell'entità di database proprietaria dell'oggetto. Corrispondente per impostazione predefinita al proprietario dello schema contenente l'oggetto.|  
    |**Object_type**|**nvarchar(** 31 **)**|Tipo oggetto|  
  
2.  Se *name* è un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati o tipo di dati definito dall'utente **sp_help** restituisce questo set di risultati.  
  
    |Nome colonna|Tipo di dati|Descrizione|  
    |-----------------|---------------|-----------------|  
    |**Type_name**|**nvarchar(** 128 **)**|Nome del tipo di dati.|  
    |**Storage_type**|**nvarchar(** 128 **)**|Nome del tipo di archiviazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
    |**Lunghezza**|**smallint**|Lunghezza fisica del tipo di dati in byte.|  
    |**Prec**|**int**|Precisione, ovvero il numero totale di cifre.|  
    |**Scala**|**int**|Numero di cifre a destra del separatore decimale.|  
    |**Ammette i valori Null**|**varchar(** 35 **)**|Indica se i valori NULL sono consentiti: Sì o No.|  
    |**Default_name**|**nvarchar(** 128 **)**|Nome del valore predefinito associato al tipo di dati specificato.<br /><br /> NULL = Non è associata alcuna regola predefinita.|  
    |**Nome_regola**|**nvarchar(** 128 **)**|Nome di una regola associata al tipo di dati specificato.<br /><br /> NULL = Non è associata alcuna regola predefinita.|  
    |**Regole di confronto**|**sysname**|Regole di confronto per il tipo di dati. Per i tipi di dati non carattere, è NULL.|  
  
3.  Se *name* è qualsiasi oggetto di database diverso da un tipo di dati **sp_help** restituisce questo risultato del set di risultati di set e anche altri, in base al tipo di oggetto specificato.  
  
    |Nome colonna|Tipo di dati|Descrizione|  
    |-----------------|---------------|-----------------|  
    |**Name**|**nvarchar(** 128 **)**|Nome tabella|  
    |**Proprietario**|**nvarchar(** 128 **)**|Proprietario della tabella.|  
    |**Tipo**|**nvarchar(** 31 **)**|Tipo di tabella.|  
    |**Created_datetime**|**datetime**|Data di creazione della tabella.|  
  
     A seconda dell'oggetto di database specificato, **sp_help** restituisce set di risultati aggiuntivi.  
  
     Se *name* è una tabella di sistema, una vista o una tabella utente **sp_help** restituisce i set di risultati seguente. Per le viste non viene tuttavia restituito il set di risultati relativo alla posizione del file di dati in un filegroup.  
  
    -   Set di risultati aggiuntivo restituito per gli oggetti colonna  
  
        |Nome colonna|Tipo di dati|Descrizione|  
        |-----------------|---------------|-----------------|  
        |**Column_name**|**nvarchar(** 128 **)**|Nome colonna.|  
        |**Tipo**|**nvarchar(** 128 **)**|Tipo di dati della colonna.|  
        |**Computed**|**varchar(** 35 **)**|Indica se i valori nella colonna sono calcolati: Sì o No.|  
        |**Lunghezza**|**int**|Lunghezza della colonna in byte.<br /><br /> Nota: Se il tipo di dati di colonna è un tipo di valori di grandi dimensioni (**varchar (max)** , **nvarchar (max)** , **varbinary (max)** , oppure **xml**), il valore verrà vengono visualizzati come -1.|  
        |**Prec**|**char(** 5 **)**|Precisione della colonna.|  
        |**Scala**|**char(** 5 **)**|Scala della colonna.|  
        |**Ammette i valori Null**|**varchar(** 35 **)**|Indica se sono consentiti valori NULL nella colonna: Sì o No.|  
        |**TrimTrailingBlanks**|**varchar(** 35 **)**|Specifica se gli spazi vuoti finali devono essere eliminati o meno. Restituisce Yes o No.|  
        |**FixedLenNullInSource**|**varchar(** 35 **)**|Disponibile solo per compatibilità con le versioni precedenti.|  
        |**Regole di confronto**|**sysname**|Regole di confronto della colonna. NULL per i tipi di dati non carattere.|  
  
    -   Set di risultati aggiuntivo restituito per le colonne Identity  
  
        |Nome colonna|Tipo di dati|Descrizione|  
        |-----------------|---------------|-----------------|  
        |**Identità**|**nvarchar(** 128 **)**|Nome della colonna il cui tipo di dati viene dichiarato come Identity.|  
        |**Valore di inizializzazione**|**numeric**|Valore iniziale per la colonna Identity.|  
        |**Incremento valore Identity**|**numeric**|Incremento da utilizzare per i valori della colonna.|  
        |**Non applicare in processi di replica**|**int**|La proprietà IDENTITY non viene applicata quando un account di accesso di replica, ad esempio **sqlrepl**, inserisce dati nella tabella:<br /><br /> 1 = True<br /><br /> 0 = False|  
  
    -   Set di risultati aggiuntivo restituito per le colonne  
  
        |Nome colonna|Tipo di dati|Descrizione|  
        |-----------------|---------------|-----------------|  
        |**RowGuidCol**|**sysname**|Nome della colonna che include il valore GUID.|  
  
    -   Set di risultati aggiuntivo restituito per i filegroup  
  
        |Nome colonna|Tipo di dati|Descrizione|  
        |-----------------|---------------|-----------------|  
        |**Data_located_on_filegroup**|**nvarchar(** 128 **)**|Filegroup in cui si trovano i dati: Database primario, secondario o Log delle transazioni.|  
  
    -   Set di risultati aggiuntivo restituito per gli indici:  
  
        |Nome colonna|Tipo di dati|Descrizione|  
        |-----------------|---------------|-----------------|  
        |**index_name**|**sysname**|Nome dell'indice.|  
        |**Index_description**|**varchar(** 210 **)**|Descrizione dell'indice.|  
        |**index_keys**|**nvarchar(** 2078 **)**|Nomi delle colonne in cui viene compilato l'indice. Restituisce NULL per gli indici columnstore con ottimizzazione per la memoria xVelocity.|  
  
    -   Set di risultati aggiuntivo restituito per i vincoli:  
  
        |Nome colonna|Tipo di dati|Descrizione|  
        |-----------------|---------------|-----------------|  
        |**constraint_type**|**nvarchar(** 146 **)**|Tipo di vincolo.|  
        |**constraint_name**|**nvarchar(** 128 **)**|Nome del vincolo.|  
        |**delete_action**|**nvarchar(** 9 **)**|Indica se l'azione di eliminazione è: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT o n/d.<br /><br /> Valido solo per i vincoli FOREIGN KEY.|  
        |**update_action**|**nvarchar(** 9 **)**|Indica se l'azione di aggiornamento è: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT o n/d.<br /><br /> Valido solo per i vincoli FOREIGN KEY.|  
        |**status_enabled**|**varchar(** 8 **)**|Indica se il vincolo è abilitato: Enabled, Disabled o n/d.<br /><br /> Valido solo per i vincoli CHECK e FOREIGN KEY.|  
        |**status_for_replication**|**varchar(** 19 **)**|Indica se il vincolo è relativo alla replica.<br /><br /> Valido solo per i vincoli CHECK e FOREIGN KEY.|  
        |**constraint_keys**|**nvarchar(** 2078 **)**|Nomi delle colonne che formano il vincolo o, nel caso di valori predefiniti e regole, il testo che definisce il valore predefinito o la regola.|  
  
    -   Set di risultati aggiuntivo restituito per gli oggetti di riferimento  
  
        |Nome colonna|Tipo di dati|Descrizione|  
        |-----------------|---------------|-----------------|  
        |**Fa riferimento alla tabella**|**nvarchar(** 516 **)**|Identifica gli oggetti di database che fanno riferimento alla tabella.|  
  
    -   Set di risultati aggiuntivo restituito per stored procedure, funzioni o stored procedure estese  
  
        |Nome colonna|Tipo di dati|Descrizione|  
        |-----------------|---------------|-----------------|  
        |**Parameter_name**|**nvarchar(** 128 **)**|Nome del parametro della stored procedure.|  
        |**Tipo**|**nvarchar(** 128 **)**|Tipo di dati del parametro della stored procedure.|  
        |**Lunghezza**|**smallint**|Capacità massima di archiviazione fisica in byte.|  
        |**Prec**|**int**|Precisione, ovvero il numero totale di cifre.|  
        |**Scala**|**int**|Numero di cifre a destra del separatore decimale.|  
        |**Param_order**|**smallint**|Ordine del parametro.|  
  
## <a name="remarks"></a>Note  
 Il **sp_help** eseguita la ricerca di un oggetto nel database corrente.  
  
 Quando *name* non viene specificato, **sp_help** gli elenchi di nomi, i proprietari e i tipi di oggetto per tutti gli oggetti nel database corrente dell'oggetto. **sp_helptrigger** vengono fornite informazioni sui trigger.  
  
 **sp_help** espone solo le colonne di indice ordinabili, pertanto non espone informazioni sugli indici XML o spaziali.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo **public** . L'utente deve avere almeno un'autorizzazione *objname*. Per visualizzare chiavi del vincolo di colonna, impostazioni predefinite o regole, è necessario disporre dell'autorizzazione VIEW DEFINITION per la tabella.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-information-about-all-objects"></a>A. Restituzione di informazioni su tutti gli oggetti  
 Nell'esempio seguente vengono elencate le informazioni su ogni oggetto incluso nel database `master`.  
  
```  
USE master;  
GO  
EXEC sp_help;  
GO  
```  
  
### <a name="b-returning-information-about-a-single-object"></a>B. Restituzione di informazioni su un solo oggetto  
 Nell'esempio seguente vengono visualizzate informazioni sulla tabella `Person`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help 'Person.Person';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpindex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sysobjects &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)  
  
  
