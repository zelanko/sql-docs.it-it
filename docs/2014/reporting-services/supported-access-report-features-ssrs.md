---
title: Caratteristiche supportate dei accesso Report (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], Access reports
- functions [Reporting Services]
- controls [Reporting Services]
- Access reports [Reporting Services]
- properties [Reporting Services], Access reports
- importing reports
- modules [Reporting Services]
ms.assetid: 7ffec331-6365-4c13-8e58-b77a48cffb44
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: e33547643adf7345bbbc7c020dcbd11959bb6119
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012030"
---
# <a name="supported-access-report-features-ssrs"></a>Caratteristiche supportate dei report di Access (SSRS)
  Quando si importa un report in Progettazione report, il processo di importazione converte il report di Access [!INCLUDE[msCoName](../includes/msconame-md.md)] in un file RDL (Report Definition Language) [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] supporta molte caratteristiche di Access; tuttavia, a causa delle differenze tra Access e [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], alcuni elementi vengono modificati leggermente o non sono supportati. In questo argomento vengono descritte le modalità di conversione delle caratteristiche dei report di Access in file RDL.  
  
## <a name="importing-access-reports"></a>Importazione di report di Access  
 Alcune query contengono codice specifico di Access. Il codice di Access non viene importato con il report. Inoltre, se una query contiene stringhe incorporate, il report potrebbe essere importato in modo non corretto. Per risolvere il problema, sostituire le stringhe con un codice con caratteri. Sostituire, ad esempio, il carattere virgola (,) con CHAR(34).  
  
 Il processo di importazione non supera correttamente il punto e virgola (;) o caratteri di markup XML (\<, > e così via) nelle informazioni della stringa di connessione. Se una stringa di connessione include un punto e virgola o un carattere di markup XML, sarà necessario impostare manualmente la password nel nuovo report dopo l'importazione.  
  
 Durante l'importazione non vengono importate le impostazioni di connessione o di timeout generale nella stringa di connessione. Potrebbe essere necessario correggere queste impostazioni dopo l'importazione del report.  
  
 Se si importa un report che include una query con parametri, la query non verrà convertita durante l'importazione del report. Per importare la query insieme al report, sostituire temporaneamente i parametri della query nel report di Access con valori hardcoded, quindi sostituirli nuovamente con i parametri di query dopo l'importazione.  
  
## <a name="page-layout"></a>Layout di pagina  
 Il layout di pagina di Access è diverso rispetto a quello di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. In Access gli elementi vengono organizzati in sezioni disposte verticalmente nella pagina. Queste sezioni possono includere l'intestazione e il piè di pagina del report, l'intestazione e il piè di pagina della pagina, gruppi e dettagli. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] offre un layout più flessibile. I raggruppamenti e il posizionamento dei dettagli vengono gestiti tramite aree dati ed è possibile posizionare più aree dati in qualsiasi punto nel corpo del report, anche in modo affiancato. Anche in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono disponibili sezioni distinte per l'intestazione e il piè di pagina della pagina, simili a quelle di Access.  
  
 Quando si importa un report da Access in Progettazione report, l'intestazione e il piè di pagina del report di Access vengono convertiti in intestazione e piè di pagina del report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Le sezioni dei gruppi e dei dettagli vengono convertite in un'area dati elenco. L'intestazione e il piè di pagina del report vengono inseriti nel corpo del report anziché in una sezione distinta. Ne consegue che gli elementi possono avere posizioni leggermente diverse rispetto al report di Access originale.  
  
> [!NOTE]  
>  In alcuni report di Access, elementi del report che apparentemente sono adiacenti potrebbero in realtà essere sovrapposti. Quando si importa il report con Progettazione report, questa sovrapposizione non viene corretta e può dar luogo a risultati inattesi in fase di esecuzione del report.  
  
## <a name="data-sources"></a>Origini dati  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] supporta origini dati OLE DB, ad esempio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se i report vengono importati da un progetto di Access (file con estensione adp), la stringa di connessione per l'origine dei dati viene recuperata dalla stringa di connessione presente nel file con estensione adp. Nel caso di report importati da database di Access (file con estensione mdb o accdb), è possibile che la stringa di connessione punti al database di Access e che sia necessario correggerla dopo l'importazione dei report. Se l'origine dei dati del report di Access è una query, le informazioni della query vengono archiviate nel file RDL senza modifiche. Se invece l'origine dei dati è una tabella, durante il processo di conversione viene creata una query in base al nome della tabella e ai campi in essa contenuti.  
  
## <a name="reports-with-custom-modules"></a>Report con moduli personalizzati  
 Se è presente personalizzato [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] codice contenuto all'interno dei moduli non viene convertito. Se vengono rilevati blocchi di codice durante il processo di importazione, un avviso viene generato e visualizzato nei **elenco attività** finestra.  
  
## <a name="report-controls"></a>Controlli dei report  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportati i seguenti controlli di Access, che vengono inclusi nelle definizioni dei report convertiti.  
  
|||||  
|-|-|-|-|  
|Image|Label|Riga|Rectangle|  
|SubForm|SubReport<br /><br /> **Nota** controllo mentre SubReport viene convertito nel report principale, il sottoreport vero e proprio viene convertito separatamente.|TextBox||  
  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono supportati i seguenti controlli:  
  
|||||  
|-|-|-|-|  
|BoundObjectFrame|CheckBox|ComboBox|CommandButton|  
|CustomControl|ListBox|ObjectFrame|OptionButton|  
|TabControl|ToggleButton|||  
  
 Se vengono rilevati questi controlli durante il processo di importazione, un avviso viene generato e visualizzato nei **elenco attività** finestra.  
  
 Gli altri controlli, ad esempio i controlli ActiveX e Office Web Components, non vengono importati. Se ad esempio un report di Access include un controllo grafico OWC, tale controllo non verrà convertito durante l'importazione del report.  
  
## <a name="report-properties"></a>Proprietà dei report  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le proprietà elencate di seguito, disponibili tramite l'interfaccia utente di Access. Le proprietà disponibili solo a livello di codice non sono supportate e quindi non sono presenti in questo elenco.  
  
|||||  
|-|-|-|-|  
|ColoreSfondo|StileSfondo|ColoreBordo|BorderStyle|  
|SpessoreBordo|BottomMargin|Espandibile (casella di testo)|Riducibile (casella di testo)|  
|Didascalia|FontBold|CarattereCorsivo|TipoCarattere|  
|FontSize|CarattereSottolineato|SpessoreCarattere|InterruzionePagina|  
|ColorePrimoPiano|Altezza|HideDuplicates|Hyperlink|  
|IsHyperlink|IsVisible|StampaSezioneUnita (gruppo)|Left|  
|LeftMargin|InclinazioneLinea|LineSpacing|CollegaCampiSecondari|  
|CollegaCampiMaster|NuovaRigaOColonna|PageFooter|PageHeader|  
|Pages|Immagine|EspansioneImmagine (report)|ReadingOrder|  
|RipetiSezione|RightMargin|RunningSum|SizeMode|  
|TextAlign|TOP|TopMargin|Larghezza|  
  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono supportate le proprietà elencate di seguito, disponibili tramite l'interfaccia utente di Access.  
  
|||||  
|-|-|-|-|  
|CanGrow (sezione)|CanShrink (sezione)|DecimalPlaces|FastLaserPrinting|  
|Filtro|ApplicaFiltro|Formato|FormatConditions|  
|ModalitàRaggruppamento|StampaSezioneUnita (sezione)|NumeralShapes|Orientamento|  
|TavolozzaDisegno|OrigineTavolozza|AllineamentoImmagine|PagineImmagine|  
|ModalitàRidimensImmagine|EspansioneImmagine (immagine)|BarreScorrimento|SpecialEffect|  
|Verticale||||  
  
## <a name="grouping"></a>Raggruppamento  
 In Access, i livelli di raggruppamento vengono definiti tramite la combinazione di tre proprietà, ovvero l'espressione di raggruppamento, la proprietà `GroupOn` e la proprietà `GroupInterval`. Un gruppo senza intestazione o piè di pagina di gruppo viene unito al gruppo in esso contenuto. Se il gruppo non contiene un altro gruppo, l'ordinamento viene applicato alla sezione corpo e il gruppo viene eliminato.  
  
## <a name="expressions"></a>Espressioni  
 In Access vengono utilizzate le espressioni per specificare i valori visualizzati nelle caselle di testo. Come linguaggio per le espressioni viene utilizzato [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], oltre ad alcune funzioni di aggregazione. Progettazione report converte queste espressioni di Access in espressioni report.  
  
### <a name="functions"></a>Funzioni  
 Nelle definizioni di report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] viene utilizzato [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET come linguaggio nativo per le espressioni, mentre in Access 2002 viene utilizzato Visual Basic. Nell'elenco seguente sono indicate le funzioni supportate da [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
#### <a name="array-functions"></a>Funzioni di matrice  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni di matrice seguenti:  
  
-   LBound  
  
-   UBound  
  
#### <a name="conversion-functions"></a>Funzioni di conversione  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni di conversione seguenti:  
  
|||||  
|-|-|-|-|  
|Asc|CBool|CByte|CCur|  
|CDate|CDbl|CDec|Chr|  
|Chr$|CInt|CLng|CSng|  
|CStr|CVar|CVDate|Formato|  
|FormatCurrency|FormatDateTime|FormatNumber|FormatPercent|  
|Hex|Hex$|Nz|Oct|  
|Oct$|Str|Str$|StrConv|  
|Val||||  
  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono supportate le funzioni di conversione seguenti:  
  
-   GUIDFromString  
  
-   StringFromGUID  
  
#### <a name="database-functions"></a>Funzioni di database  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni di database seguenti:  
  
|||||  
|-|-|-|-|  
|CreateReport|GetObject|HyperlinkPart|Partition|  
  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono supportate le funzioni di database seguenti:  
  
|||||  
|-|-|-|-|  
|CodeDb|CreateControl|CreateForm|CreateGroupLevel|  
|CreateObject|CreateReportControl|CurrentDb|CurrentUser|  
|DeleteControl|DeleteReportControl|Eval|IMEStatus|  
|SysCmd||||  
  
#### <a name="datetime-functions"></a>Funzioni di data/ora  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni di data/ora seguenti:  
  
|||||  
|-|-|-|-|  
|date|Date$|DateAdd|DateDiff|  
|DatePart|DateSerial|DateValue|Day|  
|Ora|Minuto|Month|MonthName|  
|Adesso|Secondo|Time|Time$|  
|Timer|TimeSerial|TimeValue|Giorno feriale|  
|WeekdayName|Year|||  
  
#### <a name="ddeole-functions"></a>Funzioni DDE/OLE  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono supportate le funzioni DDE/OLE seguenti:  
  
|||||  
|-|-|-|-|  
|DDE|DDEIntitate|DDERequest|DDESend|  
|LoadPicture||||  
  
#### <a name="domain-aggregate-functions"></a>Funzioni di aggregazione sui domini  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono supportate le funzioni di aggregazione sui domini seguenti:  
  
|||||  
|-|-|-|-|  
|DAvg|DCount|DFirst|DLast|  
|DLookup|DMax|DMin|DStDev|  
|DStDevP|DSum|DVar|DVarP|  
  
#### <a name="error-handling-functions"></a>Funzioni di gestione degli errori  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni per la gestione degli errori seguenti:  
  
|||||  
|-|-|-|-|  
|Err|Errore|Error$|IsError|  
  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non è supportata la funzione per la gestione degli errori seguente:  
  
-   CVErr  
  
#### <a name="financial-functions"></a>Funzioni finanziarie  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni finanziarie seguenti:  
  
|||||  
|-|-|-|-|  
|DDB|FV|IPmt|IRR|  
|MIRR|NPer|NPV|Pmt|  
|PPmt|PV|replica|SLN|  
|SYD||||  
  
#### <a name="interaction-functions"></a>Funzioni di interazione  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni di interazione seguenti:  
  
|||||  
|-|-|-|-|  
|Comando|Command$|CurDir|CurDir$|  
|DeleteSetting|Dir|Dir$|Environ|  
|Environ$|EOF|FileAttr|FileDateTime|  
|FileLen|FreeFile|GetAllSettings|GetAttr|  
|GetSetting|Loc|LOF|QBColor|  
|RGB|SaveSetting|Seek|SetAttr|  
|Shell|Spc|Scheda||  
  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono supportate le funzioni di interazione seguenti:  
  
|||||  
|-|-|-|-|  
|DoEvents|In|Input|Input$|  
  
#### <a name="inspection-functions"></a>Funzioni di ispezione  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni di ispezione seguenti:  
  
|||||  
|-|-|-|-|  
|IsArray|IsDate|IsEmpty|IsError|  
|IsNull|IsNumeric|IsObject|TypeName|  
|VarType||||  
  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono supportate le funzioni di ispezione seguenti:  
  
-   IsMissing  
  
#### <a name="math-functions"></a>Funzioni matematiche  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni matematiche seguenti:  
  
|||||  
|-|-|-|-|  
|Abs|Atn|Cos|Exp|  
|Fix|Int|File di log|Rnd|  
|Arrotondamento|Sgn|Sin|Sqr|  
|Tan||||  
  
#### <a name="message-functions"></a>Funzioni di messaggio  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non sono supportate le funzioni di messaggio seguenti:  
  
|||||  
|-|-|-|-|  
|InputBox|InputBox$|MsgBox||  
  
#### <a name="program-flow-functions"></a>Funzioni per flussi di esecuzione del programma  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni per flussi di esecuzione del programma seguenti:  
  
|||||  
|-|-|-|-|  
|Choose|IIf|Opzione||  
  
#### <a name="sql-aggregate-functions"></a>Funzioni di aggregazione SQL  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni aggregazione SQL seguenti:  
  
|||||  
|-|-|-|-|  
|Avg|Conteggio|Max|Min|  
|StDev|StDevP|Sum|Var|  
|VarP||||  
  
#### <a name="text-functions"></a>Funzioni di testo  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono supportate le funzioni di testo seguenti:  
  
|||||  
|-|-|-|-|  
|Formato|Format$|InStr|InStrRev|  
|LCase|LCase$|Left|Left$|  
|Len|LTrim|LTrim$|Mid|  
|Mid$|Sostituisci|Right|Right$|  
|RTrim|Space|Space$|StrComp|  
|StrConv|String|String$|StrReverse|  
|Trim|Trim$|UCase|UCase$|  
  
### <a name="constants"></a>Costanti  
 In Access non sono supportate le costanti specifiche di [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] (ad esempio, `vbTrue`) nelle espressioni, pertanto non è necessaria alcuna conversione. Esiste comunque un'eccezione, ovvero la parola chiave `Null`, che viene convertita in `System.DbNull.Value`.  
  
### <a name="parameters"></a>Parametri  
 Durante il processo di importazione, Progettazione report esegue un'analisi di ogni espressione in un report per individuare eventuali variabili non corrispondenti a nomi di campi o controlli. Queste variabili vengono aggiunte ai parametri del report.  
  
 I parametri delle stored procedure vengono sempre importati con il tipo di dati String. Dopo l'importazione del report è necessario modificare manualmente il parametro per utilizzare il tipo di dati corretto.  
  
### <a name="object-names"></a>Nomi di oggetti  
 In Access i campi possono avere lo stesso nome dei controlli, situazione non consentita in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. In [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 6.0 è consentito, a differenza di Visual Basic .NET, l'uso degli spazi nei nomi di variabile. Durante il processo di importazione, i nomi di tutti questi oggetti vengono sostituiti con nomi validi e vengono assegnati nomi univoci in presenza di più oggetti con lo stesso nome. Viene inoltre eseguita un'analisi di ogni espressione per sostituire con i nuovi nomi i nomi delle variabili corrispondenti agli oggetti rinominati.  
  
## <a name="rectangles-and-containment"></a>Rettangoli e contenitori  
 In una definizione di report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] i rettangoli possono contenere altri elementi del report. Qualsiasi rettangolo con una larghezza maggiore dell'elemento del report e che si sovrappone a più del 90% dell'area dell'elemento diventa un contenitore per l'elemento del report.  
  
## <a name="bitmaps"></a>Bitmap  
 Tutte le bitmap incorporate in un report vengono convertite in formato BMP durante l'importazione del report, indipendentemente dal formato iniziale. Ad esempio, se il report include file con estensione jpg e gif, nel report importato le risorse risultanti saranno file con estensione bmp. Le bitmap vengono archiviate come immagini incorporate nel report. Per informazioni sulle immagini incorporate, vedere [immagini &#40;Generatore Report e SSRS&#41;](report-design/images-report-builder-and-ssrs.md).  
  
## <a name="other-considerations"></a>Altre considerazioni  
 Per i report importati da Access sono valide anche le limitazioni seguenti, oltre a quanto indicato nelle sezioni precedenti:  
  
-   La formattazione condizionale non viene convertita.  
  
-   Il campo descrizione nelle proprietà del report in Access non viene convertito.  
  
  
