---
title: Gestione connessione file flat | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ffileconnection.general.f1
- sql13.dts.designer.ffileconnection.columns.f1
- sql13.dts.designer.ffileconnection.columnproperties.f1
- sql13.dts.designer.ffileconnection.preview.f1
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2cf3156597035241398e354e8c80bfebb9c16d67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728266"
---
# <a name="flat-file-connection-manager"></a>Flat File Connection Manager

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Una gestione connessione file flat consente a un pacchetto di accedere ai dati contenuti in un file flat. L'origine e la destinazione del file flat possono ad esempio utilizzare gestioni connessioni file flat per estrarre e caricare dati.  
  
 La gestione connessione file flat è in grado di accedere a un solo file. Per fare riferimento a più file, al posto di una gestione connessione file flat utilizzare una gestione connessione per più file flat. Per ulteriori informazioni, vedere [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="column-length"></a>Lunghezza di colonna  
 Per impostazione predefinita la gestione connessione file flat imposta la lunghezza delle colonne di tipo stringa su 50 caratteri. Nella finestra di dialogo **Editor gestione connessione file flat** è possibile valutare dati di esempio e modificare automaticamente la lunghezza di tali colonne in modo da evitare il troncamento dei dati o il superamento della larghezza massima delle colonne. La lunghezza di una colonna di tipo stringa rimane inoltre invariata per tutto il flusso di dati, a meno che non venga modificata successivamente in un'origine file flat o in una trasformazione. Se su tali colonne di tipo stringa viene eseguito il mapping a colonne di destinazione di larghezza inferiore, verrà visualizzato un avviso nell'interfaccia utente e in fase di esecuzione potrebbero verificarsi errori dovuti al troncamento dei dati. Per evitare errori o troncamenti, è possibile ridimensionare le colonne in modo che siano compatibili con le colonne di destinazione nella gestione connessione file flat, nell'origine file flat o in una trasformazione. Per modificare la lunghezza di una colonna di output, è necessario impostare la proprietà **Length** della colonna di output nella scheda **Proprietà input e output** della finestra di dialogo **Editor avanzato** .  
  
 Se, dopo avere aggiunto e configurato l'origine file flat che utilizza la gestione connessione, si modifica la lunghezza delle colonne nella gestione connessione file flat, non sarà necessario ridimensionare manualmente le colonne di output nell'origine file flat. Nella finestra di dialogo **Origine file flat** è disponibile un'opzione che consente di sincronizzare i metadati delle colonne per l'origine file flat.  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>Configurazione della gestione connessione file flat  
 Quando si aggiunge una gestione connessione file flat a un pacchetto, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene creata una gestione connessione che, in fase di esecuzione, verrà risolta in una connessione file flat, vengono impostate le proprietà della connessione file flat e viene aggiunta la gestione connessione file flat alla raccolta **Connessioni** del pacchetto.  
  
 La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **FLATFILE**.  
  
 Per impostazione predefinita, tramite la gestione connessione file flat viene sempre verificata la presenza di un delimitatore di riga in dati senza virgolette e viene iniziata una nuova riga quando viene individuato un relativo delimitatore. In questo modo, con la gestione connessione è possibile analizzare correttamente i file con righe prive di campi colonna.  
  
 In alcuni casi, la disabilitazione di questa funzionalità potrebbe migliorare le prestazioni del pacchetto. Questa funzionalità può essere disabilitata impostando la proprietà della gestione connessione file flat, **AlwaysCheckForRowDelimiters**, su **False**.  
  
 Per configurare la gestione connessione file flat, procedere nel modo seguente:  
  
-   Specificare il file, le impostazioni locali e la tabella codici da utilizzare. Le impostazioni locali vengono utilizzate per interpretare i dati con formato dipendente dalla lingua, come le date, mentre la tabella codici viene utilizzata per convertire i dati stringa in formato Unicode.  
  
-   Specificare il formato dei file. È possibile utilizzare un formato delimitato, a larghezza fissa o non allineato a destra.  
  
-   Specificare i delimitatori della riga di intestazione, delle righe di dati e delle colonne. I delimitatori delle colonne possono essere impostati a livello di file e sovrascritti a livello di colonna.  
  
-   Indicare se la prima riga del file contiene i nomi delle colonne.  
  
-   Specificare un qualificatore di testo. Ogni colonna può essere configurata in modo da riconoscere un qualificatore di testo.  
  
     La gestione connessione file flat supporta l'uso di un qualificatore di testo per incorporare quest'ultimo in una stringa qualificata. L'istanza doppia di un qualificatore di testo viene interpretata come una singola istanza letterale di questa stringa. Ad esempio, se il qualificatore di testo è una virgoletta singola e i dati di input sono 'abc', 'def', 'g'hi', i dati di output saranno abc, def, g'hi. Un'istanza di un qualificatore incorporato in una stringa qualificata provoca tuttavia l'esito negativo dell'origine file flat con l'errore DTS_E_PRIMEOUTPUTFAILED.
  
-   Impostare proprietà quali il nome, il tipo di dati e la larghezza massima delle singole colonne.  
  
 È possibile impostare la proprietà ConnectionString per la gestione connessione file flat specificando un'espressione nella finestra Proprietà di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per evitare errori di convalida, effettuare le operazioni seguenti.  
  
-   Quando si usa un'espressione per specificare il file, aggiungere il percorso del file nella casella **Nome file** nell' **Editor gestione connessione file flat**.  
  
-   Impostare la proprietà **DelayValidation** della gestione connessione file flat su **True**.  
  
 È possibile utilizzare un'espressione per creare un nome di file in fase di esecuzione utilizzando la gestione connessione file flat con la destinazione file flat.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="flat-file-connection-manager-editor-general-page"></a>Editor gestione connessione file flat (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo **Editor gestione connessione file flat** per selezionare un file e un formato di dati. Una connessione file flat consente a un pacchetto di connettersi a un file di testo.  
  
 Per ulteriori informazioni sull'Editor gestione connessione file flat, vedere [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la connessione file flat nel flusso di lavoro. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la connessione. È consigliabile includere nella descrizione informazioni sugli scopi della connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Nome file**  
 Consente di digitare il percorso e il nome del file da utilizzare nella connessione file flat.  
  
 **Sfoglia**  
 Consente di individuare il nome del file da utilizzare nella connessione file flat.  
  
 **Impostazioni locali**  
 Consente di specificare le impostazioni locali specifiche di una lingua per l'ordinamento e i formati di data e ora.  
  
 **Unicode**  
 Indica se utilizzare il formato Unicode. Se si utilizza il formato Unicode, non è possibile specificare una tabella codici.  
  
 **Tabella codici**  
 Consente di specificare la tabella codici per il testo non Unicode.  
  
 **Formato**  
 Consente di indicare se il file utilizza il tipo di formattazione delimitato, a larghezza fissa o non allineato a destra.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|Delimitato|Le colonne sono separate dai delimitatori specificati nella pagina **Colonne** .|  
|A larghezza fissa|Le colonne hanno una larghezza fissa.|  
|Non allineato a destra|I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa, ad eccezione dell'ultima. L'ultima colonna è delimitata dal delimitatore di riga.|  
  
 **Qualificatore di testo**  
 Consente di specificare il qualificatore di testo da utilizzare. Ad esempio, è possibile specificare che i campi di testo siano racchiusi tra virgolette.  
  
> [!NOTE]  
>  Dopo aver selezionato un qualificatore di testo non è possibile selezionare di nuovo l'opzione **Nessuno** . Digitare **Nessuno** per deselezionare il qualificatore di testo.  
  
 **Delimitatore riga di intestazione**  
 Consente di selezionare il delimitatore per la riga di intestazione nell'elenco dei delimitatori disponibili oppure di immettere il testo per il delimitatore.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**{CR}{LF}**|La riga di intestazione è delimitata dalla combinazione di caratteri ritorno a capo/avanzamento riga.|  
|**{CR}**|La riga di intestazione è delimitata da un carattere di ritorno a capo.|  
|**{LF}**|La riga di intestazione è delimitata da un carattere di avanzamento riga.|  
|**Punto e virgola {;}**|La riga di intestazione è delimitata da un carattere punto e virgola.|  
|**Due punti {:}**|La riga di intestazione è delimitata da un carattere due punti.|  
|**Virgola {,}**|La riga di intestazione è delimitata da una virgola.|  
|**Tabulazione {t}**|La riga di intestazione è delimitata da un carattere di tabulazione.|  
|**Barra verticale {&#124;}**|La riga di intestazione è delimitata da una barra verticale.|  
  
 **Righe di intestazione da ignorare**  
 Consente di specificare il numero di eventuali righe di intestazione o righe di dati iniziali da ignorare.  
  
 **Nomi di colonne nella prima riga di dati**  
 Consente di indicare se prevedere o fornire nomi di colonne nella prima riga di dati.  
## <a name="flat-file-connection-manager-editor-columns-page"></a>Editor gestione connessione file flat (pagina Colonne)
  Utilizzare la pagina **Colonne** della finestra di dialogo **Editor gestione connessione file flat** per specificare le informazioni di riga e di colonna e per visualizzare un'anteprima del file.  
  
 Per ulteriori informazioni sull'Editor gestione connessione file flat, vedere [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="static-options"></a>Opzioni statiche  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la connessione del file flat nel flusso di lavoro. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la connessione. È consigliabile includere nella descrizione informazioni sugli scopi della connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
### <a name="flat-file-format-dynamic-options"></a>Opzioni dinamiche relative al formato file flat  
  
#### <a name="format--delimited"></a>Formato = Delimitato  
 **Delimitatore di riga**  
 Consente di selezionare il delimitatore di riga desiderato nell'elenco dei delimitatori disponibili oppure di immettere il testo per il delimitatore.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**{CR}{LF}**|Le righe sono delimitate dalla combinazione di caratteri ritorno a capo/avanzamento riga.|  
|**{CR}**|Le righe sono delimitate da un ritorno a capo.|  
|**{LF}**|Le righe sono delimitate da un avanzamento riga.|  
|**Punto e virgola {;}**|Le righe sono delimitate da un punto e virgola.|  
|**Due punti {:}**|Le righe sono delimitate da un carattere due punti.|  
|**Virgola {,}**|Le righe sono delimitate da una virgola.|  
|**Tabulazione {t}**|Le righe sono delimitate da un carattere di tabulazione.|  
|**Barra verticale {&#124;}**|Le righe sono delimitate da una barra verticale.|  
  
 **Delimitatore di colonna**  
 Consente di selezionare il delimitatore di colonna desiderato nell'elenco dei delimitatori disponibili oppure di immettere il testo per il delimitatore.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**{CR}{LF}**|Le colonne sono delimitate dalla combinazione di caratteri ritorno a capo/avanzamento riga.|  
|**{CR}**|Le colonne sono delimitate da un ritorno a capo.|  
|**{LF}**|Le colonne sono delimitate da un avanzamento riga.|  
|**Punto e virgola {;}**|Le colonne sono delimitate da un punto e virgola.|  
|**Due punti {:}**|Le colonne sono delimitate da due punti.|  
|**Virgola {,}**|Le colonne sono delimitate da una virgola.|  
|**Tabulazione {t}**|Le colonne sono delimitate da una tabulazione.|  
|**Barra verticale {&#124;}**|Le colonne sono delimitate da una barra verticale.|  
  
 **Aggiorna**  
 Se si fa clic su **Aggiorna**è possibile visualizzare gli effetti delle modifiche ai delimitatori da ignorare. Questo pulsante viene visualizzato solo dopo la modifica di altre opzioni della connessione.  
  
 **Anteprima righe**  
 Consente di visualizzare dati di esempio del file flat, suddivisi in righe e colonne in base alle opzioni selezionate.  
  
 **Reimposta colonne**  
 Il pulsante **Reimposta colonne**consente di rimuovere tutte le colonne tranne quelle originali.  
  
#### <a name="format--fixed-width"></a>Formato = A larghezza fissa  
 **Carattere**  
 Consente di selezionare il tipo di carattere per la visualizzazione in anteprima dei dati.  
  
 **Colonne dati di origine**  
 Per modificare la larghezza della riga, trascinare l'indicatore di riga rosso verticale. Per modificare la larghezza delle colonne, fare clic sul righello nella parte superiore della finestra di anteprima.  
  
 **Larghezza riga**  
 Consente di specificare la larghezza della riga prima dell'aggiunta dei delimitatori per le singole colonne. In alternativa, trascinare la linea rossa verticale nella finestra di anteprima per contrassegnare la fine della riga. Il valore relativo alla larghezza della riga viene aggiornato automaticamente.  
  
 **Reimposta colonne**  
 Il pulsante **Reimposta colonne**consente di rimuovere tutte le colonne tranne quelle originali.  
  
#### <a name="format--ragged-right"></a>Formato = Non allineato a destra  
  
> [!NOTE]  
>  I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa, ad eccezione dell'ultima. L'ultima colonna è delimitata dal delimitatore di riga.  
  
 **Carattere**  
 Consente di selezionare il tipo di carattere per la visualizzazione in anteprima dei dati.  
  
 **Colonne dati di origine**  
 Per modificare la larghezza della riga, trascinare l'indicatore di riga rosso verticale. Per modificare la larghezza delle colonne, fare clic sul righello nella parte superiore della finestra di anteprima.  
  
 **Delimitatore di riga**  
 Consente di selezionare il delimitatore di riga desiderato nell'elenco dei delimitatori disponibili oppure di immettere il testo per il delimitatore.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**{CR}{LF}**|Le righe sono delimitate dalla combinazione di caratteri ritorno a capo/avanzamento riga.|  
|**{CR}**|Le righe sono delimitate da un ritorno a capo.|  
|**{LF}**|Le righe sono delimitate da un avanzamento riga.|  
|**Punto e virgola {;}**|Le righe sono delimitate da un punto e virgola.|  
|**Due punti {:}**|Le righe sono delimitate da un carattere due punti.|  
|**Virgola {,}**|Le righe sono delimitate da una virgola.|  
|**Tabulazione {t}**|Le righe sono delimitate da un carattere di tabulazione.|  
|**Barra verticale {&#124;}**|Le righe sono delimitate da una barra verticale.|  
  
 **Reimposta colonne**  
 Il pulsante **Reimposta colonne**consente di rimuovere tutte le colonne tranne quelle originali.  
## <a name="flat-file-connection-manager-editor-advanced-page"></a>Editor gestione connessione file flat (pagina Avanzate)
  Usare la pagina **Avanzate** della finestra di dialogo **Editor gestione connessione file flat** per impostare le proprietà che specificano come Integration Services legge e scrive i dati nei file flat. È possibile modificare i nomi delle colonne del file flat e impostare le proprietà che includono il tipo di dati e i delimitatori per ogni colonna del file.  
  
 Per impostazione predefinita, la lunghezza delle colonne di stringhe è di 50 caratteri. È possibile ridimensionare la lunghezza di queste colonne per evitare che i dati siano troncati o che la colonna sia eccessivamente larga. È possibile aggiornare anche altri metadati per attivare la compatibilità con le colonne di destinazione. È possibile ad esempio modificare il tipo di dati di una colonna che contiene solo dati integer impostando un tipo di dati numeric, come DT_I2. È possibile apportare manualmente queste modifiche oppure fare clic sul pulsante **Suggerisci tipi** per usare la finestra di dialogo **Suggerisci tipi di colonne** per valutare i dati di esempio e apportare tali modifiche automaticamente.  
  
 Per ulteriori informazioni sull'Editor gestione connessione file flat, vedere [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la gestione connessione file flat nel flusso di lavoro. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la gestione connessione. È consigliabile includere nella descrizione informazioni sugli scopi della gestione connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Configurare le proprietà delle singole colonne**  
 È possibile selezionare una colonna nel riquadro sinistro per visualizzarne le proprietà in quello destro. Nella tabella seguente è disponibile una descrizione delle proprietà dei tipi di dati. Alcune delle proprietà incluse nell'elenco possono essere configurate solo per alcuni formati di file flat.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**ColumnType**|Indica se la colonna è delimitata, a larghezza fissa o non allineata a destra. Questa proprietà è di sola lettura. I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa, ad eccezione dell'ultima. L'ultima colonna è delimitata dal delimitatore di riga.|  
|**OutputColumnWidth**|Consente di specificare il valore da archiviare come conteggio di byte. Nel caso dei file Unicode tale valore corrisponde al conteggio di caratteri. Nell'attività Flusso di dati questo valore viene utilizzato per impostare la larghezza della colonna di output per l'origine file flat. Nel modello a oggetti il nome di questa proprietà è MaximumWidth.|  
|**DataType**|Consente di selezionare i tipi di dati disponibili nell'apposito elenco. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).|  
|**TextQualified**|Consente di indicare se i dati di tipo testo sono racchiusi tra qualificatori di testo, ad esempio le virgolette.<br /><br /> True: i dati di tipo testo nel file flat sono qualificati. False: I dati di tipo testo nel file flat NON sono qualificati.|  
|**Nome**|Consente di specificare un nome descrittivo per la colonna. Se non si immettere alcun nome, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea automaticamente un nome nel formato Colonna 0, Colonna 1 e così via.|  
|**DataScale**|Consente di specificare la scala dei dati numerici. Per scala si intende il numero di posizioni decimali. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Consente di selezionare i delimitatori di colonna disponibili nell'apposito elenco. Scegliere come delimitatori caratteri che non siano già presenti nel testo. Questo valore viene ignorato per le colonne a larghezza fissa.<br /><br /> **{CR}{LF}** . Le colonne sono delimitate dalla combinazione di caratteri ritorno a capo/avanzamento riga.<br /><br /> **{CR}** . Le colonne sono delimitate da un ritorno a capo.<br /><br /> **{LF}** . Le colonne sono delimitate da un avanzamento riga.<br /><br /> **Punto e virgola {;}** . Le colonne sono delimitate da un punto e virgola.<br /><br /> **Due punti {:}** . Le colonne sono delimitate da due punti.<br /><br /> **Virgola {,}** . Le colonne sono delimitate da una virgola.<br /><br /> **Tabulazione {t}** . Le colonne sono delimitate da una tabulazione.<br /><br /> **Barra verticale {&#124;}** . Le colonne sono delimitate da una barra verticale.|  
|**DataPrecision**|Consente di specificare la precisione dei dati numerici. Per precisione si intende il numero di cifre. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Consente di specificare il valore da archiviare come conteggio di byte. Nel caso dei file Unicode tale valore verrà visualizzato come conteggio di caratteri. Questo valore viene ignorato nelle colonne delimitate.<br /><br /> **Nota** : nel modello a oggetti il nome di questa proprietà è ColumnWidth.|  
  
 **Nuova**  
 Consente di aggiungere una **nuova**colonna. Per impostazione predefinita, il pulsante **Nuova** aggiunge una colonna alla fine dell'elenco. Il pulsante dispone inoltre delle opzioni seguenti, disponibili nell'elenco a discesa.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Aggiungi colonna**|Consente di aggiungere una nuova colonna alla fine dell'elenco.|  
|**Inserisci prima**|Consente di inserire una nuova colonna prima di quella selezionata.|  
|**Inserisci dopo**|Consente di inserire una nuova colonna dopo quella selezionata.|  
  
 **Elimina**  
 Consente di selezionare una colonna e quindi di **rimuoverla**.  
  
 **Suggerisci tipi**  
 La finestra di dialogo **Suggerisci tipi di colonne** consente di valutare dati di esempio nel file e ottenere suggerimenti sul tipo di dati e sulla lunghezza di ogni colonna. Per altre informazioni, vedere [Riferimento all'interfaccia utente della finestra di dialogo Suggerisci tipi di colonne](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
## <a name="flat-file-connection-manager-editor-preview-page"></a>Editor gestione connessione file flat (pagina Anteprima)
  Utilizzare il nodo **Anteprima** della finestra di dialogo **Editor gestione connessione file flat** per visualizzare il contenuto del file di origine in formato tabella.  
  
 Per ulteriori informazioni sull'Editor gestione connessione file flat, vedere [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la connessione del file flat nel flusso di lavoro. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la connessione. È consigliabile includere nella descrizione informazioni sugli scopi della connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Righe di dati da ignorare**  
 Consente di specificare il numero di righe che devono essere ignorate all'inizio del file flat.  
  
 **Aggiorna**  
 Facendo clic su **Aggiorna**, è possibile visualizzare l'effetto della modifica del numero di righe da ignorare. Questo pulsante viene visualizzato solo dopo la modifica di altre opzioni della connessione.  
  
 **Anteprima righe**  
 Consente di visualizzare i dati di esempio del file flat suddivisi in colonne e righe, a seconda delle opzioni selezionate.  
 
