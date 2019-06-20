---
title: Lingue e regole di confronto (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Windows collations [Analysis Services]
- default collations
- languages [Analysis Services]
- sort orders [Analysis Services]
- language identifiers [Analysis Services]
- default languages
- collations [Analysis Services]
ms.assetid: 666cf8a7-223b-4be5-86c0-7fe2bcca0d09
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 62956774e203b1438de1ea07708940d0711053ac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079374"
---
# <a name="languages-and-collations-analysis-services"></a>Lingue e regole di confronto (Analysis Services)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta le lingue e le regole di confronto fornite dai sistemi operativi [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. Le proprietà `Language` e `Collation` vengono inizialmente impostate a livello di istanza durante l'installazione, ma in seguito possono essere modificate a livelli diversi della gerarchia di oggetti.  
  
 In (solo) un modello multidimensionale, è possibile impostare queste proprietà in un database o cubo: è anche possibile impostarle nelle traduzioni create per gli oggetti all'interno di un cubo.  
  
 Durante l'impostazione di `Language` e `Collation`, è possibile specificare le impostazioni usate dal modello di dati durante l'elaborazione e l'esecuzione di query oppure, solo per i modelli multidimensionali, è possibile creare un modello con più traduzioni in modo tale che gli utenti di lingua straniera possano usare il modello nella propria lingua. L'impostazione delle proprietà `Language` e `Collation` in modo esplicito in un oggetto (database, modello o cubo) è utile nelle situazioni in cui il server di produzione e l'ambiente di sviluppo sono configurati per impostazioni locali diverse e si vuole essere certi che la lingua e le regole di confronto corrispondano a quelle dell'ambiente di destinazione previsto.  
  
 Questo argomento include le sezioni seguenti:  
  
-   [Oggetti che supportano le proprietà Language e Collation](#bkmk_object)  
  
-   [Supporto della lingua in Analysis Services](#bkmk_lang)  
  
-   [Supporto delle regole di confronto in Analysis Services](#bkmk_collations)  
  
-   [Modificare la lingua o le regole di confronto predefinite per l'istanza](#bkmk_defaultLang)  
  
-   [Modificare la lingua o le regole di confronto per un cubo](#bkmk_cube)  
  
-   [Modificare la lingua e le regole di confronto all'interno di un modello di dati mediante XMLA](#bkmk_XMLA)  
  
-   [Ottimizzare le prestazioni per le impostazioni locali inglesi tramite EnableFast1033Locale](#bkmk_enablefast1033)  
  
-   [Supporto di GB18030 in Analysis Services](#bkmk_gb18030)  
  
##  <a name="bkmk_object"></a> Oggetti che supportano le proprietà Language e Collation  
 `Language` e `Collation` delle proprietà vengono spesso mostrate insieme: quando è possibile impostare `Language`, è anche possibile impostare `Collation`.  
  
 Le proprietà `Language` e `Collation` possono essere impostate negli oggetti seguenti:  
  
-   **Istanza**. Tutti i progetti distribuiti nell'istanza adotteranno la lingua e le regole di confronto dell'istanza, supponendo che la lingua e le regole di confronto non siano definite. Per impostazione predefinita, un modello multidimensionale lascia la lingua e le regole di confronto vuote. Quando viene distribuito il progetto, il database e i cubi risultanti ottengono la lingua e le regole di confronto dell'istanza.  
  
     Le proprietà Language e Collation vengono stabilite inizialmente durante l'installazione ma un amministratore può eseguirne l'override in Management Studio. Per informazioni dettagliate, vedere [Modificare la lingua o le regole di confronto predefinite per l'istanza](#bkmk_defaultLang) .  
  
-   **Database**. Per disattivare l'ereditarietà, è possibile impostare in modo esplicito la lingua e le regole di confronto a livello di progetto usato da tutti i cubi contenuti nel database. Se non diversamente specificato, tutti i cubi nel database otterranno la lingua e le regole di confronto specificate a questo livello. Se si programma e distribuisce regolarmente usando impostazioni locali diverse (ad esempio, si sviluppa la soluzione in un computer cinese ma la si distribuisce in un server di proprietà di una filiale francese), l'impostazione della lingua e delle regole di confronto a livello di database è il primo passaggio, quello più importante, per garantire che la soluzione funzioni nell'ambiente di destinazione. È consigliabile impostare queste proprietà all'interno del progetto (tramite il comando **Modifica database** del progetto).  
  
-   **Dimensione del database**. Anche se la finestra di progettazione mostra le proprietà `Language` e `Collation` per una dimensione del database, non è utile impostare le proprietà per questo oggetto. Le dimensioni del database non vengono usate come oggetti autonomi, pertanto potrebbe essere difficile se non impossibile usare le proprietà definite. Quando una dimensione si trova in un cubo eredita sempre le proprietà `Language` e `Collation` dal relativo elemento padre del cubo. Tutti i valori che potrebbero essere stati impostati per l'oggetto dimensione del database autonomo vengono ignorati.  
  
-   **Cubo**. In quanto struttura di query primaria, è possibile impostare la lingua e le regole di confronto a livello di cubo. Ad esempio, si potrebbero voler creare versioni di un cubo in più lingue, ad esempio versioni in inglese e in cinese, all'interno dello stesso progetto, dove per ogni cubo sono definite lingua e regole di confronto specifiche.  
  
     La lingua e le regole di confronto impostate per il cubo vengono usate da tutte le misure e le dimensioni incluse nel cubo. È possibile impostare proprietà delle regole di confronto più dettagliate solo se si creano traduzioni in un attributo della dimensione. In caso contrario, supponendo che non vi siano traduzioni a livello di attributo, ci sarà un unico set di regole di confronto per ogni cubo.  
  
 Inoltre, è possibile impostare `Language`, da solo, in un **Translation** oggetto.  
  
 Un oggetto Translation vien creato quando si aggiungono traduzioni a un cubo o una dimensione. `Language` fa parte della definizione di traduzione. `Collation` invece viene impostato per il cubo o a livello superiore ed è condiviso da tutte le traduzioni. Ciò è evidente nel codice XMLA di un cubo contenente traduzioni, dove si avranno più proprietà della lingua (una per ogni traduzione), ma un solo set di regole di confronto. Si noti che esiste un'eccezione per le traduzioni dell'attributo della dimensione, in cui è possibile eseguire l'override delle regole di confronto del cubo per specificare un set di regole di confronto dell'attributo che corrisponda alla colonna di origine (il motore di database supporta l'impostazione delle regole di confronto per singole colonne ed è frequente configurare le singole traduzioni per ottenere i dati dei membri da colonne di origine diverse). Per tutte le altre traduzioni invece la proprietà `Language` viene usata da sola senza la proprietà `Collation` conseguente. Per informazioni dettagliate, vedere [Traduzioni &#40;Analysis Services&#41;](translations-analysis-services.md).  
  
##  <a name="bkmk_lang"></a> Supporto della lingua in Analysis Services  
 La proprietà `Language` definisce le impostazioni locali di un oggetto usato durante l'elaborazione, l'esecuzione di query e con `Captions` e `Translations` per supportare gli scenari multilingue. Le impostazioni locali si basano su un identificatore di lingua, ad esempio l'inglese, e su un'area, ad esempio Stati Uniti o Australia, che definiscono ulteriormente le rappresentazioni di data e ora.  
  
 A livello di istanza, la proprietà viene impostata durante l'installazione e si basa sulla lingua del sistema operativo Windows del server (una delle 37 lingue, supponendo che sia installato un Language Pack). Non è possibile modificare la lingua nell'installazione.  
  
 Dopo l'installazione, è possibile eseguire l'override della proprietà `Language` mediante la pagina delle proprietà del server in Management Studio o nel file di configurazione msmdsrv.ini. È possibile scegliere tra molte più lingue, comprese tutte quelle supportate dal client Windows. Se impostata a livello di istanza nel server, la proprietà `Language` determina le impostazioni locali di tutti i database che vengono distribuiti successivamente. Se ad esempio la proprietà `Language` viene impostata sul tedesco, tutti i database distribuiti nell'istanza avranno 1031 come proprietà Language, ovvero l'identificatore LCID per il tedesco.  
  
###  <a name="bkmk_lcid"></a> Il valore della proprietà Language è un identificatore delle impostazioni locali (LCID)  
 I valori validi includono qualsiasi LCID visualizzato nell'elenco a discesa. In Management Studio e SQL Server Data Tools, gli LCID sono rappresentati in valori equivalenti in formato stringa. Le stesse lingue vengono visualizzate dovunque sia presente la proprietà `Language`, indipendentemente dallo strumento. Un elenco di lingue identico consente di implementare e testare le traduzioni in modo coerente in tutto il modello.  
  
 Sebbene in Analysis Services le lingue vengono elencate in base al nome, il valore effettivo archiviato per la proprietà è un LCID. Per l'impostazione di una proprietà della lingua a livello di codice o tramite il file msmdsrv.ini, usare l' [identificatore delle impostazioni locali (LCID)](http://en.wikipedia.org/wiki/Locale) come valore. Un LCID è un valore a 32 bit costituito da un ID lingua, un ID di ordinamento e bit riservati che identificano una particolare lingua. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa gli LCID per specificare la lingua selezionata per gli oggetti e le istanze di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 È possibile impostare l'identificatore LCID usando il formato decimale o esadecimale. Alcuni esempi di valori validi per il `Language` proprietà includono:  
  
-   0x0409 o 1033 per **Inglese (Stati Uniti)**  
  
-   0x0411 o 1041 per **Giapponese**  
  
-   0x0407 o 1031 per **Tedesco (Germania)**  
  
-   0x0416 o 1046 per **Portoghese (Brasile)** .  
  
 Per visualizzare un elenco più completo, vedere [ID delle impostazioni locali assegnati da Microsoft](https://msdn.microsoft.com/goglobal/bb964664.aspx). Per altre informazioni, vedere [codici](/windows/desktop/Intl/code-pages).  
  
> [!NOTE]  
>  La proprietà `Language` non determina la lingua in cui vengono restituiti i messaggi di sistema né le stringhe che vengono visualizzate nell'interfaccia utente. Errori, avvisi e messaggi vengono localizzati in tutte le lingue supportate in Office e Office 365 e vengono usati automaticamente quando la connessione client specifica le impostazioni locali supportate.  
  
##  <a name="bkmk_collations"></a> Supporto delle regole di confronto in Analysis Services  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Usa esclusivamente le regole di confronto binarie e di Windows. Non usa le regole di confronto datate di SQL Server. Un singolo set di regole di confronto viene usato in tutto il cubo ad eccezione delle traduzioni a livello di attributo. Per altre informazioni sulla definizione di traduzioni per gli attributi, vedere [Traduzioni &#40;Analysis Services&#41;](translations-analysis-services.md).  
  
 Le regole di confronto controllano la distinzione tra maiuscole/minuscole di tutte le stringhe di un alfabeto composto da due set di caratteri maiuscoli/minuscoli distinti ad eccezione degli identificatori di oggetto. Se si usano caratteri maiuscoli e minuscoli in un identificatore di oggetto, tenere presente che la distinzione tra maiuscole e minuscole degli identificatori di oggetto non è determinata dalle regole di confronto, ma da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per gli identificatori di oggetto creati con l'alfabeto inglese non verrà mai fatta distinzione tra maiuscole e minuscole, indipendentemente dalle regole di confronto. Per il cirillico e le altre lingue che usano un alfabeto composto da due set di caratteri maiuscoli/minuscoli distinti avviene il contrario, ovvero viene sempre fatta distinzione tra maiuscole/minuscole. Per informazioni dettagliate, vedere [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) .  
  
 Le regole di confronto di Analysis Services sono compatibili con quelle del motore di database relazionale di SQL Server, supponendo di mantenere la parità nelle opzioni di ordinamento selezionate per ogni servizio. Se ad esempio il database relazionale fa distinzione tra caratteri accentati e non accentati, è necessario configurare il cubo allo stesso modo. Se le impostazioni delle regole di confronto sono diverse, possono verificarsi dei problemi. Per un esempio e soluzioni alternative, vedere [Gli spazi vuoti in una stringa Unicode restituiscono risultati di elaborazione diversi in base alle regole di confronto](https://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx). Per altre informazioni sulle regole di confronto e sul motore di database, vedere [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
###  <a name="bkmk_collationtype"></a> Tipi di regole di confronto  
 Analysis Services supporta due tipi di regole di confronto:  
  
-   **Regole di confronto di Windows**  
  
     Le regole di confronto di Windows ordinano i caratteri in base alle caratteristiche linguistiche e culturali della lingua. In Windows le regole di confronto sono maggiori delle impostazioni locali (o delle lingue) con cui vengono usate poiché molte lingue condividono alfabeti e regole comuni per l'ordinamento e il confronto dei caratteri. Ad esempio, 33 impostazioni locali di Windows, incluse tutte le impostazioni locali di Windows portoghesi e inglesi, utilizzano la tabella codici Latino 1 (1252) e seguono un set comune di regole per l'ordinamento e il confronto dei caratteri.  
  
-   **Regole di confronto binarie (BIN o BIN2)**  
  
     Le regole di confronto binarie eseguono l'ordinamento in base a elementi di codice Unicode e non a valori linguistici. Ad esempio, Latin1_General_BIN e Japanese_BIN generano risultati di ordinamento identici se utilizzati su dati Unicode. Mentre un ordinamento linguistico potrebbe restituire risultati come aAbBcCdD, un ordinamento binario restituirà ABCDabcd perché l'elemento di codice di tutti i caratteri maiuscoli è complessivamente superiore rispetto agli elementi di codice dei caratteri minuscoli.  
  
###  <a name="bkmk_sortorder"></a> Opzioni di ordinamento  
 Le opzioni di ordinamento vengono usate per definire meglio le regole di ordinamento e confronto in base alla distinzione tra maiuscole e minuscole, caratteri accentati e non accentati, Kana e di larghezza. Ad esempio, il valore predefinito della proprietà di configurazione `Collation` per [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è Latin1_General_AS_CS, che specifica l'utilizzo delle regole di confronto Latin1_General insieme all'ordinamento con distinzione tra caratteri accentati e non accentati e tra maiuscole e minuscole.  
  
 Si noti che BIN e BIN2 sono reciprocamente esclusivi di altre opzioni di ordinamento, pertanto se si desidera usare BIN o BIN2, deselezionare l'opzione di ordinamento per la distinzione tra caratteri accentati e non accentati. Analogamente, se è selezionata l'opzione BIN2, non saranno disponibili le opzioni per effettuare o meno la distinzione tra maiuscole e minuscole, tra carattere accentati e non accentati, per la distinzione Kana e di larghezza.  
  
 Nella tabella seguente vengono descritte le opzioni di ordinamento delle regole di confronto di Windows con i suffissi associati per [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
|Ordinamento (suffisso)|Descrizione dell'ordinamento|  
|---------------------------|----------------------------|  
|Binario (_BIN) o BIN2 (_BIN2)|Esistono due tipi di regole di confronto binarie in SQL Server: le regole di confronto BIN meno recenti e le regole di confronto BIN2 più recenti. Nelle regole di confronto BIN2 tutti i caratteri vengono ordinati in base ai relativi elementi di codice. Nelle regole di confronto BIN solo il primo carattere viene ordinato in base all'elemento di codice e i restanti caratteri vengono ordinati in base ai relativi valori di byte. Poiché la piattaforma Intel si avvale di un'architettura little endian, i caratteri di codice Unicode vengono sempre scambiati con i byte archiviati.<br /><br /> Per le regole di confronto binarie nei tipi di dati Unicode, le impostazioni locali non vengono considerate ai fini dell'ordinamento dei dati. Ad esempio, l'utilizzo di Latin_1_General_BIN e Japanese_BIN su dati Unicode restituisce risultati di ordinamento identici.<br /><br /> L'ordinamento binario supporta la distinzione tra maiuscole e minuscole e tra caratteri accentati e non accentati e rappresenta inoltre il tipo di ordinamento più rapido.|  
|Distinzione maiuscole/minuscole (_CS)|Opera una distinzione tra lettere maiuscole e minuscole. Se viene selezionata questa opzione, le lettere minuscole precedono le versioni maiuscole corrispondenti nell'ordinamento. È possibile impostare in modo esplicito di non effettuare la distinzione tra maiuscole e minuscole specificando _CI. Le impostazioni relative ai caratteri maiuscoli/minuscoli specifiche delle regole di confronto non si applicano agli identificatori di oggetto, ad esempio all'ID di una dimensione, a un cubo e ad altri oggetti. Per informazioni dettagliate, vedere [Globalization Tips and Best Practices &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) .|  
|Distinzione caratteri accentati/non accentati (_AS)|Opera una distinzione tra caratteri accentati e non accentati. Il carattere 'a', ad esempio, non viene considerato uguale ad 'ấ'. Se questa opzione non è selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera identiche le versioni accentate e non accentate delle lettere ai fini dell'ordinamento. È possibile impostare in modo esplicito di non effettuare la distinzione tra caratteri accentati e non accentati specificando _AI.|  
|Distinzione Kana (_KS)|Opera una distinzione tra i due tipi di caratteri Kana giapponesi: Hiragana e Katakana. Se questa opzione non è selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera identici i caratteri Hiragana e Katakana ai fini dell'ordinamento. Non è disponibile un suffisso per l'ordinamento senza distinzione Kana.|  
|Distinzione larghezza (_WS)|Opera una distinzione tra la rappresentazione a un byte di un carattere e la rappresentazione a due byte dello stesso carattere. Se questa opzione non è selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera identica la rappresentazione a un byte e a byte doppio dello stesso carattere ai fini dell'ordinamento. Non è disponibile un suffisso per l'ordinamento senza distinzione di larghezza.|  
  
##  <a name="bkmk_defaultLang"></a> Modificare la lingua o le regole di confronto predefinite per l'istanza  
 La lingua e le regole di confronto predefinite vengono stabilite durante l'installazione, ma possono essere modificate come parte della configurazione post-installazione. La modifica delle regole di confronto a livello di istanza non è semplice e implica i requisiti seguenti:  
  
-   Riavvio del servizio.  
  
-   Aggiornamento delle impostazioni delle regole di confronto di oggetti esistenti. Le impostazioni delle regole di confronto vengono ereditate alla creazione dell'oggetto. Le successive modifiche alle regole di confronto devono essere eseguite manualmente. Per informazioni dettagliate, vedere [Modificare la lingua e le regole di confronto all'interno di un modello di dati mediante XMLA](#bkmk_XMLA) .  
  
-   Rielaborazione delle partizioni e delle dimensioni dopo l'aggiornamento delle regole di confronto.  
  
 Per modificare la lingua o le regole di confronto predefinite a livello di server, è possibile usare SQL Server Management Studio o PowerShell per AMO. In alternativa, è possibile modificare il  **\<lingua >** e  **\<CollationName >** impostazioni nel file msmdsrv. ini, specificando l'identificatore LCID della lingua.  
  
1.  In Management Studio fare clic con il pulsante destro del mouse sul nome del server | **Proprietà** | **Lingua/Regole di confronto**.  
  
2.  Scegliere le opzioni di ordinamento. Per selezionare **Binario** o **Binario 2**, deselezionare prima la casella di controllo **Distinzione caratteri accentati/non accentati**.  
  
     Si noti che le regole di confronto e la lingua sono impostazioni completamente indipendenti. Se si modifica un'impostazione, i valori dell'altra non vengono filtrati per visualizzare le combinazioni comuni.  
  
3.  Aggiornare il modello di dati per l'utilizzo delle nuove regole di confronto (vedere la sezione seguente).  
  
4.  Riavviare il servizio.  
  
##  <a name="bkmk_cube"></a> Modificare la lingua o le regole di confronto per un cubo  
  
1.  In Esplora soluzioni fare doppio clic sul cubo per aprirlo in Progettazione cubi.  
  
2.  Nel riquadro Misure o Dimensioni selezionare il nodo principale. L'oggetto di primo livello per entrambi i riquadri è il cubo.  
  
3.  In Proprietà impostare `Language` e `Collation`. I valori scelti verranno usati da tutti gli oggetti del cubo, incluse le dimensioni e le misure del cubo, e influiranno sulle sull'elaborazione e le operazioni di query.  
  
     L'unico modo per incorporare proprietà diverse per la lingua e le regole di confronto per gli oggetti all'interno del cubo è tramite le traduzioni. Per informazioni dettagliate, vedere [Traduzioni &#40;Analysis Services&#41;](translations-analysis-services.md).  
  
##  <a name="bkmk_XMLA"></a> Modificare la lingua e le regole di confronto all'interno di un modello di dati mediante XMLA  
 Le impostazioni della lingua e delle regole di confronto vengono ereditate alla creazione dell'oggetto. Le successive modifiche a tali proprietà devono essere eseguite manualmente. Un approccio per modificare rapidamente le regole di confronto per più oggetti è usare il comando ALTER in uno script XMLA.  
  
 Per impostazione predefinita, le regole di confronto vengono impostate una sola volta a livello di database. L'ereditarietà è implicita per tutta la gerarchia di oggetti. Se si imposta in modo esplicito `Collation` per gli oggetti all'interno del cubo, operazione consentita per i singoli attributi della dimensione, l'impostazione verrà visualizzata nella definizione di XMLA. In caso contrario, sarà presente solo la proprietà delle regole di confronto di livello superiore.  
  
 Prima di usare XMLA per modificare un database esistente, assicurarsi di non introdurre discrepanze tra il database e i file di origine usati per compilarlo. Ad esempio, si potrebbe voler usare XMLA per modificare rapidamente la lingua o le regole di confronto per il test di prova, ma continuare poi con le modifiche al file di origine (vedere [Modificare la lingua o le regole di confronto per un cubo](#bkmk_cube)), ridistribuendo la soluzione con le procedure operative esistenti già definite.  
  
1.  In Management Studio fare clic con il pulsante destro del mouse sul database | **Crea script per database** | **ALTER To** | **Nuova finestra editor di query**.  
  
2.  Cercare e sostituire la lingua o le regole di confronto esistenti con un valore diverso.  
  
3.  Premere F5 per eseguire lo script.  
  
4.  Rielaborare il cubo.  
  
##  <a name="bkmk_enablefast1033"></a> Ottimizzare le prestazioni per le impostazioni locali inglesi tramite EnableFast1033Locale  
 Se si utilizza l'identificatore di lingua Inglese (Stati Uniti) (0x0409 o 1033) come lingua predefinita per l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], è possibile ottenere ulteriori miglioramenti delle prestazioni impostando la proprietà di configurazione avanzata `EnableFast1033Locale`, disponibile solo per tale identificatore di lingua. Se si imposta il valore di questa proprietà su **true** , [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizzerà un algoritmo più veloce per il confronto e l'hashing di stringhe. Per altre informazioni sull'impostazione delle proprietà di configurazione, vedere [Configurare le proprietà del server in Analysis Services](server-properties/server-properties-in-analysis-services.md).  
  
##  <a name="bkmk_gb18030"></a> Supporto di GB18030 in Analysis Services  
 GB18030 è uno standard separato usato nella Repubblica popolare Cinese per la codifica dei caratteri cinesi. In GB18030, i caratteri possono essere di 1, 2 o 4 byte di lunghezza. In Analysis Services non viene eseguita alcuna conversione dei dati durante l'elaborazione dei dati da origini esterne. I dati vengono archiviati semplicemente in formato Unicode. In fase di query viene eseguita una conversione GB18030 tramite le librerie client di Analysis Services (in particolare, il provider OLE DB MSOLAP.dll) quando vengono restituiti i dati di testo nei risultati della query, in base alle impostazioni del sistema operativo client. Anche il motore di database supporta GB18030. Per informazioni dettagliate, vedere [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Scenari di globalizzazione per Analysis Services multidimensionale](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)   
 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)  
  
  
