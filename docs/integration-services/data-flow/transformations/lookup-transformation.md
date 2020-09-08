---
description: Trasformazione Ricerca
title: Trasformazione Ricerca | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.lookuptrans.f1
- sql13.dts.designer.lookuptransformation.general.f1
- sql13.dts.designer.lookuptransformation.referencetable.f1
- sql13.dts.designer.lookuptransformation.columns.f1
- sql13.dts.designer.lookuptransformation.advanced.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f6daf6002a66dcffc032e9953cf400f91d725d91
ms.sourcegitcommit: 827ad02375793090fa8fee63cc372d130f11393f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2020
ms.locfileid: "89480907"
---
# <a name="lookup-transformation"></a>Trasformazione Ricerca

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  La trasformazione Ricerca consente di eseguire ricerche unendo in join i dati contenuti nelle colonne di input con le colonne in un set di dati di riferimento. È possibile utilizzare la ricerca per accedere a informazioni aggiuntive in una tabella correlata basata sui valori presenti nelle colonne comuni.  
  
 Il set di dati di riferimento può essere un file di cache, una vista o una tabella esistente, una nuova tabella o il risultato di una query SQL. La trasformazione Ricerca utilizza una gestione connessione OLE DB o una gestione connessione cache per connettersi al set di dati di riferimento. Per altre informazioni, vedere [Gestione connessione OLE DB](../../../integration-services/connection-manager/ole-db-connection-manager.md) e [Gestione connessione della cache](../../../integration-services/data-flow/transformations/cache-connection-manager.md)  
  
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
  
-   Se non esiste una voce corrispondente nel set di dati di riferimento, non viene eseguito alcun join. Per impostazione predefinita, le righe senza voci corrispondenti vengono gestite come errori dalla trasformazione Ricerca. Tuttavia, è possibile configurare la trasformazione Ricerca per reindirizzare tali righe a un output senza corrispondenza.  
  
-   Se nella tabella di riferimento sono presenti più corrispondenze, la trasformazione Ricerca restituisce solo la prima corrispondenza restituita dalla query di ricerca. Se vengono rilevate più corrispondenze, viene generato un errore o un avviso nella trasformazione Ricerca solo se questa è stata configurata in modo da caricare l'intero set di dati di riferimento nella cache. In questo caso, viene generato un avviso quando vengono individuate più corrispondenze durante il riempimento della cache.  
  
 È possibile utilizzare anche join composti, ovvero unire in join più colonne nell'input della trasformazione alle colonne nel set di dati di riferimento. La trasformazione supporta colonne di join con qualsiasi tipo di dati, ad eccezione di DT_R4, DT_R8, DT_TEXT, DT_NTEXT o DT_IMAGE. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 I valori ottenuti dal set di dati di riferimento vengono in genere aggiunti all'output della trasformazione. La trasformazione Ricerca può ad esempio estrarre il nome di un prodotto da una tabella utilizzando un valore letto da una colonna di input e quindi aggiungere il nome del prodotto all'output della trasformazione. I valori ottenuti dalla tabella di riferimento possono sostituire i valori delle colonne o essere aggiunti a nuove colonne.  
  
 Nelle ricerche eseguite dalla trasformazione Ricerca viene fatta distinzione tra maiuscole e minuscole. Per evitare errori di ricerca causati dalle differenze tra maiuscole e minuscole all'interno dei dati, utilizzare la trasformazione Mappa caratteri per convertire i dati in maiuscolo o minuscolo. Successivamente, includere la funzione UPPER o LOWER nell'istruzione SQL che genera la tabella di riferimento. Per altre informazioni, vedere [Trasformazione Mappa caratteri](../../../integration-services/data-flow/transformations/character-map-transformation.md), [UPPER &#40;Transact-SQL&#41;](../../../t-sql/functions/upper-transact-sql.md) e [LOWER &#40;Transact-SQL&#41;](../../../t-sql/functions/lower-transact-sql.md).  
  
 La trasformazione Ricerca dispone degli input e degli output seguenti:  
  
-   Input.  
  
-   Output con corrispondenza. L'output con corrispondenza gestisce le righe nell'input della trasformazione che corrispondono ad almeno una voce nel set di dati di riferimento.  
  
-   Output nessuna corrispondenza. L'output senza corrispondenza gestisce le righe nell'input che non corrispondono ad almeno una voce nel set di dati di riferimento. Se si configura la trasformazione Ricerca in modo da gestire le righe senza corrispondenza come errori, le righe vengono reindirizzate all'output degli errori. In caso contrario, la trasformazione reindirizza tali righe all'output senza corrispondenza.  
  
-   Output degli errori.  
  
## <a name="caching-the-reference-dataset"></a>Memorizzazione nella cache del set di dati di riferimento  
 Una cache in memoria archivia il set di dati di riferimento e una tabella hash che indicizza i dati. La cache rimane in memoria fino a quando l'esecuzione del pacchetto non viene completata. È possibile salvare in modo permanente la cache in un file di cache (.caw).  
  
 Quando si rende la cache persistente in un file, il sistema carica la cache più velocemente. In questo modo le prestazioni della trasformazione Ricerca e del pacchetto vengono migliorate. È importante ricordare che quando si utilizza un file di cache, i dati utilizzati non sono aggiornati come quelli presenti nel database.  
  
 Di seguito sono elencati i vantaggi aggiuntivi del salvataggio permanente della cache in un file:  
  
-   ***Condividere il file di cache tra più pacchetti. Per altre informazioni, vedere***  [Implementazione di una trasformazione Ricerca in modalità Full Cache utilizzando la gestione connessione della cache](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)  ***.***  
  
-   Distribuire il file di cache con un pacchetto. ***È quindi possibile usare i dati su più computer.*** Per altre informazioni, vedere [Creazione e distribuzione di una cache per la trasformazione Ricerca](../../../integration-services/data-flow/transformations/create-and-deploy-a-cache-for-the-lookup-transformation.md).  
  
-   Utilizzare Origine file non elaborato per la lettura dei dati dal file di cache. Successivamente è possibile utilizzare gli altri componenti flusso di dati per trasformare o spostare i dati. Per ulteriori informazioni, vedere [Raw File Source](../../../integration-services/data-flow/raw-file-source.md).  
  
    > [!NOTE]  
    >  I file di cache creati o modificati tramite Destinazione file non elaborato non sono supportati dalla gestione connessione della cache.  
  
-   Eseguire operazioni e impostare attributi nel file di cache attraverso l'attività File system. Per altre informazioni, vedere [Attività File system](../../../integration-services/control-flow/file-system-task.md).  
  
 Di seguito sono indicate le opzioni di memorizzazione nella cache:  
  
-   Il set di dati di riferimento viene generato tramite una tabella, una vista o una query SQL e caricato quindi nella cache prima dell'esecuzione della trasformazione Ricerca. È possibile utilizzare la gestione connessione OLE DB per accedere al set di dati.  
  
     Tale opzione di memorizzazione nella cache è compatibile con l'opzione di memorizzazione nella cache completa disponibile per la trasformazione Ricerca in [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   Il set di dati di riferimento è generato da un'origine dati connessa nel flusso di dati o da un file di cache e viene caricato nella cache prima dell'esecuzione della trasformazione Ricerca. Per accedere al set di dati utilizzare la gestione connessione della cache e, facoltativamente, la trasformazione della cache. Per altre informazioni, vedere [Gestione connessione della cache](../../../integration-services/data-flow/transformations/cache-connection-manager.md) e [Trasformazione Cache](../../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   Il set di dati di riferimento viene generato utilizzando una tabella, una vista o una query SQL durante l'esecuzione della trasformazione Ricerca. Le righe con le voci corrispondenti nel set di dati di riferimento e le righe senza voci corrispondenti nel set di dati vengono caricate nella cache.  
  
     Quando viene superata la dimensione massima consentita per la memoria della cache, la trasformazione Ricerca rimuove automaticamente dalla cache le righe utilizzate meno frequentemente.  
  
     Tale opzione di memorizzazione nella cache è compatibile con l'opzione di memorizzazione nella cache parziale disponibile per la trasformazione Ricerca in [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   Il set di dati di riferimento viene generato utilizzando una tabella, una vista o una query SQL durante l'esecuzione della trasformazione Ricerca. Non sono memorizzati dati nella cache.  
  
     Tale opzione di memorizzazione nella cache è compatibile con l'opzione di non memorizzazione nella cache disponibile per la trasformazione Ricerca in [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] si comportano in modo diverso ai fini del confronto tra le stringhe. Se la trasformazione Ricerca è configurata per caricare il set di dati di riferimento nella cache prima dell'esecuzione della trasformazione Ricerca, in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] viene eseguito il confronto della ricerca nella cache. In caso contrario, l'operazione di ricerca usa un'istruzione SQL con parametri e in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene eseguito il confronto della ricerca. Ciò significa che la trasformazione Ricerca potrebbe restituire un diverso numero di corrispondenze dalla stessa tabella di ricerca in base al tipo di cache.  
  
## <a name="related-tasks"></a>Attività correlate  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice. Per informazioni dettagliate, vedere gli argomenti seguenti.  
  
-   [Implementare una ricerca in modalità No Cache o Partial Cache](../../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [Implementazione di una trasformazione Ricerca in modalità Full Cache utilizzando la gestione connessione della cache](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [Implementare una trasformazione Ricerca in modalità Full Cache tramite la gestione connessione OLE DB](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Video [Procedura: Implementazione di una trasformazione Ricerca nella modalità Full Cache](https://go.microsoft.com/fwlink/?LinkId=131031)sul sito Web all'indirizzo msdn.microsoft.com  
  
-   Intervento nel blog relativo alle [procedure consigliate per l'utilizzo della trasformazione Ricerca nelle modalità cache](https://go.microsoft.com/fwlink/?LinkId=146623)sul sito Web all'indirizzo blogs.msdn.com  
  
-   Intervento nel blog relativo allo [schema di ricerca che non è sensibile alle maiuscole](https://go.microsoft.com/fwlink/?LinkId=157782)sul sito Web all'indirizzo blogs.msdn.com  
  
-   Esempio [trasformazione Ricerca](https://go.microsoft.com/fwlink/?LinkId=267528), su msftisprodsamples.codeplex.com.  
  
     Per informazioni sull'installazione di esempi del prodotto e database di esempio di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , vedere [Esempi del prodotto SQL Server Integration Services](https://go.microsoft.com/fwlink/?LinkId=267527).  
  
## <a name="lookup-transformation-editor-general-page"></a>Editor trasformazione Ricerca (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo Editor trasformazione Ricerca per selezionare la modalità di cache, selezionare il tipo di connessione e specificare la modalità di gestione delle righe senza voci corrispondenti.  
  
### <a name="options"></a>Opzioni  
 **Full Cache**  
 Generare e caricare il set di dati di riferimento nella cache prima dell'esecuzione della trasformazione Ricerca.  
  
 **Partial Cache**  
 Generare il set di dati di riferimento durante l'esecuzione della trasformazione Ricerca. Caricare le righe con le voci corrispondenti nel set di dati di riferimento e le righe senza voci corrispondenti nel set di dati nella cache.  
  
 **No Cache**  
 Generare il set di dati di riferimento durante l'esecuzione della trasformazione Ricerca. Non sono stati caricati dati in cache.  
  
 **Gestione connessione della cache**  
 Configurare la trasformazione Ricerca per l'utilizzo della gestione connessione della cache. L'opzione è disponibile solo se è stata selezionata anche l'opzione Full Cache.  
  
 **Gestione connessione OLE DB**  
 Configurare la trasformazione Ricerca per l'utilizzo della gestione connessione OLE DB.  
  
 **Specificare come gestire le righe senza voci corrispondenti**  
 Selezionare un'opzione per la gestione delle righe che non dispongono di almeno una voce corrispondente nel set di dati di riferimento.  
  
 Quando si seleziona **Reindirizza righe all'output nessuna corrispondenza**, le righe vengono reindirizzate a un output senza corrispondenze e non vengono gestite come errori. L'opzione **Errore** nella pagina **Output errori** della finestra di dialogo **Editor trasformazione Ricerca** non è disponibile.  
  
 Quando si seleziona un'altra opzione nella casella di riepilogo **Specificare come gestire le righe senza voci corrispondenti** , le righe vengono gestite come errori. L'opzione **Errore** nella pagina **Output errori** è disponibile.  
  
### <a name="external-resources"></a>Risorse esterne  
 Intervento nel blog sulle [modalità cache di ricerca](https://www.timmitchell.net/post/2019/09/05/ssis-lookup-cache-modes/) su blogs.msdn.com  
  
## <a name="lookup-transformation-editor-connection-page"></a>Editor trasformazione Ricerca (pagina Connessione)
  Usare la pagina **Connessione** della finestra di dialogo **Editor trasformazione Ricerca** per selezionare una gestione connessione. Se si seleziona una gestione connessione OLE DB, viene anche selezionata anche una query, una tabella o una vista per generare il set di dati di riferimento.  
  
### <a name="options"></a>Opzioni  
 Le opzioni seguenti sono disponibili quando si selezionano **Full cache** e **Gestione connessione della cache** nella pagina Generale della finestra di dialogo **Editor trasformazione Ricerca** .  
  
 **Gestione connessione della cache**  
 Selezionare una gestione connessione della cache esistente nell'elenco o fare clic su **Nuova**per creare una nuova connessione.  
  
 **Nuovo**  
 Consente di creare una nuova gestione connessione nella finestra di dialogo **Editor gestione connessione della cache** .  
  
 Le opzioni seguenti sono disponibili quando si selezionano **Full cache**, **Partial cache**o **No cache**e **Gestione connessione OLE DB**nella pagina Generale della finestra di dialogo **Editor trasformazione Ricerca** .  
  
 **Gestione connessione OLE DB**  
 Selezionare una gestione connessione OLE DB esistente nell'elenco o fare clic su **Nuova**per creare una nuova connessione.  
  
 **Nuovo**  
 Consente di creare una nuova connessione usando la finestra di dialogo **Configura gestione connessione OLE DB** .  
  
 **Tabella o vista**  
 Consente di selezionare una tabella o vista esistente nell'elenco o di creare una nuova tabella facendo clic su **Nuova**.  
  
> [!NOTE]  
>  Se si specifica un'istruzione SQL nella pagina **Avanzate** di **Editor trasformazione Ricerca**, tale istruzione sostituisce il nome di tabella selezionato, in quanto ha priorità su di esso. Per altre informazioni, vedere [Editor trasformazione Ricerca &#40;pagina Avanzate&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md).  
  
 **Nuovo**  
 Consente di creare una nuova tabella usando la finestra di dialogo **Crea tabella** .  
  
 **Usa i risultati di una query SQL**  
 Questa opzione consente di visualizzare una query preesistente, compilare una nuova query, controllare la sintassi della query e visualizzare in anteprima i risultati della query.  
  
 **Compila query**  
 Consente di creare l'istruzione Transact-SQL da usare per l'esecuzione tramite **Generatore query**, uno strumento grafico usato per creare query tramite la visualizzazione dei dati.  
  
 **Sfoglia**  
 Utilizzare questa opzione per visualizzare una query preesistente salvata in un file.  
  
 **Analizza query**  
 Consente di controllare la sintassi della query.  
  
 **Anteprima**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Anteprima risultati query** . Questa opzione consente di visualizzare fino a 200 righe.  
  
### <a name="external-resources"></a>Risorse esterne  
 Intervento nel blog sulle [modalità cache di ricerca](https://www.timmitchell.net/post/2019/09/05/ssis-lookup-cache-modes/) su blogs.msdn.com  
  
## <a name="lookup-transformation-editor-columns-page"></a>Editor trasformazione Ricerca (pagina Colonne)
  Utilizzare la pagina **Colonne** della finestra di dialogo **Editor trasformazione Ricerca** per specificare il join tra la tabella di origine e la tabella di riferimento e selezionare colonne di ricerca nella tabella di riferimento.  
  
### <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di visualizzare l'elenco delle colonne di input disponibili. Le colonne di input sono le colonne nel flusso di dati provenienti da un'origine connessa. Le colonne di input e le colonne di ricerca devono contenere tipi di dati corrispondenti.  
  
 Effettuare un'operazione di trascinamento della selezione per eseguire il mapping delle colonne di input disponibili alle colonne di ricerca.  
  
 È anche possibile eseguire il mapping delle colonne di input alle colonne di ricerca mediante la tastiera, evidenziando una colonna nella tabella **Colonne di input disponibili** , premendo il tasto MENU SCELTA RAPIDA, quindi facendo clic su **Modifica mapping**.  
  
 **Colonne di ricerca disponibili**  
 Consente di visualizzare l'elenco delle colonne di ricerca. Le colonne di ricerca sono colonne nella tabella di riferimento nelle quali si desidera cercare i valori corrispondenti alle colonne di input.  
  
 Eseguire un'operazione di trascinamento della selezione per eseguire il mapping delle colonne di ricerca disponibili alle colonne di input.  
  
 Utilizzare le caselle di controllo per selezionare le colonne di ricerca nella tabella di riferimento su cui eseguire operazioni di ricerca.  
  
 È anche possibile eseguire il mapping delle colonne di ricerca alle colonne di input mediante la tastiera, evidenziando una colonna nella tabella **Colonne di ricerca disponibili** , premendo il tasto MENU SCELTA RAPIDA, quindi facendo clic su **Modifica mapping**.  
  
 **Colonna di ricerca**  
 Consente di visualizzare le colonne di ricerca selezionate. Le selezioni effettuate vengono riflesse nelle selezioni delle caselle di controllo nella tabella **Colonne di ricerca disponibili** .  
  
 **Operazione di ricerca**  
 Consente di selezionare un'operazione di ricerca da eseguire sulla colonna di ricerca.  
  
 **Alias di output**  
 Consente di digitare un alias per l'output relativo a ogni colonna di ricerca. Per impostazione predefinita viene suggerito il nome della colonna di ricerca. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
## <a name="lookup-transformation-editor-advanced-page"></a>Editor trasformazione Ricerca (pagina Avanzate)
  La pagina **Avanzate** della finestra di dialogo **Editor trasformazione Ricerca** consente di configurare la memorizzazione nella cache parziale e di modificare l'istruzione SQL della trasformazione Ricerca.  
  
### <a name="options"></a>Opzioni  
 **Dimensioni cache (32 bit)**  
 Consente di regolare le dimensioni della cache (in megabyte) per i computer a 32 bit. Il valore predefinito è 5 MB.  
  
 **Dimensioni cache (64 bit)**  
 Consente di regolare le dimensioni della cache (in megabyte) per i computer a 64 bit. Il valore predefinito è 5 MB.  
  
 **Attivare cache per righe senza voci corrispondenti**  
 Consente di memorizzare nella cache le righe senza voci corrispondenti nel set di dati di riferimento.  
  
 **Allocazione dalla cache**  
 Consente di specificare la percentuale della cache da allocare per le righe senza voci corrispondenti nel set di dati di riferimento.  
  
 **Modifica istruzione SQL**  
 Consente di modificare l'istruzione SQL utilizzata per generare il set di dati di riferimento.  
  
> [!NOTE]  
>  L'istruzione SQL facoltativa specificata in questa pagina sostituisce il nome tabella specificato nella pagina **Connessione** di **Editor trasformazione Ricerca**. Per altre informazioni, vedere [Editor trasformazione Ricerca &#40;pagina Connessione&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md).  
  
 **Impostazione dei parametri**  
 Consente di eseguire il mapping delle colonne di input ai parametri mediante la finestra di dialogo **Imposta parametri query** .  
  
### <a name="external-resources"></a>Risorse esterne  
 Intervento nel blog sulle [modalità cache di ricerca](https://www.timmitchell.net/post/2019/09/05/ssis-lookup-cache-modes/) su blogs.msdn.com  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Ricerca fuzzy](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Trasformazione Ricerca termini](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)   
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
