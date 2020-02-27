---
title: Esportazione in un file CSV (Generatore report) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 68ec746e-8c82-47f5-8c3d-dbe403a441e5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0b53c40aeb36b2db7586fe135daa05aff17e54e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77078371"
---
# <a name="exporting-to-a-csv-file-report-builder-and-ssrs"></a>Esportazione in un file CSV (Generatore report e SSRS)
  L'estensione per il rendering CSV (Comma-Separated Value) consente di eseguire il rendering di report impaginati come rappresentazione bidimensionale dei dati di un report in un formato di testo normale standardizzato, facilmente leggibile e interscambiabile con numerose applicazioni.  
  
 Per la separazione dei campi e delle righe con l'estensione per il rendering CSV viene usato un delimitatore di stringhe di caratteri che è possibile configurare per impostare un carattere diverso dalla virgola. Il file risultante può essere aperto in un foglio di calcolo, ad esempio [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] , oppure usato come formato di importazione per altri programmi. Il report esportato viene salvato come file con estensione csv e restituisce il tipo MIME **text/csv**.  
  
 Se si desidera usare dati correlati a grafici, barre dei dati, grafici sparkline, misuratori e indicatori in [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)], esportare il report in un file CSV, quindi aprire il file in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  
  
 Per informazioni dettagliate su come esportare in formato CSV, vedere [Esportazione di report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CSVRendering"></a> Rendering CSV  
 Se il rendering viene eseguito usando le impostazioni predefinite, il report CSV avrà le caratteristiche seguenti:  
  
-   Il delimitatore di campo predefinito è la virgola (,).  
  
    > [!NOTE]  
    >  È possibile impostare il delimitatore del campo su qualsiasi carattere desiderato, incluso TAB, modificando le impostazioni relative alle informazioni sui dispositivi. Per altre informazioni, vedere [CSV Device Information Settings](../../reporting-services/csv-device-information-settings.md).  
  
-   La stringa di delimitazione dei record è una sequenza di ritorno a capo e avanzamento riga (\<cr>\<lf>).  
  
-   Il carattere qualificatore di testo è la virgoletta doppia (").  
  
     Il renderer CSV non racchiude le stringhe di testo tra qualificatori. I qualificatori di testo vengono aggiunti solo quando il valore contiene il carattere del delimitatore o include un'interruzione di riga.  
  
-   Se il testo contiene uno dei delimitatori o qualificatori, il qualificatore di testo viene posizionato attorno al testo e i caratteri qualificatori all'interno del testo vengono raddoppiati.  
  
-   La formattazione e il layout vengono ignorati.  
  
 Durante il rendering i seguenti elementi vengono ignorati:  
  
-   Intestazione di pagina  
  
-   Piè di pagina  
  
-   Elementi personalizzati del report  
  
-   Grafico a linee  
  
-   Immagine  
  
-   Rectangle  
  
-   Subtotali automatici  
  
 Gli elementi rimanenti del report vengono ordinati dall'alto verso il basso, quindi da sinistra a destra. Viene quindi eseguito il rendering di ogni elemento in una colonna. Se il report include elementi di dati nidificati, ad esempio elenchi o tabelle, gli elementi padre vengono ripetuti in ogni record.  
  
 Nella seguente tabella è indicato l'aspetto degli elementi del report di cui è stato eseguito il rendering:  
  
|Elemento|Tipo di rendering|  
|----------|------------------------|  
|Casella di testo|Viene eseguito il rendering del contenuto della casella di testo. Nella modalità predefinita gli elementi vengono formattati in base alle proprietà di formattazione dell'elemento. Nella modalità conforme la formattazione può essere modificata dalle impostazioni relative alle informazioni sui dispositivi. Per altre informazioni sulle modalità di rendering CSV, vedere di seguito.|  
|Tabella|Il rendering viene eseguito mediante l'espansione della tabella e la creazione di una riga e una colonna per ogni riga e colonna al livello di dettaglio inferiore. Per le righe e le colonne di subtotali non sono disponibili intestazioni. I report drill-through non sono supportati.|  
|Matrice|Il rendering viene eseguito mediante l'espansione della matrice e la creazione di una riga e una colonna per ogni riga e colonna al livello di dettaglio inferiore. Per le righe e le colonne di subtotali non sono disponibili intestazioni.|  
|Elenco|Viene eseguito il rendering di un record per ogni riga di dettagli o istanza nell'elenco.|  
|Sottoreport|L'elemento padre viene ripetuto per ogni istanza del contenuto.|  
|Grafico|Il rendering viene eseguito mediante la creazione di una riga per ogni valore del grafico ed etichetta del membro. Le etichette delle serie e delle categorie nelle gerarchie sono rese bidimensionali e incluse nella riga per un valore del grafico.|  
|Barra dei dati|Viene eseguito il rendering come grafico. In genere, in una barra dei dati non sono incluse gerarchie o etichette.|  
|Grafico sparkline|Viene eseguito il rendering come grafico. In genere, in un grafico sparkline non sono incluse gerarchie o etichette.|  
|Misuratore|Viene eseguito il rendering come un record singolo con i valori minimo e massimo della scala lineare, i valori iniziale e finale dell'intervallo e il valore dell'indicatore di misura.|  
|Indicatore|Viene eseguito il rendering come un singolo record con il nome di stato attivo, gli stati disponibili e il valore dei dati.|  
|Mappa|Viene eseguito il rendering di una riga con le etichette e i valori per ogni membro della mappa di un livello mappa.<br /><br /> Se la mappa ha più livelli, i valori nelle righe variano a seconda se i livelli mappa usano le stesse aree dati della mappa o aree diverse. Se più livelli mappa usano la stessa area dati, le righe contengono i dati di tutti i livelli.|  
  
### <a name="hierarchical-and-grouped-data"></a>Dati gerarchici e raggruppati  
 Per poter essere rappresentati nel formato CSV, i dati gerarchici e raggruppati devono essere bidimensionali.  
  
 L'estensione per il rendering rende bidimensionale il report in una struttura ad albero che rappresenta i gruppi nidificati all'interno dell'area dati. Per rendere bidimensionale il report:  
  
-   Una gerarchia di righe viene resa bidimensionale prima di una gerarchia di colonne.  
  
-   Le colonne vengono ordinate nel modo seguente: caselle di testo presenti nel corpo da sinistra verso destra e quindi dall'alto verso il basso seguite dalle aree dati da sinistra verso destra e quindi dall'alto verso il basso.  
  
-   All'interno di un'area dati le colonne vengono ordinate nel modo seguente: membri di angolo, membri della gerarchia delle righe, membri della gerarchia delle colonne e quindi le celle.  
  
-   Le aree dati di pari livello sono aree dati o gruppi dinamici che condividono un'area dati o un predecessore dinamico comune. I dati di pari livello sono identificabili dalle diramazioni dell'albero bidimensionale.  
  
 Per altre informazioni, vedere [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
  
##  <a name="RenderingModes"></a> Modalità del renderer  
 L'estensione per il rendering CSV può operare in due modalità: una è ottimizzata per Excel, mentre l'altra è ottimizzata per applicazioni di terze parti che richiedono una rigida conformità alla specifica CSV del documento RFC 4180. Le aree dati di pari livello vengono gestite in modo diverso a seconda della modalità usata.  
  
### <a name="default-mode"></a>Modalità predefinita  
 La modalità predefinita è ottimizzata per Excel. Nella modalità predefinita il rendering del report viene eseguito come file CSV contenente più sezioni di dati di cui è stato eseguito il rendering in formato CSV. Ogni area dati peer è delimitata da una riga vuota. Il rendering di aree dati di pari livello all'interno del corpo del report viene eseguito come blocchi distinti di dati all'interno del file CSV. Il risultato è un file CSV in cui:  
  
-   Il rendering delle singole caselle di testo all'interno del corpo del report viene eseguito una sola volta come primo blocco di dati all'interno del file CSV.  
  
-   Il rendering di ciascuna area dati di pari livello di livello superiore nel corpo del report viene eseguito nel relativo blocco di dati.  
  
-   Il rendering delle aree dati nidificate viene eseguito in senso diagonale nello stesso blocco di dati.  
  
#### <a name="formatting"></a>Formattazione  
 Il rendering dei valori numerici viene eseguito nel relativo stato formattato. Excel è in grado di riconoscere valori numerici formattati, ad esempio valuta, percentuale e data, nonché di formattare le celle in modo appropriato durante l'importazione del file CSV.  
  
### <a name="compliant-mode"></a>Modalità conforme  
 La modalità conforme è ottimizzata per applicazioni di terze parti.  
  
#### <a name="data-regions"></a>Aree dati  
 Solo la prima riga del file contiene le intestazioni di colonna e ogni riga dispone dello stesso numero di colonne.  
  
#### <a name="formatting"></a>Formattazione  
 I valori non vengono formattati.  
  
##  <a name="Interactivity"></a> Interattività  
 L'interattività non è supportata da nessuno dei formati CSV generati da questo renderer. Non viene eseguito il rendering dei seguenti elementi interattivi:  
  
-   Collegamenti ipertestuali  
  
-   Elementi visualizzati o nascosti  
  
-   Mappa documento  
  
-   Collegamenti drill-through o click-through  
  
-   Ordinamento dell'utente finale  
  
-   Intestazioni fisse  
  
-   Segnalibri  
  
  
##  <a name="DeviceInfo"></a> Impostazioni relative alle informazioni sul dispositivo  
 È possibile cambiare alcune impostazioni predefinite per questo renderer, tra cui la modalità in cui eseguire il rendering, i caratteri da usare come delimitatori e i caratteri da usare come stringa predefinita del qualificatore di testo, modificando le impostazioni relative alle informazioni sui dispositivi. Per altre informazioni, vedere [CSV Device Information Settings](../../reporting-services/csv-device-information-settings.md).  
  
  
## <a name="see-also"></a>Vedere anche  
 [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Tipi di rendering &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funzionalità interattiva per estensioni per il rendering di report differenti &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Rendering degli elementi del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
