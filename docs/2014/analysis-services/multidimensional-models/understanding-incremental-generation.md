---
title: Informazioni sulla generazione incrementale | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- incremental generation [Analysis Services]
- Schema Generation Wizard, incremental generation
- relational schema [Analysis Services], incremental generation
ms.assetid: 3ca0aa63-3eb5-4fe9-934f-8e96dee84eaa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ace9bbbbbc023d14dbce91a176f7d05ad19d699b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68811065"
---
# <a name="understanding-incremental-generation"></a>Informazioni sulla generazione incrementale
  Dopo la generazione iniziale dello schema, è possibile modificare le definizioni dei cubi e delle dimensioni mediante [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e quindi eseguire di nuovo la Generazione guidata schema. La procedura guidata aggiorna lo schema nel database dell'area di interesse e nella vista origine dati associata in base alle modifiche apportate, mantenendo i dati attualmente esistenti nelle tabelle da rigenerare nella misura massima consentita. Se dopo la generazione iniziale le tabelle sono state modificate, la Generazione guidata schema mantiene tali modifiche in base alle regole seguenti:  
  
-   Le tabelle generate in precedenza dalla procedura guidata vengono sovrascritte. Per evitare che una tabella generata dalla procedura guidata venga sovrascritta, impostare la proprietà `AllowChangesDuringGeneration` della tabella nella vista origine dati su `false`. Le tabelle di cui si assume il controllo tramite questa proprietà vengono trattate come qualsiasi altra tabella definita dall'utente e non subiscono modifiche durante la rigenerazione. Dopo avere escluso una tabella dalla generazione, è possibile reimpostare la proprietà `AllowChangesDuringGeneration` della tabella nella vista origine dati su `true` se si desidera che la procedura guidata implementi di nuovo le modifiche nella tabella. Per altre informazioni, vedere [Modificare le proprietà in una vista origine dati &#40;Analysis Services&#41;](change-properties-in-a-data-source-view-analysis-services.md).  
  
-   Le tabelle aggiunte alla vista origine dati o al database sottostante senza utilizzare la procedura guidata non vengono sovrascritte.  
  
 Quando la Generazione guidata schema rigenera le tabelle generate in precedenza nel database dell'area di interesse, è possibile scegliere di mantenere i dati esistenti in tali tabelle.  
  
## <a name="supporting-data-preservation"></a>Supporto del mantenimento dei dati  
 Come regola generale, la Generazione guidata schema mantiene i dati archiviati nelle tabelle generate. Inoltre, in caso di aggiunta di nuove colonne alle tabelle generate dalla procedura guidata, vengono mantenuti anche tali dati. Questa funzionalità può essere sfruttata per aggiungere o modificare le dimensioni e i cubi e quindi rigenerare gli oggetti sottostanti senza dover ricaricare i dati archiviati nelle tabelle sottostanti.  
  
> [!NOTE]  
>  Quando si caricano dati da file di testo delimitati, è inoltre possibile scegliere se la Generazione guidata schema dovrà sovrascrivere tali file e i dati in essi contenuti durante la rigenerazione. I file di testo possono essere solo sovrascritti completamente oppure non sovrascritti affatto in quanto la Generazione guidata schema non consente di sovrascrivere parzialmente tali file. Per impostazione predefinita, questi file non vengono sovrascritti.  
  
### <a name="partial-preservation"></a>Mantenimento parziale  
 In alcune circostanze la Generazione guidata schema non è in grado di mantenere i dati esistenti. Nella tabella seguente vengono descritte alcune situazioni esemplificative in cui non è possibile mantenere tutti i dati esistenti nelle tabelle sottostanti durante le rigenerazione.  
  
|Tipo di modifica dei dati|Modalità di gestione|  
|-------------------------|---------------|  
|Impostazione di un tipo di dati non compatibile|La Generazione guidata schema esegue conversioni standard dei tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ogniqualvolta possibile per convertire i dati esistenti da un tipo a un altro. Tuttavia, quando si sostituisce il tipo di dati di un attributo con un tipo non compatibile con i dati esistenti, i dati della colonna interessata vengono eliminati.|  
|Errori di integrità referenziale|Se si apporta a una dimensione o un cubo contenente dati una modifica che causa un errore di integrità referenziale durante la rigenerazione, la Generazione guidata schema eliminerà tutti i dati nella tabella della chiave esterna. L'eliminazione dei dati non è limitata alla colonna che ha causato la violazione del vincolo di chiave esterna o alle righe contenenti gli errori di integrità referenziale. Se, ad esempio, si modifica la chiave della dimensione impostando un attributo con dati non univoci o Null, verranno eliminati tutti i dati esistenti nella tabella della chiave esterna. Inoltre, l'eliminazione di tutti i dati di una tabella può provocare un effetto a catena e causare altre violazioni di integrità referenziale.|  
|Eliminazione di un attributo o una dimensione|Se si elimina un attributo da una dimensione, la Generazione guidata schema eliminerà la colonna mappata all'attributo eliminato. Se si elimina una dimensione, la procedura guidata eliminerà la tabella mappata alla dimensione eliminata. In questi casi, i dati contenuti nella colonna o nella tabella eliminata vengono rimossi.|  
  
 Prima di eliminare qualsiasi dato, la Generazione guidata schema visualizza un messaggio di avviso per consentire all'utente di annullare la procedura guidata senza perdere alcun dato. La Procedura guidata schema, tuttavia, non è in grado di distinguere le perdite di dati previste da quelle non previste. Quando si esegue la procedura guidata, le tabelle e le colonne contenenti dati che verranno eliminati vengono elencate in una finestra di dialogo. È possibile scegliere se continuare la procedura guidata ed eliminare i dati oppure se annullare la procedura guidata e ricontrollare le modifiche apportate alle tabelle e alle colonne.  
  
## <a name="supporting-cube-and-dimension-changes"></a>Supporto delle modifiche dei cubi e delle dimensioni  
 Quando si modificano le proprietà di dimensioni e cubi, la Generazione guidata schema rigenera gli oggetti appropriati nel database dell'area di interesse sottostante nonché nella vista origine dati correlata come descritto di seguito.  
  
 Eliminazione di un oggetto, ad esempio una dimensione, un cubo o un attributo.  
 La Generazione guidata schema elimina gli oggetti sottostanti a cui l'oggetto eliminato è mappato. L'aggiunta di nuove colonne a una tabella generata dalla procedura guidata non impedisce l'eliminazione della tabella. L'eliminazione di un oggetto comporta la rimozione dei dati archiviati negli oggetti sottostanti ed eventualmente anche di altri dati se si verificano errori di integrità referenziale.  
  
 Ridenominazione di un oggetto, ad esempio una dimensione, un cubo o un attributo.  
 La Generazione guidata schema rinomina gli oggetti sottostanti a cui l'oggetto rinominato è mappato. Vengono inoltre rinominati tutti gli oggetti interessati, ad esempio le chiavi primarie. I dati esistenti negli oggetti sottostanti vengono mantenuti.  
  
 Implementazione in un oggetto di una modifica, quale la sostituzione del tipo di dati.  
 La Generazione guidata schema modifica gli oggetti sottostanti a cui l'oggetto modificato è mappato. I dati esistenti negli oggetti sottostanti nei database vengono mantenuti, a meno che non esiste un problema di compatibilità tra il nuovo tipo di dati e i dati esistenti.  
  
 Aggiunta di un nuovo oggetto, ad esempio una dimensione, un cubo o un attributo.  
 La Generazione guidata schema aggiunge gli oggetti sottostanti a cui il nuovo oggetto è mappato.  
  
 Se la Generazione guidata schema non può implementare la modifica richiesta a causa di un errore restituito dal Motore di database per la presenza di un oggetto utente nel database dell'area di interesse, la procedura guidata verrà interrotta e verrà visualizzato l'errore restituito dal Motore di database. Se, ad esempio, si crea un vincolo PRIMARY KEY o un indice non cluster in una tabella dopo che la procedura guidata ha generato la tabella, la generazione guidata schema non elimina tale tabella perché non ha creato il vincolo o l'indice.  
  
## <a name="supporting-schema-changes"></a>Supporto delle modifiche dello schema  
 Quando si modificano le proprietà delle tabelle o delle colonne nel database dell'area di interesse o nella vista origine dati associata, la Generazione guidata schema gestisce le modifiche come descritto di seguito.  
  
 Eliminazione di una tabella o una colonna generata dalla Generazione guidata schema.  
 Se si elimina una tabella o una colonna generata dalla Generazione guidata schema, la procedura guidata rigenererà la tabella o la colonna eliminata e non verrà visualizzato alcun messaggio di avviso.  
  
 Modifica delle proprietà di una tabella o una colonna generata dalla Generazione guidata schema.  
 Se si modificano le proprietà di una tabella o una colonna generata dalla Generazione guidata schema, la procedura guidata rigenererà la tabella modificata senza la modifica. Se, ad esempio, si modifica il tipo di dati o il supporto di valori Null per una colonna oppure il filegroup di una tabella generata dalla Generazione guidata schema, la modifica non verrà mantenuta al termine della rigenerazione e non verrà visualizzato alcun messaggio di avviso.  
  
 Aggiunta di una colonna a una tabella generata dalla Generazione guidata schema o aggiunta di una tabella nel database dell'area di interesse o nel database dell'area di gestione temporanea.  
 Se si aggiunge una colonna a una tabella generata dalla Generazione guidata schema, la procedura guidata manterrà la colonna aggiuntiva nonché tutti i dati in essa archiviati durante la rigenerazione. Se, tuttavia, si aggiunge una tabella nel database dell'area di interesse o nel database dell'area di gestione temporanea, la nuova tabella non verrà incorporata. La colonna o la tabella aggiunta non viene inclusa nel progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , nel database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , nei pacchetti DTS, nella vista origine dati né in qualsiasi altra posizione dello schema generato.  
  
## <a name="supporting-data-source-and-data-source-view-changes"></a>Supporto delle modifiche dell'origine dei dati e della vista origine dati  
 Quando si riesegue la Generazione guidata schema, vengono riutilizzate la stessa origine dei dati e la stessa vista origine dati utilizzate durante la generazione originale. Se si aggiunge un'origine dei dati oppure una vista origine dati, il nuovo elemento verrà ignorato dalla procedura guidata. Se si elimina l'origine dei dati o la vista origine dati originale dopo la generazione iniziale, sarà necessario eseguire la procedura guidata dall'inizio. Verranno inoltre eliminate tutte le impostazioni precedenti della procedura guidata. Tutti gli oggetti esistenti in un database sottostante associati a un'origine dei dati o una vista origine dati eliminata verranno considerati come oggetti creati dall'utente durante la successiva esecuzione della Generazione guidata schema.  
  
 Se la vista origine dati non corrisponde allo stato effettivo del database sottostante al momento della generazione, è possibile che si verifichino errori durante la generazione degli schemi per il database dell'area di interesse e il database dell'area di gestione temporanea. Se, ad esempio, nella vista origine dati il tipo di dati di una colonna risulta `int` mentre il tipo di dati effettivo della colonna è `string`, la Generazione guidata schema imposterà il tipo di dati della chiave esterna su `int` in conformità con la vista origine dati e si verificherà un errore durante la creazione della relazione perché il tipo di dati effettivo è `string`.  
  
 Se invece si modifica la stringa di connessione dell'origine dei dati impostando un database diverso rispetto alla generazione precedente, non verrà generato alcun errore. Verrà utilizzato il nuovo database senza alcuna modifica al database precedente.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione delle modifiche a viste origine dati e origini dati](manage-changes-to-data-source-views-and-data-sources.md)   
 [Generazione guidata schema &#40;Analysis Services&#41;](schema-generation-wizard-analysis-services.md)  
  
  
