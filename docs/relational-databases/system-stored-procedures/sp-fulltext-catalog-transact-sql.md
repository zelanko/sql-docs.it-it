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
ms.openlocfilehash: 4b51e4e38b7587074a39f850c2e56dbd8c09ed6f
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005968"
---
# <a name="sp_fulltext_catalog-transact-sql"></a>sp_fulltext_catalog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Consente di creare ed eliminare un catalogo full-text e di avviare e arrestare l'azione di indicizzazione per un catalogo. È possibile creare più cataloghi full-text per ogni database.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] usare in alternativa [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md), [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)e [DROP FULLTEXT CATALOG](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) .  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_fulltext_catalog [ @ftcat= ] 'fulltext_catalog_name' ,   
     [ @action= ] 'action'   
     [ , [ @path= ] 'root_directory' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @ftcat = ] 'fulltext_catalog_name'` è il nome del catalogo full-text. I nomi dei cataloghi devono essere univoci per ogni database. *fulltext_catalog_name* è di **tipo sysname**.  
  
`[ @action = ] 'action'` è l'azione da eseguire. *Action* è di tipo **varchar (20)** . i possibili valori sono i seguenti.  
  
> [!NOTE]  
>  I cataloghi full-text possono essere creati, eliminati e modificati in base alle necessità. Evitare tuttavia di modificare contemporaneamente più cataloghi a livello di schema. Queste azioni possono essere eseguite usando il stored procedure **sp_fulltext_table** , che è il metodo consigliato.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Creare**|Crea un nuovo catalogo full-text vuoto nel file system e aggiunge una riga associata in **sysfulltextcatalogs** con i valori *fulltext_catalog_name* e *root_directory*, se presenti. *fulltext_catalog_name* deve essere univoco all'interno del database.|  
|**Drop**|Elimina *fulltext_catalog_name* rimuovendo dalla file System ed eliminando la riga associata in **sysfulltextcatalogs**. Questa azione non viene completata se nel catalogo sono inclusi indici per una o più tabelle. **sp_fulltext_table** '*table_name*',' drop ' deve essere eseguito per eliminare le tabelle dal catalogo.<br /><br /> Se il catalogo non esiste, viene visualizzato un errore.|  
|**start_incremental**|Avvia un popolamento incrementale per *fulltext_catalog_name*. Se il catalogo non esiste, viene visualizzato un errore. Se è già attivo il popolamento di un indice full-text, viene visualizzato un avviso e il popolamento non viene eseguito. Con il popolamento incrementale vengono recuperate solo le righe modificate per l'indicizzazione full-text, purché sia presente una colonna **timestamp** nella tabella da indicizzare full-text.|  
|**start_full**|Avvia un popolamento completo per *fulltext_catalog_name*. Per l'indicizzazione full-text viene recuperata ogni riga di ogni tabella associata al catalogo, anche se è già stata indicizzata.|  
|**Arresta**|Arresta il popolamento di un indice per *fulltext_catalog_name*. Se il catalogo non esiste, viene visualizzato un errore. Se il popolamento è già stato arrestato, non viene visualizzato alcun avviso.|  
|**Ricompilazione**|Ricompila *fulltext_catalog_name*. Quando viene ricompilato un catalogo, il catalogo esistente viene eliminato e al suo posto viene creato un nuovo catalogo. Tutte le tabelle con riferimenti di indicizzazione full-text vengono associate al nuovo catalogo. La ricompilazione reimposta i metadati full-text nelle tabelle di sistema del database.<br /><br /> Se il rilevamento delle modifiche è impostato su OFF, la ricompilazione non comporta il ripopolamento del catalogo full-text appena creato. In questo caso, per ripopolare, eseguire **sp_fulltext_catalog** con l'azione **start_full** o **start_incremental** .|  
  
`[ @path = ] 'root_directory'` è la directory radice (non il percorso fisico completo) per un'azione di **creazione** . *root_directory* è di **tipo nvarchar (100)** e il valore predefinito è null, che indica l'utilizzo del percorso predefinito specificato al momento dell'installazione. Si tratta della sottodirectory Ftdata nella directory MSSQL. ad esempio, C:\Programmi\Microsoft SQL Server\MSSQL13. MSSQLSERVER\MSSQL\FTData. La directory radice specificata deve trovarsi in un'unità dello stesso computer, non deve corrispondere alla sola lettera di unità e non può essere un percorso relativo. Le unità di rete, le unità rimovibili, i dischi floppy e i percorsi in formato UNC non sono supportati. È necessario creare i cataloghi full-text in un'unità disco rigido locale associata a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **\@path** è valido solo quando viene **creata**l' *azione* . Per le azioni diverse da **create** (**Stop**, **Rebuild**e così via), **\@path** deve essere null o omesso.  
  
 Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un server virtuale in un cluster, la directory di catalogo specificata deve trovarsi in un'unità disco condivisa dalla quale dipende la risorsa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se non si specifica @path, il percorso della directory del catalogo predefinita si trova nell'unità disco condivisa, nella directory specificata durante l'installazione del server virtuale.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="remarks"></a>Note  
 L'azione **start_full** viene utilizzata per creare uno snapshot completo dei dati full-text in *fulltext_catalog_name*. L'azione **start_incremental** viene utilizzata per reindicizzare solo le righe modificate nel database. Il popolamento incrementale può essere applicato solo se la tabella contiene una colonna di tipo **timestamp**. Se una tabella nel catalogo full-text non contiene una colonna di tipo **timestamp**, la tabella viene sottoposta a un popolamento completo.  
  
 I dati dell'indice e del catalogo full-text vengono archiviati in file creati in una directory di catalogo full-text. La directory del catalogo full-text viene creata come una sottodirectory della directory specificata in **\@path** o nella directory del catalogo full-text predefinita del server se non si specifica **\@path** . Il nome della directory di catalogo full-text viene compilato in modo che sia univoco nel server. Le varie directory di catalogo full-text di un server pertanto possono condividere lo stesso percorso.  
  
## <a name="permissions"></a>Permissions  
 È necessario che il chiamante sia membro del ruolo **db_owner** . A seconda dell'azione richiesta, al chiamante non devono essere negate le autorizzazioni ALTER o CONTROL (che **db_owner** ha) nel catalogo full-text di destinazione.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-create-a-full-text-catalog"></a>R. Creazione di un catalogo full-text  
 In questo esempio viene creato un catalogo full-text vuoto, **Cat_Desc**, nel database **AdventureWorks2012** .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'create';  
GO  
```  
  
### <a name="b-to-rebuild-a-full-text-catalog"></a>B. Per ricompilare un catalogo full-text  
 In questo esempio viene ricompilato un catalogo full-text esistente, **Cat_Desc**, nel database **AdventureWorks2012** .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'rebuild';  
GO  
```  
  
### <a name="c-start-the-population-of-a-full-text-catalog"></a>C. Avvio del popolamento di un catalogo full-text  
 In questo esempio viene avviato un popolamento completo del catalogo **Cat_Desc** .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'start_full';  
GO  
```  
  
### <a name="d-stop-the-population-of-a-full-text-catalog"></a>D. Arresto del popolamento di un catalogo full-text  
 In questo esempio viene arrestato il popolamento del catalogo **Cat_Desc** .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'stop';  
GO  
```  
  
### <a name="e-to-remove-a-full-text-catalog"></a>E. Rimozione di un catalogo full-text  
 Questo esempio Mostra come rimuovere il catalogo **Cat_Desc** .  
  
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
  
  
