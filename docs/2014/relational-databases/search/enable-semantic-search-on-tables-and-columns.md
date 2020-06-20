---
title: Abilitare la ricerca semantica in tabelle e colonne | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], enabling
ms.assetid: 895d220c-6749-4954-9dd3-2ea4c6a321ff
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f11ba654f7cc34f521990e8c420d41885d3c55b9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85004429"
---
# <a name="enable-semantic-search-on-tables-and-columns"></a>Abilitare la ricerca semantica in tabelle e colonne
  Viene descritto come abilitare o disabilitare l'indicizzazione semantica statistica in colonne selezionate contenenti documenti o testo.  
  
 Nella ricerca semantica statistica vengono utilizzati gli indici creati dalla ricerca full-text e vengono creati indici aggiuntivi. Come risultato di questa dipendenza dalla ricerca full-text, viene creato un nuovo indice semantico quando si definisce un nuovo indice full-text o si modifica un indice full-text esistente. È possibile creare un nuovo indice semantico utilizzando le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] o l'Indicizzazione guidata full-text e le altre finestre di dialogo di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], come descritto in questo argomento.  
  
##  <a name="creating-a-semantic-index"></a><a name="BasicEnabling"></a>Creazione di un indice semantico  
  
###  <a name="requirements-and-restrictions-for-creating-a-semantic-index"></a><a name="reqenable"></a>Requisiti e restrizioni per la creazione di un indice semantico  
  
-   È possibile creare un indice in qualsiasi oggetto di database supportato per l'indicizzazione full-text, incluse tabelle e viste indicizzate.  
  
-   Prima che sia possibile abilitare l'indicizzazione semantica per colonne specifiche, devono esistere i prerequisiti riportati di seguito.  
  
    -   Deve esistere un catalogo full-text per il database.  
  
    -   La tabella deve disporre di un indice full-text.  
  
    -   Le colonne selezionate devono far parte dell'indice full-text.  
  
     È possibile creare e abilitare contemporaneamente tutti questi prerequisiti.  
  
-   È possibile creare un indice semantico in colonne che includono qualsiasi tipo di dati supportato per l'indicizzazione full-text. Per altre informazioni, vedere [Creare e gestire indici full-text](create-and-manage-full-text-indexes.md).  
  
-   È possibile specificare qualsiasi tipo di documento supportato per l'indicizzazione full-text per colonne `varbinary(max)`. Per ulteriori informazioni, vedere [Procedura: determinare quali tipi di documenti è possibile indicizzare](#doctypes) in questo argomento.  
  
-   L'indicizzazione semantica consente di creare due tipi di indici per le colonne selezionate, ovvero un indice di frasi chiave e un indice di somiglianza del documento. Non è possibile selezionare solo uno dei due tipi di indice quando si abilita l'indicizzazione semantica. È tuttavia possibile eseguire query indipendenti su questi due indici. Per altre informazioni, vedere [Trovare frasi chiave nei documenti mediante ricerca semantica](find-key-phrases-in-documents-with-semantic-search.md) e [Trovare documenti simili e correlati tramite la ricerca semantica](find-similar-and-related-documents-with-semantic-search.md).  
  
-   Se non si specifica in modo esplicito un LCID per un indice semantico, per l'indicizzazione semantica vengono utilizzate solo la lingua principale e le statistiche sulla lingua associate.  
  
-   Se si specifica una lingua per una colonna per cui non è disponibile il modello di lingua, la creazione dell'indice ha esito negativo e viene restituito un messaggio di errore.  
  
###  <a name="how-to-create-a-semantic-index-when-there-is-no-full-text-index"></a><a name="HowToEnableCreate"></a>Procedura: creare un indice semantico quando non esiste alcun indice full-text  
 Quando si crea un nuovo indice full-text con l'istruzione **CREATE FULLTEXT INDEX** , è possibile abilitare l'indicizzazione semantica a livello di colonna specificando la parola chiave **STATISTICAL_SEMANTICS** come parte della definizione della colonna. È inoltre possibile abilitare l'indicizzazione semantica quando si utilizza l'Indicizzazione guidata full-text per creare un nuovo indice full-text.  
  
 **Creare un nuovo indice semantico tramite Transact-SQL**  
 Chiamare l'istruzione **CREATE FULLTEXT INDEX** e specificare **STATISTICAL_SEMANTICS** per ogni colonna in cui creare un indice semantico. Per altre informazioni su tutte le opzioni per questa istruzione, vedere [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql).  
  
 **Esempio 1: creazione di un indice univoco, di un indice full-text e di un indice semantico**  
  
 L'esempio riportato di seguito crea il catalogo full-text predefinito **ft**. L'esempio crea quindi un indice univoco nella colonna **JobCandidateID** della tabella **HumanResources.JobCandidate** del database di esempio AdventureWorks2012. Questo indice univoco è necessario come colonna chiave di un indice full-text. L'esempio crea infine un indice full-text e un indice semantico nella colonna **Resume** .  
  
```sql  
CREATE FULLTEXT CATALOG ft AS DEFAULT  
GO  
  
CREATE UNIQUE INDEX ui_ukJobCand  
    ON HumanResources.JobCandidate(JobCandidateID)  
GO  
  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate  
    (Resume  
        Language 1033  
        Statistical_Semantics  
    )   
    KEY INDEX JobCandidateID   
    WITH STOPLIST = SYSTEM  
GO  
```  
  
 **Esempio: creazione di un indice full-text e semantico in diverse colonne con popolamento dell'indice posticipato**  
  
 L'esempio seguente crea un catalogo full-text **documents_catalog**nel database di esempio AdventureWorks2012. Nell'esempio viene quindi creato un indice full-text che utilizza questo nuovo catalogo. L'indice full-text viene creato per le colonne **Title**, **DocumentSummary**e **Document** della tabella **Production.Document** , mentre l'indice semantico viene creato solo per la colonna **Document** . Questo indice full-text usa il catalogo full-text appena creato e un indice di chiave univoca esistente, **PK_Document_DocumentID**. Come consigliato, questa chiave di indice viene creata in una colonna Integer, **DocumentID**. Nell'esempio viene specificato l'LCID 1033 per l'inglese, che identifica la lingua dei dati presenti nelle colonne.  
  
 Nell'esempio viene anche specificato che il rilevamento delle modifiche è disabilitato e che non viene eseguito il popolamento. In seguito, durante le ore di minore attività, l'esempio usa un'istruzione **ALTER FULLTEXT INDEX** per avviare un popolamento completo nel nuovo indice e abilitare il rilevamento automatico delle modifiche.  
  
```sql  
CREATE FULLTEXT CATALOG documents_catalog  
GO  
  
CREATE FULLTEXT INDEX ON Production.Document  
    (   
    Title  
        Language 1033,   
    DocumentSummary  
        Language 1033,   
    Document   
        TYPE COLUMN FileExtension  
        Language 1033  
        Statistical_Semantics  
    )  
    KEY INDEX PK_Document_DocumentID  
        ON documents_catalog  
        WITH CHANGE_TRACKING OFF, NO POPULATION  
GO  
```  
  
 In un secondo momento, in un orario di minore attività, l'indice viene popolato:  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO  
GO  
```  
  
 **Creare un nuovo indice semantico tramite SQL Server Management Studio**  
 Eseguire l'Indicizzazione guidata full-text e abilitare **Semantica statistica** nella pagina **Selezione colonne tabella** per ogni colonna in cui creare un indice semantico. Per altre informazioni, comprese le informazioni sulla modalità di avvio dell'Indicizzazione guidata full-text, vedere [Usare l'Indicizzazione guidata full-text](use-the-full-text-indexing-wizard.md).  
  
###  <a name="how-to-create-a-semantic-index-when-there-is-an-existing-full-text-index"></a><a name="HowToEnableAlter"></a>Procedura: creare un indice semantico quando esiste un indice full-text esistente  
 È possibile aggiungere un'indicizzazione semantica quando si modifica un indice full-text esistente tramite l'istruzione **ALTER FULLTEXT INDEX** . È inoltre possibile aggiungere l'indicizzazione semantica utilizzando le varie finestre di dialogo in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Aggiungere un indice semantico tramite Transact-SQL**  
 Chiamare l'istruzione **ALTER FULLTEXT INDEX** con le opzioni descritte di seguito per ogni colonna in cui aggiungere un indice semantico. Per altre informazioni su tutte le opzioni per questa istruzione, vedere [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql).  
  
 Se non diversamente specificato, dopo una chiamata ad **ALTER** vengono ripopolati sia gli indici full-text, sia gli indici semantici.  
  
-   Per aggiungere l'indicizzazione full-text solo a una colonna, usare la sintassi **ADD** .  
  
-   Per aggiungere l'indicizzazione sia full-text, sia semantica a una colonna, usare la sintassi **ADD** con l'opzione **STATISTICAL_SEMANTICS** .  
  
-   Per aggiungere l'indicizzazione semantica a una colonna già abilitata per l'indicizzazione full-text, usare l'opzione **ADD STATISTICAL_SEMANTICS** . È possibile aggiungere l'indicizzazione semantica solo a una colonna in una singola istruzione **ALTER** .  
  
 **Esempio: aggiunta di indicizzazione semantica a una colonna già abilitata per l'indicizzazione full-text**  
  
 Nell'esempio seguente viene modificato un indice full-text esistente nella tabella **Production.Document** del database di esempio AdventureWorks2012. Nell'esempio viene aggiunto un indice semantico nella colonna **Document** della tabella **Production.Document** , in cui è già presente un indice full-text. Nell'esempio viene specificato che l'indice non verrà ripopolato automaticamente.  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document  
    ALTER COLUMN Document  
        ADD Statistical_Semantics  
    WITH NO POPULATION  
GO  
```  
  
 **Aggiungere un indice semantico tramite SQL Server Management Studio**  
 È possibile modificare le colonne abilitate per l'indicizzazione semantica e full-text nella pagina **Colonne indice full-text** della finestra di dialogo **Proprietà indice full-text** . Per altre informazioni, vedere [Gestire indici full-text](../../database-engine/manage-full-text-indexes.md).  
  
###  <a name="requirements-and-restrictions-for-altering-an-existing-index"></a><a name="addreq"></a>Requisiti e restrizioni per la modifica di un indice esistente  
  
-   Non è possibile modificare un indice esistente mentre è in corso il popolamento dell'indice. Per altre informazioni sul monitoraggio dello stato di popolamento dell'indice, vedere [Gestire e monitorare la ricerca semantica](manage-and-monitor-semantic-search.md).  
  
-   Non è possibile aggiungere l'indicizzazione a una colonna e modificare o eliminare l'indicizzazione per la stessa colonna in una singola chiamata all'istruzione **ALTER FULLTEXT INDEX** .  
  
##  <a name="dropping-a-semantic-index"></a><a name="dropping"></a>Eliminazione di un indice semantico  
  
###  <a name="how-to-drop-a-semantic-index"></a><a name="drophow"></a>Procedura: eliminare un indice semantico  
 È possibile eliminare un'indicizzazione semantica quando si modifica un indice full-text esistente tramite l'istruzione **ALTER FULLTEXT INDEX** . È possibile eliminare inoltre l'indicizzazione semantica tramite le varie finestre di dialogo in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Eliminare l'indice semantico tramite Transact-SQL**  
 -   Per eliminare l'indicizzazione semantica solo da una colonna o da colonne, chiamare l'istruzione **ALTER FULLTEXT INDEX** con l'opzione **ALTER column***column_name***drop STATISTICAL_SEMANTICS** . È possibile eliminare l'indicizzazione da più colonne in una singola istruzione **ALTER** .  
  
    ```sql  
    USE database_name  
    GO  
  
    ALTER FULLTEXT INDEX  
        ALTER COLUMN column_name  
        DROP STATISTICAL_SEMANTICS  
    GO  
    ```  
  
-   Per eliminare l'indicizzazione full-text e semantica da una colonna, chiamare l'istruzione **ALTER FULLTEXT INDEX** con l'opzione **ALTER COLUMN***column_name***drop** .  
  
    ```sql  
    USE database_name  
    GO  
  
    ALTER FULLTEXT INDEX  
        ALTER COLUMN column_name  
        DROP  
    GO  
    ```  
  
 **Eliminare un indice semantico tramite SQL Server Management Studio**  
 È possibile modificare le colonne abilitate per l'indicizzazione semantica e full-text nella pagina **Colonne indice full-text** della finestra di dialogo **Proprietà indice full-text** . Per altre informazioni, vedere [Gestire indici full-text](../../database-engine/manage-full-text-indexes.md).  
  
###  <a name="requirements-and-restrictions-for-dropping-a-semantic-index"></a><a name="dropreq"></a>Requisiti e restrizioni per l'eliminazione di un indice semantico  
  
-   Non è possibile eliminare indicizzazione full-text da una colonna mantenendo l'indicizzazione semantica. L'indicizzazione semantica dipende dall'indicizzazione full-text per i risultati di somiglianza del documento.  
  
-   Non è possibile specificare l'opzione **NO POPULATION** quando si elimina l'indicizzazione semantica dall'ultima colonna in una tabella per cui è stata abilitata l'indicizzazione semantica. È necessario un ciclo di popolamento per rimuovere i risultati precedentemente indicizzati.  
  
## <a name="checking-whether-semantic-search-is-enabled-on-database-objects"></a>Verifica dell'abilitazione della ricerca semantica su oggetti di database  
  
###  <a name="how-to-check-whether-semantic-search-is-enabled-on-database-objects"></a><a name="HowToCheckEnabled"></a>Procedura: verificare se la ricerca semantica è abilitata per gli oggetti di database  
 **Verifica dell'abilitazione della ricerca semantica per un database**  
 Eseguire una query sulla proprietà **IsFullTextEnabled** della funzione per i metadati [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/databasepropertyex-transact-sql).  
  
 Se viene restituito il valore 1, la ricerca full-text e la ricerca semantica sono abilitate per il database. Se viene restituito il valore 0, le ricerche non sono abilitate.  
  
```sql  
SELECT DATABASEPROPERTYEX('database_name', 'IsFullTextEnabled')  
GO  
```  
  
 **Verifica dell'abilitazione della ricerca semantica per una tabella**  
 Eseguire una query sulla proprietà **TableFullTextSemanticExtraction** della funzione per i metadati [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql).  
  
 Se viene restituito il valore 1, la ricerca semantica è abilitata per la tabella. Se viene restituito il valore 0, la ricerca non è abilitata.  
  
```scr  
SELECT OBJECTPROPERTYEX(OBJECT_ID('table_name'), 'TableFullTextSemanticExtraction')  
GO  
```  
  
 **Verifica dell'abilitazione della ricerca semantica per una colonna**  
 Per determinare se la ricerca semantica è abilitata per una colonna specifica:  
  
-   Eseguire una query sulla proprietà **StatisticalSemantics** della funzione per i metadati [COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql).  
  
     Se viene restituito il valore 1, la ricerca semantica è abilitata per la colonna. Se viene restituito il valore 0, la ricerca non è abilitata.  
  
    ```sql  
    SELECT COLUMNPROPERTY(OBJECT_ID('table_name'), 'column_name', 'StatisticalSemantics')  
    GO  
    ```  
  
-   Eseguire una query sulla vista del catalogo [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql) per l'indice full-text.  
  
     Il valore 1 nella colonna **statistical_semantics** indica che la colonna specificata è abilitata per l'indicizzazione semantica oltre che per l'indicizzazione full-text.  
  
    ```sql  
    SELECT * FROM sys.fulltext_index_columns WHERE object_id = OBJECT_ID('table_name')  
    GO  
    ```  
  
-   In Esplora oggetti in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]fare clic con il pulsante destro del mouse su una colonna e scegliere **Proprietà**. Nella pagina **Generale** della finestra di dialogo **Proprietà colonna** verificare il valore della proprietà **Semantica statistica** .  
  
     Il valore True indica che la colonna specificata è abilitata per l'indicizzazione semantica oltre che per l'indicizzazione full-text.  
  
## <a name="determining-what-can-be-indexed-for-semantic-search"></a>Determinare ciò che può essere indicizzato per la ricerca semantica  
  
###  <a name="how-to-check-which-languages-are-supported-for-semantic-search"></a><a name="HowToCheckLanguages"></a>Procedura: verificare quali lingue sono supportate per la ricerca semantica  
  
> [!IMPORTANT]  
>  L'indicizzazione semantica supporta un numero minore di lingue rispetto all'indicizzazione full-text. Di conseguenza, alcune colonne supportano l'indicizzazione full-text, ma non l'indicizzazione semantica.  
  
 Eseguire una query sulla vista del catalogo [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql).  
  
```sql  
SELECT * FROM sys.fulltext_semantic_languages  
GO  
```  
  
 Per l'indicizzazione semantica sono supportate le lingue seguenti. Questo elenco rappresenta l'output della vista del catalogo [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql), ordinato per LCID.  
  
|Linguaggio|LCID|  
|--------------|----------|  
|Tedesco|1031|  
|Inglese (Stati Uniti)|1033|  
|Francese|1036|  
|Italiano|1040|  
|Portoghese (Brasile)|1046|  
|Russo|1049|  
|Svedese|1053|  
|Inglese (Regno Unito)|2057|  
|Portoghese (Portogallo)|2070|  
|Spagnolo|3082|  
  
###  <a name="how-to-determine-which-document-types-can-be-indexed"></a><a name="doctypes"></a>Procedura: determinare quali tipi di documenti è possibile indicizzare  
 Eseguire una query sulla vista del catalogo [sys.fulltext_document_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).  
  
 Se il tipo di documento che si desidera indicizzare non è nell'elenco di tipi supportati, può essere necessario individuare, scaricare e installare filtri aggiuntivi. Per altre informazioni, vedere [Visualizzazione o modifica di word breaker e filtri registrati](view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="best-practice-consider-creating-a-separate-filegroup-for-the-full-text-and-semantic-indexes"></a><a name="BestPracticeFilegroup"></a>Procedura consigliata: provare a creare un filegroup distinto per gli indici full-text e semantico  
 Valutare se creare un filegroup distinto per gli indici full-text e semantici se l'allocazione di spazio su disco costituisce un problema. Gli indici semantici vengono creati nello stesso filegroup dell'indice full-text. Un indice semantico completamente popolato può contenere una notevole quantità di dati.  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="problem-searching-on-specific-column-returns-no-results"></a><a name="IssueNoResults"></a>Problema: la ricerca in una colonna specifica non restituisce alcun risultato  
 **È possibile che sia stato specificato un LCID non Unicode per una lingua Unicode.**  
 È possibile abilitare l'indicizzazione semantica in un tipo di colonna non Unicode con un LCID per una lingua che include solo parole Unicode, ad esempio l'LCID 1049 per il russo. In questo caso, non verrà restituito alcun risultato dagli indici semantici in questa colonna.  
  
  
