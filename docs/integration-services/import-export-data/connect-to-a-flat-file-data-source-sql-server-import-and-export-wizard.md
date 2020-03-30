---
title: Connettersi a un'origine dati file flat (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d7e7067b-f5a5-482f-b97e-9d82fe8e9f76
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bef4e8032ad605382b3312cac11840ed959a7571
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296352"
---
# <a name="connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard"></a>Connettersi a un'origine dati file flat (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Questo argomento illustra come connettersi a un'origine dati **file flat** (file di testo) dalla pagina **Scelta origine dati** o **Scelta destinazione** dell'Importazione/Esportazione guidata SQL Server. Poiché per i file flat queste due pagine della procedura guidata visualizzano set di opzioni diversi, questo argomento descrive l'origine file flat e la destinazione file flat separatamente.

## <a name="an-alternative-for-simple-text-import"></a>Alternativa all'importazione di testo semplice
Se si deve importare un file di testo in SQL Server e non sono necessarie tutte le opzioni di configurazione disponibili nell'Importazione/Esportazione guidata, può essere utile usare la **procedura guidata Importa file flat** in SQL Server Management Studio (SSMS). Per altre informazioni, vedere gli articoli seguenti:
- [What’s new in SQL Server Management Studio 17.3](https://blogs.technet.microsoft.com/dataplatforminsider/2017/10/10/whats-new-in-sql-server-management-studio-17-3/) (Novità di SQL Server Management Studio 17.3)
- [Introducing the new Import Flat File Wizard in SSMS 17.3](https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173) (Introduzione alla nuova procedura guidata Importa file flat in SSMS 17.3)

## <a name="connect-to-a-flat-file-source"></a>Connettersi a un'origine file flat
 
 Per le origini dati file flat sono disponibili quattro pagine di opzioni. La configurazione di ogni pagina tuttavia non richiede molto tempo. Di seguito sono elencate le operazioni utili da eseguire.
 
Pagina|Recommendation  |Type  
----|---------|---------
**Generale**|Assicurarsi di aggiornare le opzioni della sezione **Formato**.|Consigliato    
**Colonne**|Assicurarsi di controllare i delimitatori di colonna e riga (per un file delimitato) o di contrassegnare le colonne (per un file a larghezza fissa).|Consigliato
**Funzionalità avanzate**|Facoltativamente, controllare i tipi di dati e le altre proprietà assegnate per impostazione predefinita alle colonne.|Facoltativo
**Anteprima**|Facoltativamente, visualizzare in anteprima un campione di dati usando le impostazioni specificate.|Facoltativo

## <a name="general-page-source"></a>Pagina Generale (origine)
 Nella pagina **Generale**, selezionare il file, quindi verificare le impostazioni nella sezione **Formato**.
 
 ![Connessione file flat generale](../../integration-services/import-export-data/media/flat-file-connection-general.png)  

### <a name="options-to-specify-general-page"></a>Opzioni da specificare (pagina **Generale**)

 **Nome file**  
 Immettere il percorso e il nome del file del file flat.  
  
 **Sfoglia**  
 Individuare il file flat.  
  
 **Impostazioni locali**  
 Specificare le impostazioni locali per fornire le informazioni specifiche della lingua per l'ordinamento e i formati di data e ora.  
  
 **Unicode**  
 Specificare se il file usa Unicode. Se si usa Unicode, non è possibile specificare una tabella codici.  
  
 **Tabella codici**  
 Consente di specificare la tabella codici per il testo non Unicode.  
  
 **Formato**  
 Specificare se il file usa il tipo di formattazione delimitato, a larghezza fissa o non allineato a destra.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|Delimitato|Le colonne sono separate da delimitatori. Specificare il delimitatore nella pagina **Colonne**.|  
|File a larghezza fissa|Le colonne hanno una larghezza fissa.|  
|Non allineato a destra|I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa ad eccezione dell'ultima, per la quale viene utilizzato il delimitatore di riga.|  
  
 **Qualificatore di testo**  
 Specificare il qualificatore di testo, se presente, usato dal file. Ad esempio, è possibile specificare che i campi di testo siano racchiusi tra virgolette. Questa proprietà si applica solo ai file delimitati. 
  
> [!NOTE]
> Dopo aver selezionato un qualificatore di testo non è possibile selezionare di nuovo l'opzione **Nessuno**. Digitare **Nessuno** per deselezionare il qualificatore di testo.  
  
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
 Specificare il numero di righe da ignorare nella parte superiore del file.  
  
 **Nomi di colonne nella prima riga di dati**  
 Specificare se la prima riga di dati (dopo le righe ignorate) contiene nomi di colonna.

## <a name="columns-page---format--delimited-source"></a>Pagina Colonne - Formato = Delimitato (origine)
 Nella pagina **Colonne** verificare l'elenco di colonne e i delimitatori che la procedura guidata ha identificato. Lo screenshot seguente mostra la pagina dopo aver selezionato **Delimitato** come formato del file flat.
 
![Flat file, Delimitato, pagina Colonne](../../integration-services/import-export-data/media/flat-file-delimited-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--delimited"></a>Opzioni da specificare (Pagina **Colonne** - Formato = Delimitato)

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
  
 **Anteprima righe**  
 Consente di visualizzare dati di esempio del file flat, suddivisi in righe e colonne in base alle opzioni selezionate.  
 
 **Aggiorna**  
 Se si fa clic su **Aggiorna**è possibile visualizzare gli effetti delle modifiche ai delimitatori da ignorare. Questo pulsante viene visualizzato solo dopo la modifica di altre opzioni della connessione.  
  
 **Reimposta colonne**  
 Ripristinare le colonne originali.  

## <a name="columns-page---format--fixed-width-source"></a>Pagina Colonne - Formato = A larghezza fissa (origine)
Nella pagina **Colonne** verificare l'elenco di colonne e i delimitatori che la procedura guidata ha identificato. Lo screenshot seguente mostra la pagina dopo aver selezionato **A larghezza fissa** come formato del file flat.
  
![File flat, A larghezza fissa, pagina Colonne](../../integration-services/import-export-data/media/flat-file-fixed-width-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--fixed-width"></a>Opzioni da specificare (Pagina **Colonne** - Formato = A larghezza fissa)

 **Carattere**  
 Consente di selezionare il tipo di carattere per la visualizzazione in anteprima dei dati.  
  
 **Colonne dati di origine**  
 Per modificare la larghezza della riga, trascinare l'indicatore di riga rosso verticale. Per modificare la larghezza delle colonne, fare clic sul righello nella parte superiore della finestra di anteprima.  
  
 **Larghezza riga**  
 Consente di specificare la larghezza della riga prima dell'aggiunta dei delimitatori per le singole colonne. In alternativa, trascinare la linea rossa verticale nella finestra di anteprima per contrassegnare la fine della riga. Il valore relativo alla larghezza della riga viene aggiornato automaticamente.  
  
 **Reimposta colonne**  
 Ripristinare le colonne originali.  
  
## <a name="columns-page---format--ragged-right-source"></a>Pagina Colonne - Formato = Non allineato a destra (origine)
Nella pagina **Colonne** verificare l'elenco di colonne e i delimitatori che la procedura guidata ha identificato. Lo screenshot seguente mostra la pagina dopo aver selezionato **Non allineato a destra** come formato del file flat.

> [!NOTE]
> I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa ad eccezione dell'ultima, per la quale viene utilizzato il delimitatore di riga.  
 
![File flat, Non allineato a destra, pagina Colonne](../../integration-services/import-export-data/media/flat-file-ragged-right-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--ragged-right"></a>Opzioni da specificare (pagina **Colonne** - Formato = Non allineato a destra)
   
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
 Ripristinare le colonne originali.  

## <a name="advanced-page-source"></a>Pagina Avanzate (origine)
La pagina **Avanzate** mostra informazioni dettagliate su ogni colonna nell'origine dati, inclusi il tipo di dati e le dimensioni. Lo screenshot seguente mostra la pagina **Avanzate** per la prima colonna in un file flat delimitato.

![File flat, delimitato, pagina Avanzate](../../integration-services/import-export-data/media/flat-file-delimited-advanced-page.jpg)

Nello screenshot si noti che il tipo di dati della colonna **id**, che contiene numeri, è inizialmente string.

### <a name="options-to-specify-advanced-page"></a>Opzioni da specificare (pagina **Avanzate**)

 **Configurare le proprietà delle singole colonne**  
 È possibile selezionare una colonna nel riquadro sinistro per visualizzarne le proprietà in quello destro. La tabella seguente descrive le proprietà delle colonne. Alcune delle proprietà elencate sono configurabili solo per alcuni formati di file flat e per le colonne di determinati tipi di dati.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**Nome**|Consente di specificare un nome descrittivo per la colonna. Se non si immettere alcun nome, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea automaticamente un nome nel formato Colonna 0, Colonna 1 e così via.|
|**ColumnDelimiter**|Consente di selezionare i delimitatori di colonna disponibili nell'apposito elenco. Scegliere come delimitatori caratteri che non siano già presenti nel testo. Questo valore viene ignorato per le colonne a larghezza fissa.<br /><br /> **{CR}{LF}** . Le colonne sono delimitate dalla combinazione di caratteri ritorno a capo/avanzamento riga.<br /><br /> **{CR}** . Le colonne sono delimitate da un ritorno a capo.<br /><br /> **{LF}** . Le colonne sono delimitate da un avanzamento riga.<br /><br /> **Punto e virgola {;}** . Le colonne sono delimitate da un punto e virgola.<br /><br /> **Due punti {:}** . Le colonne sono delimitate da due punti.<br /><br /> **Virgola {,}** . Le colonne sono delimitate da una virgola.<br /><br /> **Tabulazione {t}** . Le colonne sono delimitate da una tabulazione.<br /><br /> **Barra verticale {&#124;}** . Le colonne sono delimitate da una barra verticale.|
|**ColumnType**|Indica se la colonna è delimitata, a larghezza fissa o non allineata a destra. Questa proprietà è di sola lettura. I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa, ad eccezione dell'ultima. L'ultima colonna è delimitata dal delimitatore di riga.|  
|**InputColumnWidth**|Specificare il valore da archiviare come numero di byte. Per i file Unicode, questo valore corrisponde al numero di caratteri. Questo valore viene ignorato nelle colonne delimitate.<br /><br /> **Nota** : nel modello a oggetti il nome di questa proprietà è ColumnWidth.|
|**DataPrecision**|Consente di specificare la precisione dei dati numerici. Per precisione si intende il numero di cifre.|
|**DataScale**|Consente di specificare la scala dei dati numerici. Per scala si intende il numero di posizioni decimali.|
|**DataType**|Consente di selezionare i tipi di dati disponibili nell'apposito elenco.<br/>Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).|
|**OutputColumnWidth**|Consente di specificare il valore da archiviare come conteggio di byte. Nel caso dei file Unicode tale valore corrisponde al conteggio di caratteri. Nell'attività Flusso di dati questo valore viene utilizzato per impostare la larghezza della colonna di output per l'origine file flat. Nel modello a oggetti il nome di questa proprietà è MaximumWidth.|  
|**TextQualified**|Consente di indicare se i dati di tipo testo sono racchiusi tra qualificatori di testo, ad esempio le virgolette.<br /><br /> True: i dati di tipo testo nel file flat sono qualificati. False: i dati di tipo testo nel file flat NON sono qualificati.|  
  
**Nuovo**  
 Consente di aggiungere una **nuova**colonna. Per impostazione predefinita, il pulsante **Nuova** aggiunge una colonna alla fine dell'elenco. Il pulsante dispone inoltre delle opzioni seguenti, disponibili nell'elenco a discesa.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Aggiungi colonna**|Consente di aggiungere una nuova colonna alla fine dell'elenco.|  
|**Inserisci prima**|Consente di inserire una nuova colonna prima di quella selezionata.|  
|**Inserisci dopo**|Consente di inserire una nuova colonna dopo quella selezionata.|  
  
 **Elimina**  
 Consente di selezionare una colonna e quindi di **rimuoverla**.  
  
 **Suggerisci tipi**  
 La finestra di dialogo **Suggerisci tipi di colonne** consente di valutare dati di esempio nel file e ottenere suggerimenti sul tipo di dati e sulla lunghezza di ogni colonna.  
 
Fare clic su **Suggerisci tipi** per visualizzare la finestra di dialogo **Suggerisci tipi di colonne**. 

![Finestra di dialogo di suggerimento dei tipi della connessione file flat](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

Dopo aver selezionato le opzioni nella finestra di dialogo **Suggerisci tipi di colonne** e aver fatto clic su **OK**, è possibile che la procedura guidata modifichi i tipi di dati di alcune colonne.

Lo screenshot seguente mostra che, dopo aver fatto clic su **Suggerisci tipi**, la procedura guidata ha rilevato che la colonna **id** nell'origine dati è un numero e non una stringa di testo e che il tipo di dati della colonna è stato modificato da string a integer.

![Connessione file flat avanzate dopo](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)

Per altre informazioni, vedere [Riferimento all'interfaccia utente della finestra di dialogo Suggerisci tipi di colonne](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).

## <a name="preview-page-source"></a>Pagina Anteprima (origine)

Nella pagina **Anteprima** verificare che l'elenco di colonne e i dati di esempio siano quelli desiderati.

![File flat, pagina Anteprima](../../integration-services/import-export-data/media/flat-file-preview-page.jpg)

### <a name="options-to-specify-preview-page"></a>Opzioni da specificare (pagina **Anteprima**)

 **Righe di dati da ignorare**  
 Consente di specificare il numero di righe che devono essere ignorate all'inizio del file flat.  
  
 **Anteprima righe**  
 Consente di visualizzare i dati di esempio del file flat suddivisi in colonne e righe, a seconda delle opzioni selezionate.
 
 **Aggiorna**  
 Facendo clic su **Aggiorna**, è possibile visualizzare l'effetto della modifica del numero di righe da ignorare. Questo pulsante viene visualizzato solo dopo la modifica di altre opzioni della connessione.  
 
Per altre informazioni sulla pagina **Anteprima**, vedere la pagina di riferimento di Integration Services seguente: [Editor gestione connessione file flat &#40;pagina Anteprima&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md).

## <a name="connect-to-a-flat-file-destination"></a>Connettersi a una destinazione file flat
Per una destinazione file flat, è disponibile solo una singola pagina di opzioni, come illustrato nello screenshot seguente. Selezionare il file, quindi verificare le impostazioni nella sezione **Formato**.

![Connettersi a una destinazione file flat](../../integration-services/import-export-data/media/connect-to-flat-file-destination.jpg)

### <a name="options-to-specify-choose-a-destination-page"></a>Opzioni da specificare (pagina **Scelta destinazione**)

 **Nome file**  
 Immettere il percorso e il nome del file del file flat.  
  
 **Sfoglia**  
 Individuare il file flat.  
  
 **Impostazioni locali**  
 Specificare le impostazioni locali per fornire le informazioni specifiche della lingua per l'ordinamento e i formati di data e ora.  
  
 **Unicode**  
 Specificare se il file usa Unicode. Se si usa Unicode, non è possibile specificare una tabella codici.  
  
 **Tabella codici**  
 Consente di specificare la tabella codici per il testo non Unicode.  
  
 **Formato**  
 Specificare se il file usa il tipo di formattazione delimitato, a larghezza fissa o non allineato a destra.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|Delimitato|Le colonne sono separate da delimitatori. Specificare il delimitatore nella pagina **Colonne**.|  
|File a larghezza fissa|Le colonne hanno una larghezza fissa.|  
|Non allineato a destra|I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa ad eccezione dell'ultima, per la quale viene utilizzato il delimitatore di riga.|  
  
 **Qualificatore di testo**  
 Specificare il qualificatore di testo, se presente, usato dal file. Ad esempio, è possibile specificare che i campi di testo siano racchiusi tra virgolette. Questa proprietà si applica solo ai file delimitati. 
  
> [!NOTE] 
> Dopo aver selezionato un qualificatore di testo non è possibile selezionare di nuovo l'opzione **Nessuno**. Digitare **Nessuno** per deselezionare il qualificatore di testo.  

## <a name="see-also"></a>Vedere anche
[Scelta origine dati](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Scegliere una destinazione](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

