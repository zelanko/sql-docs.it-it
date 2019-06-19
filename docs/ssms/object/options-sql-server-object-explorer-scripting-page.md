---
title: Opzioni (Esplora oggetti di SQL Server - pagina Generazione script) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bd09972eaebba893ac92198c9b953392e383f9e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65095728"
---
# <a name="options-sql-server-object-explorer---scripting-page"></a>Opzioni (Esplora oggetti di SQL Server - pagina Generazione script)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Usare questa pagina per impostare le opzioni di scripting valide per i comandi seguenti dei menu di scelta rapida degli oggetti in **Esplora oggetti**:  
  
-   Comandi **Modifica** per tabelle e viste utente.  
  
-   Comandi **Crea script<object> per** per oggetti creati dall'utente.  
  
-   Comandi **Modifica** per oggetti creati dall'utente.  
  
-   Questa pagina consente inoltre di impostare i valori predefiniti per le opzioni di creazione di script per **Generazione guidata script di SQL Server**.  
  
## <a name="remarks"></a>Remarks  
I comandi **Modifica** e **Cambia** potrebbero produrre risultati diversi rispetto al comando **Crea script <object> per** con la stessa impostazione dell'opzione. I comandi **Modifica** e **Cambia** sono infatti stati creati per modificare oggetti nel database corrente durante una sessione dell'editor di query. Il comando **Crea script<object> per** è invece stato creato per generare uno script affinché possa essere usato in seguito per la creazione di oggetti.  
  
## <a name="options"></a>Opzioni  
Specificare le opzioni di scripting selezionando le impostazioni desiderate tra quelle disponibili nell'elenco visualizzato a destra di ciascuna opzione.  
  
### <a name="general-scripting-options"></a>Opzioni generali di scripting  
**Delimita singole istruzioni**  
Consente di separare istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] singole utilizzando un separatore batch. Per modificare il separatore batch predefinito per l' **editor di query**, scegliere **Strumenti**/**Opzioni**/**Esecuzione query**/**SQL Server**/**Generale**/**Separatore batch**. Il valore predefinito è False. Per altre informazioni, vedere [GO (Transact-SQL)](https://msdn.microsoft.com/b2ca6791-3a07-4209-ba8e-2248a92dd738).  
  
**Includi intestazioni descrittive**  
Consente di aggiungere commenti descrittivi allo script dividendolo in sezioni per ogni oggetto. Il valore predefinito è True. Per altre informazioni, vedere [/ *...* / (Comment) (Transact-SQL)](https://msdn.microsoft.com/4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c).  
  
**Includi abilitazione compressione VarDecimal**  
Consente di includere le opzioni per l'archiviazione vardecimal. Il valore predefinito è False. Per altre informazioni, vedere [sp_db_vardecimal_storage_format (Transact-SQL)](https://msdn.microsoft.com/9920b2f7-b802-4003-913c-978c17ae4542).  
  
**Genera script per il rilevamento modifiche**  
Consente di includere nello script le informazioni sul rilevamento delle modifiche.  
  
**Script per cataloghi full-text**  
Consente di includere uno script per cataloghi full-text. Il valore predefinito è False. Per altre informazioni, vedere [CREATE FULLTEXT CATALOG (Transact-SQL)](https://msdn.microsoft.com/d7a8bd93-e2d7-4a40-82ef-39069e65523b).  
  
**Script per USE <database>**  
Aggiunge l'istruzione USE DATABASE allo script per creare oggetti di database nel contesto del database di **Esplora oggetti** corrente. Se si prevede di utilizzare lo script in un database diverso, selezionare False per omettere tale istruzione. Il valore predefinito è True. Per altre informazioni, vedere [USE (Transact-SQL)](https://msdn.microsoft.com/c05acac8-c063-4770-8e36-d7f71d500b10).  
  
### <a name="object-scripting-options"></a>Opzioni di scripting per gli oggetti  

**Verifica esistenza oggetto**: verifica che un oggetto con il nome specificato esista prima dell'eliminazione o della modifica oppure che un oggetto con il nome specificato non esista prima della creazione. Per altre informazioni, vedere [IF...ELSE (Transact-SQL)](https://msdn.microsoft.com/676c881f-dee1-417a-bc51-55da62398e81) e [EXISTS (Transact-SQL)](https://msdn.microsoft.com/b6510a65-ac38-4296-a3d5-640db0c27631).

**Genera script per oggetti dipendenti**  
Consente di generare uno script per oggetti aggiuntivi, richiesti quando viene eseguito lo script per l'oggetto selezionato. Il valore predefinito è False.  
  
**Schema per qualifica dei nomi degli oggetti**  
Consente di qualificare il nome degli oggetti con lo schema dell'oggetto. Il valore predefinito è False. Per altre informazioni, vedere [Creazione di uno schema di database](../../relational-databases/security/authentication-access/create-a-database-schema.md).  

**Genera script per le opzioni di compressione dati**: include opzioni di compressione dati nello script. Il valore predefinito è False.

**Script per proprietà estese**  
Consente di includere le proprietà estese nello script qualora l'oggetto disponga di proprietà estese. Il valore predefinito è False. Per altre informazioni, vedere [sp_addextendedproperty (Transact-SQL)](https://msdn.microsoft.com/565483ea-875b-4133-b327-d0006d2d7b4c).  
  
**Proprietario script**  
Consente di includere il proprietario nello script generato. Il valore predefinito è False.  
  
**Script per autorizzazioni**  
Consente di includere autorizzazioni sugli oggetti di database nello script. Il valore predefinito è True. Per altre informazioni, vedere [Autorizzazioni](../../relational-databases/security/permissions-database-engine.md).  
  
### <a name="tableview-options"></a>Opzioni tabella/vista  
Le opzioni seguenti si applicano solo agli script per tabelle o viste.  
  
**Converti tipi di dati definiti dall'utente in tipi di base**  
Consente di convertire i tipi di dati definiti dall'utente nei tipi di base da cui sono stati creati. Utilizzare True se il tipo di dati definito dall'utente nel database di origine non è presente nel database in cui lo script verrà eseguito. Utilizzare False per mantenere i tipi di dati definiti dall'utente. Il valore predefinito è False. Per altre informazioni, vedere [CREATE TYPE (Transact-SQL)](https://msdn.microsoft.com/2202236b-e09f-40a1-bbc7-b8cff7488905).  
  
**Genera comandi SET ANSI PADDING**  
Consente di aggiungere l'istruzione SET ANSI_PADDING prima e dopo ogni istruzione CREATE TABLE. Il valore predefinito è True. Per altre informazioni, vedere [SET ANSI_PADDING (Transact-SQL)](https://msdn.microsoft.com/92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0).  
  
**Includi regole di confronto**  
Consente di includere le regole di confronto nella definizione della colonna. Il valore predefinito è True. Per altre informazioni, vedere [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
**Includi proprietà IDENTITY**  
Consente di includere definizioni per il valore di inizializzazione di IDENTITY e l'incremento di IDENTITY. Il valore predefinito è True. Per altre informazioni, vedere [IDENTITY (Property) (Transact-SQL)](https://msdn.microsoft.com/8429134f-c821-4033-a07c-f782a48d501c).  
  
**Schema per qualifica dei riferimenti alle chiavi esterne**  
Consente di aggiungere il nome dello schema ai riferimenti alle tabelle per i vincoli FOREIGN KEY. Il valore predefinito è True.  
  
**Script per associazione di valori predefiniti e regole**  
Includere le chiamate alle stored procedure di associazione **sp_bindefault** e **sp_bindrule** . Il valore predefinito è True. Per altre informazioni, vedere [sp_bindefault (Transact-SQL)](https://msdn.microsoft.com/3da70c10-68d0-4c16-94a5-9e84c4a520f6) e [sp_bindrule (Transact-SQL)](https://msdn.microsoft.com/2606073e-c52f-498d-a923-5026b9d97e67).  
  
**Script per vincoli CHECK**  
Aggiunge [vincoli CHECK](../../relational-databases/tables/unique-constraints-and-check-constraints.md) allo script. Il valore predefinito è True.  
  
**Script per valori predefiniti**  
Consente di includere i valori predefiniti delle colonne nello script. Il valore predefinito è False. Per altre informazioni, vedere [CREATE DEFAULT (Transact-SQL)](https://msdn.microsoft.com/08475db4-7d90-486a-814c-01a99d783d41).  
  
**Script per filegroup**  
Consente di specificare il filegroup nella clausola ON per le definizioni di tabella. Il valore predefinito è False. Per altre informazioni, vedere [CREATE TABLE (Transact-SQL)](https://msdn.microsoft.com/1e068443-b9ea-486a-804f-ce7b6e048e8b).  
  
**Script per chiavi esterne**  
Include [vincoli FOREIGN KEY](../../relational-databases/tables/primary-and-foreign-key-constraints.md) nello script. Il valore predefinito è False.  
  
**Script per indici full-text**  
Consente di includere indici full-text nello script. Il valore predefinito è False. Per altre informazioni, vedere [CREATE FULLTEXT INDEX (Transact-SQL)](https://msdn.microsoft.com/8b80390f-5f8b-4e66-9bcc-cabd653c19fd).  
  
**Script per indici**  
Consente di includere indici cluster, non cluster e XML nello script. Il valore predefinito è True. Per altre informazioni, vedere [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/d2297805-412b-47b5-aeeb-53388349a5b9).  
  
**Script per schemi di partizione**  
Consente di includere schemi di partizione di tabelle nello script. Il valore predefinito è False. Per altre informazioni, vedere [CREATE PARTITION SCHEME (Transact-SQL)](https://msdn.microsoft.com/5b21c53a-b4f4-4988-89a2-801f512126e4).  
  
**Script per chiavi primarie**  
Include [vincoli primari e FOREIGN KEY](../../relational-databases/tables/primary-and-foreign-key-constraints.md) nello script. Il valore predefinito è True.  
  
**Script per statistiche**  
Consente di includere statistiche definite dall'utente nello script. Il valore predefinito è False. Per altre informazioni, vedere [CREATE STATISTICS (Transact-SQL)](https://msdn.microsoft.com/b23e2f6b-076c-4e6d-9281-764bdb616ad2).  
  
**Script per trigger**  
Consente di includere trigger nello script. Il valore predefinito è False. Per altre informazioni, vedere [CREATE TRIGGER (Transact-SQL)](https://msdn.microsoft.com/edeced03-decd-44c3-8c74-2c02f801d3e7).  
  
**Script per chiavi univoche**  
Include [vincoli UNIQUE e CHECK](../../relational-databases/tables/unique-constraints-and-check-constraints.md) nello script. Il valore predefinito è False.  
  
**Script per colonne vista**  
Consente di dichiarare colonne di viste in intestazioni di viste. Il valore predefinito è False. Per altre informazioni, vedere [CREATE VIEW (Transact-SQL)](https://msdn.microsoft.com/aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9).  
  
**Includi nomi di sistema DRI**  
Consente di includere nomi di vincoli generati dal sistema per applicare l'integrità referenziale dichiarativa. Il valore predefinito è False. Per altre informazioni, vedere [REFERENTIAL_CONSTRAINTS (Transact-SQL)](https://msdn.microsoft.com/5d358f18-0a85-4b55-af4b-98d5f4cd1020).  
  
### <a name="version-options"></a>Opzioni di versione

**Corrispondenza delle impostazioni dello script con l'origine**: se abilitata, la versione di destinazione, l'edizione e il tipo del motore degli script generati saranno impostati sui valori del server da cui viene eseguito l'inserimento dell'oggetto nello script. Vengono così disabilitate e ignorate le altre opzioni di versione. 

**Script per l'edizione del motore di database**: gli script generati saranno destinati all'[edizione del motore](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.edition.aspx) specificata.

**Script per il tipo di motore di database**: gli script generati saranno destinati al [tipo di motore di database](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.databaseenginetype.aspx) specificato.

**Script per versione server**  
Gli script saranno destinati alla versione specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non è possibile creare script per versioni precedenti per le nuove funzionalità di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Alcuni script creati per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] non possono essere eseguiti in server con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o in un database con un' [impostazione del livello di compatibilità del database](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)precedente.  

## <a name="see-also"></a>Vedere anche  
[Generare script (SQL Server Management Studio)](https://msdn.microsoft.com/9711c617-3c68-4e5a-aea3-befc64d51524)  
  
