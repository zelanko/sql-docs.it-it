---
title: sp_fulltext_catalog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_catalog_TSQL
- sp_fulltext_catalog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_catalog
ms.assetid: e49b98e4-d1f1-42b2-b16f-eb2fc7aa1cf5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c219189fbd10ca91d91f3f5a527f88c1804d6d84
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124367"
---
# <a name="spfulltextcatalog-transact-sql"></a>sp_fulltext_catalog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Consente di creare ed eliminare un catalogo full-text e di avviare e arrestare l'azione di indicizzazione per un catalogo. È possibile creare più cataloghi full-text per ogni database.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Uso [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md), [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md), e [DROP FULLTEXT CATALOG](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_fulltext_catalog [ @ftcat= ] 'fulltext_catalog_name' ,   
     [ @action= ] 'action'   
     [ , [ @path= ] 'root_directory' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @ftcat = ] 'fulltext_catalog_name'` È il nome del catalogo full-text. I nomi dei cataloghi devono essere univoci per ogni database. *fulltext_catalog_name* viene **sysname**.  
  
`[ @action = ] 'action'` È l'azione da eseguire. *azione* viene **varchar (20)** , i possibili valori sono i seguenti.  
  
> [!NOTE]  
>  I cataloghi full-text possono essere creati, eliminati e modificati in base alle necessità. Evitare tuttavia di modificare contemporaneamente più cataloghi a livello di schema. È possibile eseguire queste azioni usando il **sp_fulltext_table** stored procedure, che è il metodo consigliato.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Creare**|Crea un catalogo full-text vuoto, una novità nel file system e aggiunge una riga corrispondente in **sysfulltextcatalogs** con il *fulltext_catalog_name* e *root_directory*, Se presente, i valori. *fulltext_catalog_name* deve essere univoco all'interno del database.|  
|**Drop**|Eliminazioni *fulltext_catalog_name* rimuoverlo dal file system ed eliminando la riga associata nella **sysfulltextcatalogs**. Questa azione non viene completata se nel catalogo sono inclusi indici per una o più tabelle. **sp_fulltext_table** »*table_name*', 'drop' deve essere eseguita per eliminare le tabelle dal catalogo.<br /><br /> Se il catalogo non esiste, viene visualizzato un errore.|  
|**start_incremental**|Avvia un popolamento incrementale per *fulltext_catalog_name*. Se il catalogo non esiste, viene visualizzato un errore. Se è già attivo il popolamento di un indice full-text, viene visualizzato un avviso e il popolamento non viene eseguito. Popolamento incrementale vengono recuperate solo le righe modificate per l'indicizzazione full-text, purché sia disponibile un' **timestamp** le colonne presenti nella tabella full-text indicizzate.|  
|**start_full**|Avvia un popolamento completo per *fulltext_catalog_name*. Per l'indicizzazione full-text viene recuperata ogni riga di ogni tabella associata al catalogo, anche se è già stata indicizzata.|  
|**Arresta**|Arresta un popolamento dell'indice per *fulltext_catalog_name*. Se il catalogo non esiste, viene visualizzato un errore. Se il popolamento è già stato arrestato, non viene visualizzato alcun avviso.|  
|**Ricompilazione**|Consente di ricompilare *fulltext_catalog_name*. Quando viene ricompilato un catalogo, il catalogo esistente viene eliminato e al suo posto viene creato un nuovo catalogo. Tutte le tabelle con riferimenti di indicizzazione full-text vengono associate al nuovo catalogo. La ricompilazione reimposta i metadati full-text nelle tabelle di sistema del database.<br /><br /> Se il rilevamento delle modifiche è impostato su OFF, la ricompilazione non comporta il ripopolamento del catalogo full-text appena creato. In questo caso, per eseguire la ricompilazione, eseguire **sp_fulltext_catalog** con il **start_full** oppure **start_incremental** azione.|  
  
`[ @path = ] 'root_directory'` È la directory radice (non percorso fisico completo) per un **creare** azione. *root_directory* viene **nvarchar(100)** e ha un valore predefinito null, ovvero viene utilizzato il percorso predefinito specificato al momento dell'installazione. Si tratta della sottodirectory Ftdata della directory Mssql, ad esempio, C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\MSSQL\FTData. La directory radice specificata deve trovarsi in un'unità dello stesso computer, non deve corrispondere alla sola lettera di unità e non può essere un percorso relativo. Le unità di rete, le unità rimovibili, i dischi floppy e i percorsi in formato UNC non sono supportati. È necessario creare i cataloghi full-text in un'unità disco rigido locale associata a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **@path** è valido solo quando *azione* viene **creare**. Per le azioni diverse da **creare** (**arrestare**, **ricompilare**e così via), **@path** deve essere NULL o omesso.  
  
 Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un server virtuale in un cluster, la directory di catalogo specificata deve trovarsi in un'unità disco condivisa dalla quale dipende la risorsa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se @path non viene specificato, il percorso della directory predefinita del catalogo è nell'unità disco condivisa nella directory specificata durante l'installazione del server virtuale.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="remarks"></a>Note  
 Il **start_full** azione viene usata per creare uno snapshot completo dei dati full-text nella *fulltext_catalog_name*. Il **start_incremental** azione viene utilizzata per ripetere l'indicizzazione solo delle righe modificate nel database. Popolamento incrementale può essere applicato solo se la tabella include una colonna di tipo **timestamp**. Se una tabella nel catalogo full-text non contiene una colonna di tipo **timestamp**, la tabella viene eseguito un popolamento completo.  
  
 I dati dell'indice e del catalogo full-text vengono archiviati in file creati in una directory di catalogo full-text. La directory di catalogo full-text viene creata come una sottodirectory della directory specificata **@path** o nella directory di catalogo full-text predefinito del server se **@path** non specificato. Il nome della directory di catalogo full-text viene compilato in modo che sia univoco nel server. Le varie directory di catalogo full-text di un server pertanto possono condividere lo stesso percorso.  
  
## <a name="permissions"></a>Permissions  
 Il chiamante deve essere membro del **db_owner** ruolo. A seconda dell'azione richiesta, il chiamante non deve essere negato le autorizzazioni ALTER o CONTROL (quale **db_owner** ha) sul catalogo full-text di destinazione.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-create-a-full-text-catalog"></a>R. Creazione di un catalogo full-text  
 In questo esempio viene creato un catalogo full-text vuoto **Cat_Desc**, nella **AdventureWorks2012** database.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'create';  
GO  
```  
  
### <a name="b-to-rebuild-a-full-text-catalog"></a>B. Per ricompilare un catalogo full-text  
 Questo esempio viene ricompilato un catalogo full-text esistente, **Cat_Desc**, nella **AdventureWorks2012** database.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'rebuild';  
GO  
```  
  
### <a name="c-start-the-population-of-a-full-text-catalog"></a>C. Avvio del popolamento di un catalogo full-text  
 In questo esempio viene avviato un popolamento completo del **Cat_Desc** catalogo.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'start_full';  
GO  
```  
  
### <a name="d-stop-the-population-of-a-full-text-catalog"></a>D. Arresto del popolamento di un catalogo full-text  
 Questo esempio mostra come arrestare il popolamento della **Cat_Desc** catalogo.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'stop';  
GO  
```  
  
### <a name="e-to-remove-a-full-text-catalog"></a>E. Rimozione di un catalogo full-text  
 Questo esempio vengono rimossi i **Cat_Desc** catalogo.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'drop';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [sp_help_fulltext_catalogs_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Ricerca full-text](../../relational-databases/search/full-text-search.md)  
  
  
