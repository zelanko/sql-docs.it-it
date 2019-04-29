---
title: Trasformazione Ricerca | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptrans.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47b04c547700eda94d4c4f19b4a1211f8cdbf694
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900242"
---
# <a name="lookup-transformation"></a>Trasformazione Ricerca
  La trasformazione Ricerca consente di eseguire ricerche unendo in join i dati contenuti nelle colonne di input con le colonne in un set di dati di riferimento. È possibile utilizzare la ricerca per accedere a informazioni aggiuntive in una tabella correlata basata sui valori presenti nelle colonne comuni.  
  
 Il set di dati di riferimento può essere un file di cache, una vista o una tabella esistente, una nuova tabella o il risultato di una query SQL. La trasformazione Ricerca utilizza una gestione connessione OLE DB o una gestione connessione cache per connettersi al set di dati di riferimento. Per altre informazioni, vedere [Gestione connessione OLE DB](../../connection-manager/ole-db-connection-manager.md) e [Gestione connessione della cache](../../connection-manager/cache-connection-manager.md)  
  
 Per configurare la trasformazione Ricerca, procedere nel modo seguente:  
  
-   Selezionare la gestione connessione che si desidera utilizzare. Se si desidera eseguire la connessione a un database, selezionare una gestione connessione OLE DB. Se si desidera eseguire una connessione a un file di cache, selezionare una gestione connessione della cache.  
  
-   Specificare la tabella o la vista che contiene il set di dati di riferimento.  
  
-   Generare un set di dati di riferimento specificando un'istruzione SQL.  
  
-   Specificare i join tra il set di dati di input e quello di riferimento.  
  
-   Aggiungere le colonne dal set di dati di riferimento all'output della trasformazione Ricerca.  
  
-   Configurare le opzioni di memorizzazione nella cache.  
  
 La trasformazione Ricerca supporta i provider del database seguenti per la gestione connessione OLE DB:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Oracle  
  
-   DB2  
  
 La trasformazione Ricerca tenta di eseguire un equijoin tra i valori nell'input della trasformazione e quelli nel set di dati di riferimento. Questo significa che a ogni riga nell'input della trasformazione deve corrispondere almeno una riga nel set di dati di riferimento. Se non è possibile eseguire un equijoin, viene eseguita una delle azioni seguenti:  
  
-   Se non esiste una voce corrispondente nel set di dati di riferimento, non viene eseguito alcun join. Per impostazione predefinita, le righe senza voci corrispondenti vengono gestite come errori dalla trasformazione Ricerca. Tuttavia, è possibile configurare la trasformazione Ricerca per reindirizzare tali righe a un output senza corrispondenza. Per altre informazioni, vedere [Editor trasformazione Ricerca &#40;pagina Generale&#41;](../../lookup-transformation-editor-general-page.md) e [Editor trasformazione Ricerca &#40;pagina Output degli errori&#41;](../../lookup-transformation-editor-error-output-page.md).  
  
-   Se nella tabella di riferimento sono presenti più corrispondenze, la trasformazione Ricerca restituisce solo la prima corrispondenza restituita dalla query di ricerca. Se vengono rilevate più corrispondenze, viene generato un errore o un avviso nella trasformazione Ricerca solo se questa è stata configurata in modo da caricare l'intero set di dati di riferimento nella cache. In questo caso, viene generato un avviso quando vengono individuate più corrispondenze durante il riempimento della cache.  
  
 È possibile utilizzare anche join composti, ovvero unire in join più colonne nell'input della trasformazione alle colonne nel set di dati di riferimento. La trasformazione supporta colonne di join con qualsiasi tipo di dati, ad eccezione di DT_R4, DT_R8, DT_TEXT, DT_NTEXT o DT_IMAGE. Per altre informazioni, vedere [Tipi di dati di Integration Services](../integration-services-data-types.md).  
  
 I valori ottenuti dal set di dati di riferimento vengono in genere aggiunti all'output della trasformazione. La trasformazione Ricerca può ad esempio estrarre il nome di un prodotto da una tabella utilizzando un valore letto da una colonna di input e quindi aggiungere il nome del prodotto all'output della trasformazione. I valori ottenuti dalla tabella di riferimento possono sostituire i valori delle colonne o essere aggiunti a nuove colonne.  
  
 Nelle ricerche eseguite dalla trasformazione Ricerca viene fatta distinzione tra maiuscole e minuscole. Per evitare errori di ricerca causati dalle differenze tra maiuscole e minuscole all'interno dei dati, utilizzare la trasformazione Mappa caratteri per convertire i dati in maiuscolo o minuscolo. Successivamente, includere la funzione UPPER o LOWER nell'istruzione SQL che genera la tabella di riferimento. Per altre informazioni, vedere [Trasformazione Mappa caratteri](character-map-transformation.md), [UPPER &#40;Transact-SQL&#41;](/sql/t-sql/functions/upper-transact-sql) e [LOWER &#40;Transact-SQL&#41;](/sql/t-sql/functions/lower-transact-sql).  
  
 La trasformazione Ricerca dispone degli input e degli output seguenti:  
  
-   Input.  
  
-   Output con corrispondenza. L'output con corrispondenza gestisce le righe nell'input della trasformazione che corrispondono ad almeno una voce nel set di dati di riferimento.  
  
-   Output nessuna corrispondenza. L'output senza corrispondenza gestisce le righe nell'input che non corrispondono ad almeno una voce nel set di dati di riferimento. Se si configura la trasformazione Ricerca in modo da gestire le righe senza corrispondenza come errori, le righe vengono reindirizzate all'output degli errori. In caso contrario, la trasformazione reindirizza tali righe all'output senza corrispondenza.  
  
    > [!NOTE]  
    >  In [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)], la trasformazione Ricerca disponeva solo di un output. Per altre informazioni su come eseguire una trasformazione ricerca creata in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], vedere [aggiornare le trasformazioni ricerca](../../../sql-server/install/upgrade-lookup-transformations.md).  
  
-   Output degli errori.  
  
## <a name="caching-the-reference-dataset"></a>Memorizzazione nella cache del set di dati di riferimento  
 Una cache in memoria archivia il set di dati di riferimento e una tabella hash che indicizza i dati. La cache rimane in memoria fino a quando l'esecuzione del pacchetto non viene completata. È possibile salvare in modo permanente la cache in un file di cache (.caw).  
  
 Quando si rende la cache persistente in un file, il sistema carica la cache più velocemente. In questo modo le prestazioni della trasformazione Ricerca e del pacchetto vengono migliorate. È importante ricordare che quando si utilizza un file di cache, i dati utilizzati non sono aggiornati come quelli presenti nel database.  
  
 Di seguito sono elencati i vantaggi aggiuntivi del salvataggio permanente della cache in un file:  
  
-   ***Condividere il file di cache tra più pacchetti. Per altre informazioni, vedere***   [Implementazione di una trasformazione Ricerca in modalità Full Cache utilizzando la gestione connessione della cache](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  ***.***  
  
-   Distribuire il file di cache con un pacchetto. ***È quindi possibile usare i dati su più computer.*** Per altre informazioni, vedere [Creazione e distribuzione di una cache per la trasformazione Ricerca](create-and-deploy-a-cache-for-the-lookup-transformation.md).  
  
-   Utilizzare Origine file non elaborato per la lettura dei dati dal file di cache. Successivamente è possibile utilizzare gli altri componenti flusso di dati per trasformare o spostare i dati. Per ulteriori informazioni, vedere [Raw File Source](../raw-file-source.md).  
  
    > [!NOTE]  
    >  I file di cache creati o modificati tramite Destinazione file non elaborato non sono supportati dalla gestione connessione della cache.  
  
-   Eseguire operazioni e impostare attributi nel file di cache attraverso l'attività File system. Per altre informazioni, vedere [Attività File system](../../control-flow/file-system-task.md).  
  
 Di seguito sono indicate le opzioni di memorizzazione nella cache:  
  
-   Il set di dati di riferimento viene generato tramite una tabella, una vista o una query SQL e caricato quindi nella cache prima dell'esecuzione della trasformazione Ricerca. È possibile utilizzare la gestione connessione OLE DB per accedere al set di dati.  
  
     Tale opzione di memorizzazione nella cache è compatibile con l'opzione di memorizzazione nella cache completa disponibile per la trasformazione Ricerca in [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   Il set di dati di riferimento è generato da un'origine dati connessa nel flusso di dati o da un file di cache e viene caricato nella cache prima dell'esecuzione della trasformazione Ricerca. Per accedere al set di dati utilizzare la gestione connessione della cache e, facoltativamente, la trasformazione della cache. Per altre informazioni, vedere [Gestione connessione della cache](../../connection-manager/cache-connection-manager.md) e [Trasformazione Cache](cache-transform.md).  
  
-   Il set di dati di riferimento viene generato utilizzando una tabella, una vista o una query SQL durante l'esecuzione della trasformazione Ricerca. Le righe con le voci corrispondenti nel set di dati di riferimento e le righe senza voci corrispondenti nel set di dati vengono caricate nella cache.  
  
     Quando viene superata la dimensione massima consentita per la memoria della cache, la trasformazione Ricerca rimuove automaticamente dalla cache le righe utilizzate meno frequentemente.  
  
     Tale opzione di memorizzazione nella cache è compatibile con l'opzione di memorizzazione nella cache parziale disponibile per la trasformazione Ricerca in [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   Il set di dati di riferimento viene generato utilizzando una tabella, una vista o una query SQL durante l'esecuzione della trasformazione Ricerca. Non sono memorizzati dati nella cache.  
  
     Tale opzione di memorizzazione nella cache è compatibile con l'opzione di non memorizzazione nella cache disponibile per la trasformazione Ricerca in [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] si comportano in modo diverso ai fini del confronto tra le stringhe. Se la trasformazione Ricerca è configurata per caricare il set di dati di riferimento nella cache prima dell'esecuzione della trasformazione Ricerca, in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] viene eseguito il confronto della ricerca nella cache. In caso contrario, l'operazione di ricerca usa un'istruzione SQL con parametri e in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene eseguito il confronto della ricerca. Ciò significa che la trasformazione Ricerca potrebbe restituire un diverso numero di corrispondenze dalla stessa tabella di ricerca in base al tipo di cache.  
  
## <a name="related-tasks"></a>Attività correlate  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice. Per informazioni dettagliate, vedere gli argomenti seguenti.  
  
-   [Implementazione di una ricerca in modalità No Cache o Partial Cache](implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [Implementare una trasformazione Ricerca in modalità Full Cache tramite la gestione connessione della cache](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [Implementazione di una trasformazione Ricerca in modalità Full cache utilizzando la gestione connessione OLE DB](../../connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Video [Procedura: Implementazione di una trasformazione Ricerca nella modalità Full Cache](https://go.microsoft.com/fwlink/?LinkId=131031) in msdn.microsoft.com  
  
-   Intervento nel blog relativo alle [procedure consigliate per l'utilizzo della trasformazione Ricerca nelle modalità cache](https://go.microsoft.com/fwlink/?LinkId=146623)sul sito Web all'indirizzo blogs.msdn.com  
  
-   Post di blog [Lookup Pattern: Case Insensitive](https://go.microsoft.com/fwlink/?LinkId=157782) (Modello di ricerca senza distinzione tra maiuscole e minuscole) in blogs.msdn.com  
  
-   Esempio [trasformazione Ricerca](https://go.microsoft.com/fwlink/?LinkId=267528), su msftisprodsamples.codeplex.com.  
  
     Per informazioni sull'installazione di esempi del prodotto e database di esempio di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , vedere [Esempi del prodotto SQL Server Integration Services](https://go.microsoft.com/fwlink/?LinkId=267527).  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Ricerca fuzzy](fuzzy-lookup-transformation.md)   
 [Trasformazione Ricerca termini](term-lookup-transformation.md)   
 [Flusso di dati](../data-flow.md)   
 [Trasformazioni di Integration Services](integration-services-transformations.md)  
  
  
