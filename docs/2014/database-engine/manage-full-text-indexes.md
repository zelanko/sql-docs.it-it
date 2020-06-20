---
title: Gestire indici full-text | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: 28ff17dc-172b-4ac4-853f-990b5dc02fd1
author: rothja
ms.author: jroth
ms.openlocfilehash: 92eb3669930407b359b8eeed4d3df2e802bdacdf
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930947"
---
# <a name="manage-full-text-indexes"></a>Gestione di indici full-text.
     
##  <a name="viewing-and-changing-the-properties-of-a-full-text-index"></a><a name="view"></a>Visualizzazione e modifica delle proprietà di un indice full-text  
  
#### <a name="to-view-or-change-the-properties-of-a-full-text-index-in-management-studio"></a>Per visualizzare o modificare le proprietà di un indice full-text in Management Studio  
  
1.  In Esplora oggetti espandere il server.  
  
2.  Espandere **Database**e quindi il database contenente l'indice full-text.  
  
3.  Espandere **Tabelle**.  
  
4.  Fare clic con il pulsante destro del mouse sulla tabella in cui viene definito l'indice full-text, scegliere **Indice full-text**e quindi **Proprietà** dal menu di scelta rapida **Indice full-text**. Verrà visualizzata la finestra di dialogo **Proprietà indice full-text** .  
  
5.  Nel riquadro **Seleziona una pagina** è possibile selezionare le pagine seguenti:  
  
    |Pagina|Descrizione|  
    |----------|-----------------|  
    |**Generale**|Sono contenute le proprietà di base dell'indice full-text, incluse diverse proprietà modificabili e alcune proprietà non modificabili quali il nome del database, il nome della tabella e il nome della colonna chiave full-text. Le proprietà modificabili sono le seguenti:<br /><br /> **Elenco di parole non significative indice full-text**<br /><br /> **Indicizzazione full-text abilitata**<br /><br /> **Rilevamento delle modifiche**<br /><br /> **Elenco delle proprietà di ricerca**<br /><br /> <br /><br /> Per altre informazioni, vedere [Proprietà indice full-text &#40;pagina Generale&#41;](full-text-index-properties-general-page.md).|  
    |**Colonne**|Consente di visualizzare le colonne della tabella disponibili per l'indicizzazione full-text. La colonna o le colonne selezionate contengono indici full-text. È possibile selezionare il numero desiderato di colonne disponibili da includere nell'indice full-text. Per altre informazioni, vedere [Proprietà indice full-text &#40;pagina Colonne&#41;](../../2014/database-engine/full-text-index-properties-columns-page.md).|  
    |**Pianificazioni**|Utilizzare questa pagina per creare o gestire le pianificazioni per un processo di SQL Server Agent che consente di avviare un popolamento incrementale della tabella per i popolamenti dell'indice full-text. Per altre informazioni sugli indici full-text, vedere [Popolamento degli indici full-text](../relational-databases/indexes/indexes.md).<br /><br /> <strong> \* \* Importante \* dopo \* </strong> aver chiuso la finestra di dialogo **Proprietà indice full-text** , eventuali nuove pianificazioni vengono associate a un processo di SQL Server Agent (avvio del popolamento incrementale della tabella su *database_name*.* table_name*).|  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)] per salvare le modifiche e uscire dalla finestra di dialogo **Proprietà indice full-text**.  
  
##  <a name="viewing-the-properties-of-indexed-tables-and-columns"></a><a name="props"></a>Visualizzazione delle proprietà di tabelle e colonne indicizzate  
 Per ottenere il valore di diverse proprietà di indicizzazione full-text, è possibile utilizzare varie funzioni [!INCLUDE[tsql](../includes/tsql-md.md)] come OBJECTPROPERTYEX. Queste informazioni sono utili per l'amministrazione e la risoluzione dei problemi relativi alla ricerca full-text.  
  
 Nella tabella seguente sono elencate le proprietà full-text relative a tabelle e colonne indicizzate e le funzioni [!INCLUDE[tsql](../includes/tsql-md.md)] correlate.  
  
|Proprietà|Descrizione|Funzione|  
|--------------|-----------------|--------------|  
|`FullTextTypeColumn`|TYPE COLUMN nella tabella in cui sono contenute le informazioni sui tipi di documenti della colonna.|[COLUMNPROPERTY](/sql/t-sql/functions/columnproperty-transact-sql)|  
|`IsFulltextIndexed`|Indica se una colonna è stata abilitata per l'indicizzazione full-text.|COLUMNPROPERTY|  
|`IsFulltextKey`|Indica se l'indice è la chiave full-text di una tabella.|[INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql)|  
|**TableFulltextBackgroundUpdateIndexOn**|Indica se per una tabella è stata impostata l'indicizzazione full-text degli aggiornamenti in background.|[OBJECTPROPERTYEX](/sql/t-sql/functions/objectproperty-transact-sql)|  
|`TableFulltextCatalogId`|ID del catalogo full-text contenente i dati dell'indice full-text per la tabella.|OBJECTPROPERTYEX|  
|`TableFulltextChangeTrackingOn`|Indica se per la tabella è abilitato il rilevamento delle modifiche full-text.|OBJECTPROPERTYEX|  
|`TableFulltextDocsProcessed`|Numero di righe elaborate dopo l'avvio dell'indicizzazione full-text.|OBJECTPROPERTYEX|  
|**TableFulltextFailCount**|Numero di righe non indicizzate dalla ricerca full-text.|OBJECTPROPERTYEX|  
|**TableFulltextItemCount**|Numero di righe per cui l'indicizzazione full-text ha avuto esito positivo.|OBJECTPROPERTYEX|  
|`TableFulltextKeyColumn`|ID della colonna chiave univoca full-text.|OBJECTPROPERTYEX|  
|`TableFullTextMergeStatus`|Indica se in una tabella che dispone di un indice full-text è attualmente in corso un'operazione di unione.|OBJECTPROPERTYEX|  
|**TableFulltextPendingChanges**|Numero di voci in sospeso del rilevamento delle modifiche da elaborare.|OBJECTPROPERTYEX|  
|`TableFulltextPopulateStatus`|Stato popolamento di una tabella full-text.|OBJECTPROPERTYEX|  
|`TableHasActiveFulltextIndex`|Indica se una tabella include un indice full-text attivo.|OBJECTPROPERTYEX|  
  
##  <a name="getting-information-about-the-full-text-key-column"></a><a name="key"></a>Recupero di informazioni sulla colonna chiave full-text  
 In genere, il risultato della funzione con valori del set di righe CONTAINSTABLE o FREETEXTTABLE deve essere unito in join alla tabella di base. In questi casi, è necessario conoscere il nome della colonna chiave univoca. È possibile verificare se un determinato indice univoco viene utilizzato come chiave full-text e ottenere l'identificatore della colonna chiave full-text.  
  
#### <a name="to-inquire-whether-a-given-unique-index-is-used-as-the-full-text-key-column"></a>Per verificare se un determinato indice univoco viene utilizzato come colonna chiave full-text  
  
1.  Usare un'istruzione [SELECT](/sql/t-sql/queries/select-transact-sql) per chiamare la funzione [INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql). Nella chiamata di funzione utilizzare la funzione OBJECT_ID per convertire il nome della tabella (*table_name*) nell'ID tabella, specificare il nome di un indice univoco per la tabella e specificare la `IsFulltextKey` proprietà di indice, come indicato di seguito:  
  
    ```  
    SELECT INDEXPROPERTY( OBJECT_ID('table_name'), 'index_name',  'IsFulltextKey' );  
    ```  
  
     L'istruzione restituisce 1 se l'indice viene utilizzato per applicare l'unicità della colonna chiave full-text e 0 in caso contrario.  
  
 **Esempio**  
  
 Nell'esempio seguente viene illustrato come verificare se l'indice `PK_Document_DocumentID` viene utilizzato per applicare l'univocità della colonna chiave full-text:  
  
```  
USE AdventureWorks  
GO  
SELECT INDEXPROPERTY ( OBJECT_ID('Production.Document'), 'PK_Document_DocumentID',  'IsFulltextKey' )  
```  
  
 In questo esempio viene restituito 1 se l'indice `PK_Document_DocumentID` viene utilizzato per applicare l'univocità della colonna chiave full-text. In caso contrario, viene restituito 0 o NULL. NULL indica che è in uso un nome di indice non valido, il nome dell'indice non corrisponde alla tabella, la tabella non esiste e così via.  
  
#### <a name="to-find-the-identifier-of-the-full-text-key-column"></a>Per trovare l'identificatore della colonna chiave full-text  
  
1.  Ogni tabella abilitata per la funzionalità full-text include una colonna che viene usata per applicare righe univoche per la tabella (la *colonna chiave**univoca*). La proprietà `TableFulltextKeyColumn`, ottenuta dalla funzione OBJECTPROPERTYEX contiene l'ID della colonna chiave univoca.  
  
     Per ottenere questo identificatore, è possibile utilizzare un'istruzione SELECT per chiamare la funzione OBJECTPROPERTYEX. Utilizzare la funzione OBJECT_ID per convertire il nome della tabella (*table_name*) nell'ID della tabella e specificare la `TableFulltextKeyColumn` proprietà, come indicato di seguito:  
  
    ```  
    SELECT OBJECTPROPERTYEX(OBJECT_ID( 'table_name'), 'TableFulltextKeyColumn' ) AS 'Column Identifier';  
    ```  
  
 **esempi**  
  
 Nell'esempio seguente viene restituito l'identificatore della colonna chiave full-text o NULL. NULL indica che è in uso un nome di indice non valido, il nome dell'indice non corrisponde alla tabella, la tabella non esiste e così via.  
  
```  
USE AdventureWorks;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('Production.Document'), 'TableFulltextKeyColumn');  
GO  
```  
  
 Nell'esempio seguente viene illustrato come utilizzare l'identificatore della colonna chiave univoca per ottenere il nome della colonna.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @key_column sysname  
SET @key_column = Col_Name(Object_Id('Production.Document'),  
ObjectProperty(Object_id('Production.Document'),  
'TableFulltextKeyColumn')   
)  
SELECT @key_column AS 'Unique Key Column';  
GO  
```  
  
 Nell'esempio viene restituita una colonna del set di risultati denominata `Unique Key Column`in cui viene visualizzata una sola riga contenente il nome della colonna chiave univoca della tabella Document, DocumentID. Si noti che se questa query contenesse un nome di indice non valido, il nome di indice non corrispondesse alla tabella, la tabella non esistesse e così via, il risultato restituito sarebbe NULL.  
  
##  <a name="disabling-or-re-enabling-a-table-for-full-text-indexing"></a><a name="disable"></a>Disabilitazione o riabilitazione di una tabella per l'indicizzazione full-text  
 Per impostazione predefinita, in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tutti i database creati dall'utente sono abilitati per la funzionalità full-text. Una tabella viene inoltre abilitata automaticamente per l'indicizzazione full-text dopo la creazione di un indice full-text nella tabella e l'aggiunta di una colonna all'indice. L'indicizzazione full-text viene disabilitata automaticamente nella tabella quando l'ultima colonna viene eliminata dall'indice full-text.  
  
 In una tabella che dispone di un indice full-text è possibile disabilitare o riabilitare manualmente una tabella per indicizzazione full-text utilizzando [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-enable-a-table-for-full-text-indexing"></a>Per abilitare una tabella per l'indicizzazione full-text  
  
1.  Espandere il gruppo di server, espandere **Database**, quindi il database contenente la tabella che si vuole abilitare per l'indicizzazione full-text.  
  
2.  Espandere **Tabelle**e fare clic con il pulsante destro del mouse sulla tabella che si vuole disabilitare o riabilitare per l'indicizzazione full-text.  
  
3.  Scegliere **Indice full-text**, quindi fare clic su **Disabilita indicizzazione full-text** o **Abilita indicizzazione full-text**.  
  
##  <a name="removing-a-full-text-index-from-a-table"></a><a name="remove"></a>Rimozione di un indice full-text da una tabella  
  
#### <a name="to-remove-a-full-text-index-from-a-table"></a>Per rimuovere un indice full-text da una tabella  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sulla tabella contenente l'indice full-text che si desidera eliminare.  
  
2.  Selezionare **Elimina indice full-text**.  
  
3.  Quando richiesto, fare clic su **OK** per confermare l'eliminazione dell'indice full-text.  
  
  
