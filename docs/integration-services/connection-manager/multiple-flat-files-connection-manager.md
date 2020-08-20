---
description: gestione connessione per più file flat
title: Gestione connessione per più file flat | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.multifile.advanced.f1
- sql13.dts.designer.multifile.columns.f1
- sql13.dts.designer.multifile.general.f1
- sql13.dts.designer.multifile.preview.f1
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bac3edc5c3be2a54a999a4b68c7bb0e15f686651
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484704"
---
# <a name="multiple-flat-files-connection-manager"></a>gestione connessione per più file flat

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Una gestione connessione per più file flat consente a un pacchetto di accedere a dati contenuti in più file flat. Ad esempio, un'origine file flat può utilizzare una gestione connessione per più file quando l'attività Flusso di dati si trova in un contenitore Ciclo, ad esempio il contenitore Ciclo For. In ogni ciclo del contenitore, l'origine file flat carica dati dal nome file successivo fornito dalla gestione connessione per più file.  
  
 Quando si aggiunge una gestione connessione per più file flat a un pacchetto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione per più file flat, imposta le proprietà della gestione connessione per più file flat e quindi la aggiunge alla raccolta **Connections** del pacchetto.  
  
 La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **MULTIFLATFILE**.  
  
 Per configurare la gestione connessione per più file flat, procedere nel modo seguente:  
  
-   Specificare i file, le impostazioni locali e la tabella codici da utilizzare. Le impostazioni locali vengono utilizzate per interpretare i dati con formato dipendente dalla lingua, come le date, mentre la tabella codici viene utilizzata per convertire i dati stringa in formato Unicode.  
  
-   Specificare il formato dei file. È possibile utilizzare un formato delimitato, a larghezza fissa o non allineato a destra.  
  
-   Specificare i delimitatori della riga di intestazione, delle righe di dati e delle colonne. I delimitatori delle colonne possono essere impostati a livello di file e sovrascritti a livello di colonna.  
  
-   Indicare se la prima riga dei file contiene i nomi delle colonne.  
  
-   Specificare un qualificatore di testo. Ogni colonna può essere configurata in modo da riconoscere un qualificatore di testo.  
  
-   Impostare proprietà quali il nome, il tipo di dati e la larghezza massima delle singole colonne.  
  
 Quando la gestione connessione per più file flat fa riferimento a più file, i percorsi dei file sono separati da una barra verticale. La proprietà **ConnectionString** della gestione connessione ha il formato seguente:  
  
 \<*path*>|\<*path*>  
  
 Per specificare più file è inoltre possibile utilizzare caratteri jolly. Per fare riferimento, ad esempio, a tutti i file di testo sull'unità C è possibile impostare il valore della proprietà **ConnectionString** su C:\\\*.txt.  
  
 Se una gestione connessione per più file flat fa riferimento a più file, tutti i file devono avere lo stesso formato.  
  
 Per impostazione predefinita la gestione connessione per più file flat imposta la lunghezza delle colonne di tipo stringa su 50 caratteri. Nella finestra di dialogo **Editor gestione connessione per più file flat** è possibile valutare dati di esempio e modificare automaticamente la lunghezza di tali colonne, in modo da evitare il troncamento dei dati o il superamento della larghezza massima delle colonne. La lunghezza della colonna rimane invariata per tutto il flusso di dati, a meno che non venga modificata in un'origine file flat o in una trasformazione. Se su tali colonne viene eseguito il mapping a colonne di destinazione di larghezza inferiore, verrà visualizzato un avviso nell'interfaccia utente e in fase di esecuzione potrebbero verificarsi errori dovuti al troncamento dei dati. È possibile ridimensionare le colonne in modo che siano compatibili con le colonne di destinazione nella gestione connessione file flat, nell'origine file flat o in una trasformazione. Per modificare la lunghezza di una colonna di output, è necessario impostare la proprietà **Length** della colonna di output nella scheda **Proprietà input e output** della finestra di dialogo **Editor avanzato** .  
  
 Se, dopo avere aggiunto e configurato l'origine file flat che utilizza la gestione connessione, si modifica la lunghezza delle colonne nella gestione connessione per più file flat, non sarà necessario ridimensionare manualmente le colonne di output nell'origine file flat. Nella finestra di dialogo **Origine file flat** è disponibile un'opzione che consente di sincronizzare i metadati delle colonne per l'origine file flat.  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>Configurazione della gestione connessione per più file flat  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="multiple-flat-files-connection-manager-editor-general-page"></a>Editor gestione connessione per più file flat (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo **Editor gestione connessione per più file flat** per selezionare un gruppo di file con lo stesso formato di dati e per specificare il loro formato dei dati. Una connessione per più file flat consente la connessione di un pacchetto a un gruppo di file di testo aventi lo stesso formato.  
  
 Per ulteriori informazioni sulla gestione connessione per più file flat, vedere [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la connessione per più file flat nel flusso di lavoro. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la connessione. È consigliabile includere nella descrizione informazioni sugli scopi della connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Nomi file**  
 Consente di digitare il percorso e i nomi dei file da utilizzare nella connessione per più flat file. È possibile specificare più file usando caratteri jolly, ad esempio "C:\\*.txt", oppure il carattere barra verticale (|) per separare più nomi di file. Tutti i file devono avere lo stesso formato data.  
  
 **Sfoglia**  
 Consente di cercare i nomi dei file da utilizzare nella connessione per più file flat. È possibile selezionare più file. Tutti i file devono avere lo stesso formato data.  
  
 **Impostazioni locali**  
 Consente di specificare la località per specificare informazioni relative all'ordinamento e alla conversione di data e ora.  
  
 **Unicode**  
 Indica se utilizzare il formato Unicode. L'utilizzo di Unicode impedisce di specificare una tabella codici.  
  
 **Tabella codici**  
 Consente di specificare la tabella codici per il testo non Unicode.  
  
 **Formato**  
 Consente di indicare se utilizzare la formattazione non allineata a destra, a larghezza fissa o delimitata. Tutti i file devono avere lo stesso formato data.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|Delimitato|Le colonne sono separate dai delimitatori specificati nella pagina **Colonne** .|  
|File a larghezza fissa|Le colonne hanno una larghezza fissa, specificata trascinando le linee dei marcatori nella pagina **Colonne** .|  
|Non allineato a destra|I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa, ad eccezione dell'ultima colonna, delimitata dal delimitatore di riga, che viene specificato nella pagina **Colonne** .|  
  
 **Qualificatore di testo**  
 Consente di specificare il qualificatore di testo da utilizzare. È possibile, ad esempio, racchiudere il testo tra virgolette.  
  
 **Delimitatore riga di intestazione**  
 Consente di selezionare il delimitatore per la riga di intestazione nell'elenco dei delimitatori disponibili oppure di immettere il testo per il delimitatore.  
  
|Valore|Descrizione|  
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
 Consente di specificare il numero di righe di intestazione da ignorare, se presenti.  
  
 **Nomi di colonne nella prima riga di dati**  
 Consente di indicare se prevedere o fornire nomi di colonne nella prima riga di dati.  
  
## <a name="multiple-flat-files-connection-manager-editor-columns-page"></a>Editor gestione connessione per più file flat (pagina Colonne)
  Utilizzare il nodo **Colonne** della finestra di dialogo **Editor gestione connessione per più file flat** per specificare informazioni sulla riga e la colonna e visualizzare l'anteprima del primo file selezionato.  
  
 Per ulteriori informazioni sulla gestione connessione per più file flat, vedere [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="static-options"></a>Opzioni statiche  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la connessione per più file flat nel flusso di lavoro. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la connessione. È consigliabile includere nella descrizione informazioni sugli scopi della connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
### <a name="flat-file-format-dynamic-options"></a>Opzioni dinamiche relative al formato file flat  
  
#### <a name="format--delimited"></a>Formato = Delimitato  
 **Delimitatore di riga**  
 Consente di selezionare il delimitatore di riga desiderato nell'elenco dei delimitatori disponibili oppure di immettere il testo per il delimitatore.  
  
|Valore|Descrizione|  
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
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**{CR}{LF}**|Le colonne sono delimitate dalla combinazione di caratteri ritorno a capo/avanzamento riga.|  
|**{CR}**|Le colonne sono delimitate da un ritorno a capo.|  
|**{LF}**|Le colonne sono delimitate da un avanzamento riga.|  
|**Punto e virgola {;}**|Le colonne sono delimitate da un punto e virgola.|  
|**Due punti {:}**|Le colonne sono delimitate da due punti.|  
|**Virgola {,}**|Le colonne sono delimitate da una virgola.|  
|**Tabulazione {t}**|Le colonne sono delimitate da una tabulazione.|  
|**Barra verticale {&#124;}**|Le colonne sono delimitate da una barra verticale.|  
  
 **Reimposta colonne**  
 Il pulsante **Reimposta colonne**consente di rimuovere tutte le colonne tranne quelle originali.  
  
#### <a name="format--fixed-width"></a>Formato = A larghezza fissa  
 **Carattere**  
 Consente di selezionare il tipo di carattere per la visualizzazione in anteprima dei dati.  
  
 **Colonne dati di origine**  
 Per modificare la larghezza della riga, trascinare l'indicatore di riga verticale, mentre per modificare la larghezza delle colonne, fare clic sul righello nella parte superiore della finestra di anteprima.  
  
 **Larghezza riga**  
 Consente di specificare la larghezza della riga prima dell'aggiunta dei delimitatori per le singole colonne. In alternativa, trascinare la linea verticale nella finestra di anteprima per contrassegnare la fine della riga. Il valore relativo alla larghezza della riga viene aggiornato automaticamente.  
  
 **Reimposta colonne**  
 Il pulsante **Reimposta colonne**consente di rimuovere tutte le colonne tranne quelle originali.  
  
#### <a name="format--ragged-right"></a>Formato = Non allineato a destra  
  
> [!NOTE]  
>  Nei file con formato non allineato a destra, ogni colonna ha una larghezza fissa, ad eccezione dell'ultima colonna. L'ultima colonna è delimitata dal delimitatore di riga.  
  
 **Carattere**  
 Consente di selezionare il tipo di carattere per la visualizzazione in anteprima dei dati.  
  
 **Colonne dati di origine**  
 Per modificare la larghezza della riga, trascinare l'indicatore di riga verticale, mentre per modificare la larghezza delle colonne, fare clic sul righello nella parte superiore della finestra di anteprima.  
  
 **Delimitatore di riga**  
 Consente di selezionare il delimitatore di riga desiderato nell'elenco dei delimitatori disponibili oppure di immettere il testo per il delimitatore.  
  
|Valore|Descrizione|  
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
  
## <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>Editor gestione connessione per più file flat (pagina Avanzate)
  Usare la pagina **Avanzate** della finestra di dialogo **Editor gestione connessione per più file flat** per impostare proprietà come il tipo di dati e i delimitatori di ogni colonna nei file di testo a cui si connette la gestione connessione per i file flat.  
  
 Per impostazione predefinita, la lunghezza delle colonne di stringhe è di 50 caratteri. È possibile valutare i dati di esempio e ridimensionare automaticamente la lunghezza di queste colonne per evitare che i dati siano troncati o che la colonna sia eccessivamente larga. È possibile aggiornare anche altri metadati per attivare la compatibilità con le colonne di destinazione. È possibile ad esempio modificare il tipo di dati di una colonna che contiene solo dati integer impostando un tipo di dati numeric, come DT_I2.  
  
 Per ulteriori informazioni sulla gestione connessione per più file flat, vedere [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la gestione connessione per più file flat nel flusso di lavoro. Il nome specificato verrà visualizzato nell'area **Gestioni connessioni** in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la gestione connessione. È consigliabile includere nella descrizione informazioni sugli scopi della gestione connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Configurare le proprietà delle singole colonne**  
 È possibile selezionare una colonna nel riquadro sinistro per visualizzarne le proprietà in quello destro. Nella tabella seguente è disponibile una descrizione delle proprietà dei tipi di dati. Alcune delle proprietà incluse nell'elenco possono essere configurate solo per alcuni formati di file flat.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**ColumnType**|Indica se la colonna è delimitata, a larghezza fissa o non allineata a destra. Questa proprietà è di sola lettura. I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa ad eccezione dell'ultima, per la quale viene utilizzato il delimitatore di riga.|  
|**OutputColumnWidth**|Consente di specificare il valore da archiviare come conteggio di byte. Nel caso dei file Unicode tale valore verrà visualizzato come conteggio di caratteri. Nell'attività Flusso di dati questo valore viene utilizzato per impostare la larghezza della colonna di output per l'origine file flat.<br /><br /> Nota: Nel modello a oggetti il nome di questa proprietà è MaximumWidth.|  
|**DataType**|Consente di selezionare i tipi di dati disponibili nell'apposito elenco. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).|  
|**TextQualified**|Consente di specificare se i dati di testo sono qualificati usando un carattere qualificatore di testo:<br /><br /> **True**: i dati di tipo testo nel file flat sono qualificati.<br /><br /> **False**: i dati di tipo testo nel file flat non sono qualificati.|  
|**Nome**|Consente di specificare un nome per la colonna. Per impostazione predefinita, si tratta di un elenco numerato di colonne. È comunque possibile scegliere qualsiasi nome descrittivo univoco.|  
|**DataScale**|Consente di specificare la scala dei dati numerici. Per scala si intende il numero di posizioni decimali. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Consente di selezionare i delimitatori di colonna disponibili nell'apposito elenco. Scegliere come delimitatori caratteri che non siano già presenti nel testo. Questo valore viene ignorato per le colonne a larghezza fissa.<br /><br /> **{CR}{LF}** : le colonne sono delimitate dalla combinazione di caratteri ritorno a capo/avanzamento riga<br /><br /> **{CR}** : le colonne sono delimitate da un ritorno a capo<br /><br /> **{LF}** : le colonne sono delimitate da un avanzamento riga<br /><br /> **Punto e virgola {;}** : le colonne sono delimitate da un punto e virgola<br /><br /> **Due punti {:}** : le colonne sono delimitate da due punti<br /><br /> **Virgola {,}{,}** : le colonne sono delimitate da una virgola<br /><br /> **Tabulazione {t}** : le colonne sono delimitate da una tabulazione<br /><br /> **Barra verticale {&#124;}** : le colonne sono delimitate da una barra verticale|  
|**DataPrecision**|Consente di specificare la precisione dei dati numerici. Per precisione si intende il numero di cifre. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Consente di specificare il valore da archiviare come conteggio di byte. Nel caso dei file Unicode tale valore verrà visualizzato come conteggio di caratteri. Questo valore viene ignorato nelle colonne delimitate.<br /><br /> **Nota** : nel modello a oggetti il nome di questa proprietà è ColumnWidth.|  
  
 **Nuovo**  
 Consente di aggiungere una **nuova**colonna. Per impostazione predefinita, il pulsante **Nuova** aggiunge una colonna alla fine dell'elenco. Il pulsante offre inoltre le opzioni seguenti che è possibile selezionare dall'elenco a discesa.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**Aggiungi colonna**|Consente di aggiungere una nuova colonna alla fine dell'elenco.|  
|**Inserisci prima**|Consente di inserire una nuova colonna prima di quella selezionata.|  
|**Inserisci dopo**|Consente di inserire una nuova colonna dopo quella selezionata.|  
  
 **Elimina**  
 Consente di selezionare una colonna e quindi di **rimuoverla**.  
  
 **Suggerisci tipi**  
 Usare la finestra di dialogo **Suggerisci tipi di colonne** per restituire dati di esempio nel primo file selezionato e ottenere suggerimenti relativi al tipo di dati e alla lunghezza di ogni colonna. Per altre informazioni, vedere [Riferimento all'interfaccia utente della finestra di dialogo Suggerisci tipi di colonne](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
  
## <a name="multiple-flat-files-connection-manager-editor-preview-page"></a>Editor gestione connessione per più file flat (pagina Anteprima)
  Usare la pagina **Anteprima** della finestra di dialogo **Editor gestione connessione per più file flat** per visualizzare il contenuto del primo file di origine selezionato suddiviso in colonne in base alle impostazioni definite in precedenza.  
  
 Per ulteriori informazioni sulla gestione connessione per più file flat, vedere [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la connessione per più file flat nel flusso di lavoro. Il nome specificato verrà visualizzato nell'area **Gestioni connessioni** in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la connessione. È consigliabile includere nella descrizione informazioni sugli scopi della connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Righe di dati da ignorare**  
 Consente di specificare il numero di righe che devono essere ignorate all'inizio del file flat.  
  
 **Anteprima righe**  
 Consente di visualizzare dati di esempio del primo flat file selezionato, suddivisi in righe e colonne in base alle opzioni selezionate.  
  
## <a name="see-also"></a>Vedere anche  
 [Origine file flat](../../integration-services/data-flow/flat-file-source.md)   
 [Destinazione file flat](../../integration-services/data-flow/flat-file-destination.md)   
 [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
