---
title: Opzioni (pagina di scripting Esplora oggetti di SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9966db2e5b08cd16976e2c16434cec0adca8445f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058558"
---
# <a name="options-sql-server-object-explorer-scripting-page"></a>Opzioni (Esplora oggetti di SQL Server-pagina di scripting)
  Usare questa pagina per impostare le opzioni di scripting valide per i comandi seguenti dei menu di scelta rapida degli oggetti in **Esplora oggetti**:  
  
-   Comandi**Modifica** per tabelle e viste utente.  
  
-   Comandi **Crea script\<object> per** per oggetti creati dall'utente.  
  
-   Comandi**Modifica** per oggetti creati dall'utente.  
  
-   Questa pagina consente inoltre di impostare i valori predefiniti per le opzioni di creazione di script per **Generazione guidata script di SQL Server**.  
  
## <a name="remarks"></a>Osservazioni  
 I comandi **Modifica** e **Cambia** potrebbero produrre risultati diversi rispetto al comando **Crea script \<object> per** con la stessa impostazione dell'opzione. I comandi **Modifica** e **Cambia** sono infatti stati creati per modificare oggetti nel database corrente durante una sessione dell'editor di query. Il comando **Crea script\<object> per** è invece stato creato per generare uno script affinché possa essere usato in seguito per la creazione di oggetti.  
  
## <a name="options"></a>Opzioni  
 Specificare le opzioni di scripting selezionando le impostazioni desiderate tra quelle disponibili nell'elenco visualizzato a destra di ciascuna opzione.  
  
### <a name="general-scripting-options"></a>Opzioni generali di scripting  
 **Delimita singole istruzioni**  
 Consente di separare istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] singole utilizzando un separatore batch. Per modificare il separatore batch predefinito per l' **editor di query**, scegliere **Strumenti**/**Opzioni**/**Esecuzione query**/**SQL Server**/**Generale**/**Separatore batch**. Il valore predefinito è False. Per ulteriori informazioni, vedere [GO &#40;&#41;Transact-SQL ](/sql/t-sql/language-elements/sql-server-utilities-statements-go).  
  
 **Includi intestazioni descrittive**  
 Consente di aggiungere commenti descrittivi allo script dividendolo in sezioni per ogni oggetto. Il valore predefinito è true. Per altre informazioni, vedere [Comment &#40;&#41;Transact-SQL ](/sql/t-sql/language-elements/comment-transact-sql).  
  
 **Includi opzioni vardecimal**  
 Consente di includere le opzioni per l'archiviazione vardecimal. Il valore predefinito è False. Per ulteriori informazioni, vedere e [sp_db_vardecimal_storage_format &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql).  
  
 **Genera script per il rilevamento modifiche**  
 Consente di includere nello script le informazioni sul rilevamento delle modifiche.  
  
 **Script per versione server**  
 Consente di creare uno script eseguibile nella versione selezionata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Non è possibile creare script per versioni precedenti per le nuove funzionalità di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] . Alcuni script creati per [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] non possono essere eseguiti in server con una versione precedente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]o in un database con un' [impostazione del livello di compatibilità del database](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)precedente.  
  
 **Script per cataloghi full-text**  
 Consente di includere uno script per cataloghi full-text. Il valore predefinito è False. Per altre informazioni, vedere [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql).  
  
 **UTILIZZO script\<database>**  
 Aggiunge l'istruzione USE DATABASE allo script per creare oggetti di database nel contesto del database di **Esplora oggetti** corrente. Se si prevede di utilizzare lo script in un database diverso, selezionare False per omettere tale istruzione. Il valore predefinito è true. Per altre informazioni, vedere [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql).  
  
### <a name="object-scripting-options"></a>Opzioni di scripting per gli oggetti  
 **Genera script per oggetti dipendenti**  
 Consente di generare uno script per oggetti aggiuntivi, richiesti quando viene eseguito lo script per l'oggetto selezionato. Il valore predefinito è False.  
  
 **Includi clausola IF NOT EXISTS**  
 Consente di includere un'istruzione per verificare che ogni oggetto non sia presente nel database prima del tentativo di crearlo. Il valore predefinito è False. Per ulteriori informazioni, vedere [if... In caso contrario &#40;&#41;Transact-SQL](/sql/t-sql/language-elements/if-else-transact-sql) ed [esiste &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/exists-transact-sql).  
  
 **Schema per qualifica dei nomi degli oggetti**  
 Consente di qualificare il nome degli oggetti con lo schema dell'oggetto. Il valore predefinito è False. Per altre informazioni, vedere [Creazione di uno schema di database](../../relational-databases/security/authentication-access/create-a-database-schema.md).  
  
 **Script per proprietà estese**  
 Consente di includere le proprietà estese nello script qualora l'oggetto disponga di proprietà estese. Il valore predefinito è False. Per altre informazioni, vedere [sp_addextendedproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql).  
  
 **Proprietario script**  
 Consente di includere il proprietario nello script generato. Il valore predefinito è False.  
  
 **Script per autorizzazioni**  
 Consente di includere autorizzazioni sugli oggetti di database nello script. Il valore predefinito è true. Per ulteriori informazioni, vedere [autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-database-engine.md).  
  
### <a name="tableview-options"></a>Opzioni tabella/vista  
 Le opzioni seguenti si applicano solo agli script per tabelle o viste.  
  
 **Converti tipi di dati definiti dall'utente in tipi di base**  
 Consente di convertire i tipi di dati definiti dall'utente nei tipi di base da cui sono stati creati. Utilizzare True se il tipo di dati definito dall'utente nel database di origine non è presente nel database in cui lo script verrà eseguito. Utilizzare False per mantenere i tipi di dati definiti dall'utente. Il valore predefinito è False. Per ulteriori informazioni, vedere [CREATE TYPE &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-type-transact-sql).  
  
 **Genera comandi SET ANSI PADDING**  
 Consente di aggiungere l'istruzione SET ANSI_PADDING prima e dopo ogni istruzione CREATE TABLE. Il valore predefinito è true. Per altre informazioni, vedere [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql).  
  
 **Includi regole di confronto**  
 Consente di includere le regole di confronto nella definizione della colonna. Il valore predefinito è true. Per altre informazioni, vedere [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
 **Includi proprietà IDENTITY**  
 Consente di includere definizioni per il valore di inizializzazione di IDENTITY e l'incremento di IDENTITY. Il valore predefinito è true. Per altre informazioni, vedere [IDENTITY &#40;proprietà&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property).  
  
 **Schema per qualifica dei riferimenti alle chiavi esterne**  
 Consente di aggiungere il nome dello schema ai riferimenti alle tabelle per i vincoli FOREIGN KEY. Il valore predefinito è true.  
  
 **Script per associazione di valori predefiniti e regole**  
 Includere le chiamate alle stored procedure di associazione **sp_bindefault** e **sp_bindrule** . Il valore predefinito è true. Per ulteriori informazioni, vedere [sp_bindefault &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-bindefault-transact-sql) e [sp_bindrule &#40;transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindrule-transact-sql).  
  
 **Script per vincoli CHECK**  
 Aggiunge [vincoli CHECK](../../relational-databases/tables/unique-constraints-and-check-constraints.md) allo script. Il valore predefinito è true.  
  
 **Script per valori predefiniti**  
 Consente di includere i valori predefiniti delle colonne nello script. Il valore predefinito è False. Per altre informazioni, vedere [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql).  
  
 **Script per filegroup**  
 Consente di specificare il filegroup nella clausola ON per le definizioni di tabella. Il valore predefinito è False. Per altre informazioni, vedere [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).  
  
 **Script per chiavi esterne**  
 Include [vincoli FOREIGN KEY](../../relational-databases/tables/primary-and-foreign-key-constraints.md) nello script. Il valore predefinito è False.  
  
 **Script per indici full-text**  
 Consente di includere indici full-text nello script. Il valore predefinito è False. Per altre informazioni, vedere [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql).  
  
 **Script per indici**  
 Consente di includere indici cluster, non cluster e XML nello script. Il valore predefinito è true. Per altre informazioni, vedere [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql).  
  
 **Script per schemi di partizione**  
 Consente di includere schemi di partizione di tabelle nello script. Il valore predefinito è False. Per altre informazioni, vedere [creare uno schema di partizione &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-partition-scheme-transact-sql).  
  
 **Script per chiavi primarie**  
 Include [vincoli primari e FOREIGN KEY](../../relational-databases/tables/primary-and-foreign-key-constraints.md) nello script. Il valore predefinito è true.  
  
 **Script per statistiche**  
 Consente di includere statistiche definite dall'utente nello script. Il valore predefinito è False. Per altre informazioni, vedere [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Script per trigger**  
 Consente di includere trigger nello script. Il valore predefinito è False. Per altre informazioni, vedere [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
 **Script per chiavi univoche**  
 Include [vincoli UNIQUE e CHECK](../../relational-databases/tables/unique-constraints-and-check-constraints.md) nello script. Il valore predefinito è False.  
  
 **Script per colonne vista**  
 Consente di dichiarare colonne di viste in intestazioni di viste. Il valore predefinito è False. Per altre informazioni, vedere [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql).  
  
 **ScriptDriIncludeSystemNames**  
 Consente di includere nomi di vincoli generati dal sistema per applicare l'integrità referenziale dichiarativa. Il valore predefinito è False. Per ulteriori informazioni, vedere [REFERENTIAL_CONSTRAINTS &#40;&#41;Transact-SQL ](/sql/relational-databases/system-information-schema-views/referential-constraints-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Generazione di script &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/generate-scripts-sql-server-management-studio.md)  
  
  
