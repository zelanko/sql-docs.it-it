---
title: Globalizzazione suggerimenti e procedure consigliate (Analysis Services) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 57031c75e9433981b45419348ab2d5c0745edbfd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62659495"
---
# <a name="globalization-tips-and-best-practices-analysis-services"></a>Suggerimenti e procedure consigliate per la globalizzazione (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  [!INCLUDE[applies](../includes/applies-md.md)] solo a Multidimensional  
  
 Questi suggerimenti e linee guida consentono di aumentare la portabilità delle soluzioni di Business Intelligence e di evitare errori direttamente correlati alle impostazioni relative alla lingua e alle regole di confronto.  
  
##  <a name="bkmk_sameColl"></a> Usare regole di confronto simili in tutto lo stack  
 Se possibile, provare a usare le stesse impostazioni delle regole di confronto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usate per il motore di database, cercando di ottenere una corrispondenza nella distinzione tra maiuscole/minuscole, caratteri accentati/non accentati e di larghezza.  
  
 Per ogni servizio sono previste impostazioni delle regole di confronto specifiche con il valore predefinito del motore di database impostato su SQL_Latin1_General_CP1_CI_AS e Analysis Services impostato su Latin1_General_AS. Le impostazioni predefinite sono compatibili in termini di distinzione tra maiuscole/minuscole, caratteri accentati/non accentati e di larghezza. Tenere presente che se si modificano le impostazioni di un qualsiasi set di regole di confronto, possono verificarsi problemi quando le proprietà delle regole di confronto si differenziano in modo sostanziale.  
  
 Anche quando le impostazioni delle regole di confronto sono funzionalmente equivalenti, può verificarsi un caso speciale in cui uno spazio vuoto in un punto qualsiasi all'interno di una stringa viene interpretato in modo diverso da ogni servizio.  
  
 Il carattere spazio è un caso speciale perché può essere rappresentato come set di caratteri SBCS o DBCS in Unicode. Nel motore relazionale due stringhe composte separate da uno spazio, una con il set di caratteri SBCS e l'altra con il set di caratteri DBCS, vengono considerate identiche. In Analysis Services durante l'elaborazione, le stesse due stringhe composte non sono identiche e la seconda istanza verrà contrassegnata come duplicato.  
  
 Per altre informazioni e soluzioni alternative consigliate, vedere [Gli spazi vuoti in una stringa Unicode restituiscono risultati di elaborazione diversi in base alle regole di confronto](http://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx).  
  
##  <a name="bkmk_recos"></a> Indicazioni comuni per le regole di confronto  
 In Analysis Services viene sempre visualizzato l'elenco completo di tutte le lingue e le regole di confronto disponibili; le regole di confronto non vengono filtrate in base alla lingua selezionata. Assicurarsi di scegliere una combinazione fattibile.  
  
 Alcune delle regole di confronto usate più comunemente includono quelle presenti nell'elenco seguente.  
  
 Considerare questo elenco come un punto di partenza per un'analisi più approfondita anziché un suggerimento definitivo che esclude le altre opzioni. Potrebbe essere possibile che un set di regole di confronto non specificamente consigliato sia la soluzione più adatta per i dati usati. Solo tramite test approfonditi è possibile verificare se i valori dei dati vengono ordinati e confrontati in modo appropriato. Come sempre, assicurarsi di eseguire carichi di lavoro di query ed elaborazione durante il test delle regole di confronto.  
  
-   Latin1_General_100_AS viene spesso usato per applicazioni che usano i 26 caratteri dell' [alfabeto latino di base ISO](http://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet).  
  
-   Le lingue dell'Europa settentrionale che includono le lettere scandinave, ad esempio ø, possono usare Finnish_Swedish_100.  
  
-   Le lingue dell'Europa orientale, ad esempio il russo, usano spesso Cyrillic_General_100.  
  
-   La lingua e le regole di confronto cinesi variano in base all'area, ma sono in genere cinese semplificato o cinese tradizionale.  
  
     In Cina e a Singapore, il supporto tecnico Microsoft tende a usare il cinese semplificato con il pinyin come criterio di ordinamento preferito. Le regole di confronto consigliate sono Chinese_PRC (per SQL Server 2000), Chinese_PRC_90 (per SQL Server 2005) o Chinese_Simplified_Pinyin_100 (per SQL Server 2008 e versioni successive).  
  
     Taiwan è più comune per visualizzare il cinese tradizionale con l'ordinamento consigliato è basato sul numero: Chinese_Taiwan_Stroke (per SQL Server 2000), Chinese_Taiwan_Stroke_90 (per SQL Server 2005) o Chinese_Traditional_Stroke_Count_100 (per SQL Server 2008 e versioni successive).  
  
     Anche altre aree, ad esempio Hong Kong e Macao, usano il cinese tradizionale. Per le regole di confronto, a Hong Kong non è insolito usare Chinese_Hong_Kong_Stroke_90 (in SQL Server 2005). A Macao viene usato abbastanza spesso Chinese_Traditional_Stroke_Count_100 (in SQL Server 2008 e versioni successive).  
  
-   Per il giapponese, il set di regole di confronto usato più di frequente è Japanese_CI_AS. Japanese_XJIS_100 viene usato nelle installazione che supportano [JIS2004](http://en.wikipedia.org/wiki/JIS_X_0213). Japanese_BIN2 viene in genere usato nei progetti di migrazione dei dati, con dati provenienti da piattaforme non Windows o da origini dati diverse dal motore di database relazionale di SQL Server.  
  
     Japanese_Bushu_Kakusu_100 viene usato raramente nei server che eseguono carichi di lavoro di Analysis Services.  
  
-   Peri il coreano è consigliabile Korean_100. Sebbene Korean_Wansung_Unicode sia ancora disponibile nell'elenco, è stato deprecato.  
  
##  <a name="bkmk_objid"></a> Distinzione tra maiuscole/minuscole degli identificatori di oggetto  
 A partire da SQL Server 2012 SP2, la distinzione tra maiuscole/minuscole degli ID oggetto viene applicata indipendentemente dalle regole di confronto, ma il comportamento varia a seconda della lingua:  
  
|Alfabeto|Distinzione maiuscole/minuscole|  
|---------------------|----------------------|  
|**Alfabeto latino di base**|Gli identificatori di oggetto espressi in caratteri latini (una qualsiasi delle 26 lettere minuscole o minuscole in inglese) vengono trattati come valori senza distinzione tra maiuscole e minuscole, indipendentemente dalle regole di confronto. Ad esempio, gli ID oggetto seguenti verranno considerati identici: 54321**abcdef**, 54321**ABCDEF**, 54321**AbCdEf**. Internamente, Analysis Services considera i caratteri nella stringa come se fossero tutti in maiuscolo e quindi esegue un semplice confronto tra byte indipendente dalla lingua.<br /><br /> Si noti che sono interessati solo i 26 caratteri. Nel caso di una lingua dell'Europa occidentale, che usa però caratteri scandinavi, il carattere aggiuntivo non sarà in maiuscolo.|  
|**Cirillico, greco, copto, armeno**|Gli identificatori di oggetto in un alfabeto non latino composto da due set di caratteri maiuscoli/minuscoli distinti, ad esempio il cirillico, fanno sempre distinzione tra maiuscole e minuscole. Ad esempio, Измерение e измерение sono considerati due valori distinti, anche se l'unica differenza è rappresentata dal carattere minuscolo/maiuscolo della prima lettera.|  
  
 **Implicazioni della distinzione tra maiuscole/minuscole per gli identificatori di oggetto**  
  
 Il comportamento dei caratteri maiuscoli/minuscoli descritto nella tabella riguarda solo gli identificatori di oggetto e non i nomi degli oggetti. Se si noterà una differenza nella modalità di funzionamento della soluzione (dopo l'installazione di SQL Server 2012 SP2 o versioni successive), sarà probabilmente un problema di elaborazione. Le query non sono interessate dagli identificatori di oggetto. Per entrambi linguaggi di query (DAX e MDX), il motore delle formule usa il nome dell'oggetto (non l'identificatore).  
  
> [!NOTE]  
>  Le modifiche al codice correlate alla distinzione maiuscole/minuscole sono state considerate una modifica di rilievo per alcune applicazioni. Per altre informazioni, vedere [Modifiche di rilievo nelle funzionalità di Analysis Services in SQL Server 2016](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md) .  
  
##  <a name="bkmk_test"></a> Test delle impostazioni locali con Excel, SQL Server Profiler e SQL Server Management Studio  
 Durante il test delle traduzioni, la connessione deve specificare l'identificatore LCID della traduzione. Come illustrato nell'argomento relativo a come [ottenere una lingua diversa da SSAS in Excel](http://extremeexperts.com/sql/Tips/ExcelDiffLocale.aspx)è possibile usare Excel per testare le traduzioni.  
  
 A tale scopo, modificare manualmente il file con estensione odc in modo da includere la proprietà della stringa di connessione relativa all'identificatore delle impostazioni locali. Provare questa procedura con il database multidimensionale di esempio Adventure Works.  
  
-   Cercare i file odc esistenti. Quando si trova quello per il database multidimensionale Adventure Works, fare clic con il pulsante destro del mouse sul file per aprirlo nel Blocco note.  
  
-   Aggiungere `Locale Identifier=1036` alla stringa di connessione. Salvare e chiudere il file.  
  
-   Aprire Excel | **Dati** | **Connessioni esistenti**. Filtrare l'elenco per visualizzare solo i file delle connessioni presenti nel computer in uso. Trovare la connessione per Adventure Works (controllare il nome con attenzione perché potrebbero essercene più di uno). Aprire la connessione.  
  
     Verranno visualizzate le traduzioni francesi dal database di esempio Adventure Works.  
  
     ![Tabella pivot di Excel con traduzioni in francese](../analysis-services/media/ssas-localetest-excel.png "tabella pivot di Excel con traduzioni in francese")  
  
 È possibile poi usare SQL Server Profiler per verificare le impostazioni locali. Fare clic su un evento `Session Initialize` e quindi controllare l'elenco delle proprietà nell'area di testo sottostante per trovare `<localeidentifier>1036</localeidentifier>`.  
  
 In Management Studio è possibile specificare l'identificatore delle impostazioni locali in una connessione al server.  
  
-   In Esplora oggetti | **Connetti** | **Analysis Services** | **Opzioni**fare clic sulla scheda **Parametri aggiuntivi per la connessione** .  
  
-   Immettere `Local Identifier=1036` , quindi fare clic su **Connetti**.  
  
-   Eseguire una query MDX sul database Adventure Works. I risultati della query saranno le traduzioni francesi.  
  
     ![Query MDX con traduzioni in francese in SSMS](../analysis-services/media/ssas-localetest-ssms.png "query MDX con traduzioni in francese in SSMS")  
  
##  <a name="bkmk_mdx"></a> Scrittura di query MDX in una soluzione contenente traduzioni  
 Le traduzioni forniscono informazioni visualizzate relative ai nomi degli oggetti di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , ma gli identificatori degli oggetti corrispondenti non vengono tradotti. Se possibile, per gli oggetti di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è preferibile usare gli identificatori e le chiavi anziché didascalie e nomi tradotti. Per istruzioni e script DMX (Multidimensional Expressions), ad esempio, è consigliabile usare chiavi di membri anziché nomi di membri al fine di assicurare la portabilità in contesti con più lingue.  
  
> [!NOTE]  
>  Tenere presente che i nomi degli oggetti tabulari non fanno mai distinzione tra maiuscole e minuscole, indipendentemente dalle regole di confronto. I nomi degli oggetti multidimensionali invece rispettano la distinzione tra maiuscole e minuscole delle regole di confronto. Poiché solo i nomi degli oggetti multidimensionali fanno distinzione tra maiuscole e minuscole, assicurarsi che tutte le query MDX che fanno riferimento a oggetti multidimensionali siano digitate correttamente rispettando anche i caratteri maiuscoli/minuscoli.  
  
##  <a name="bkmk_datetime"></a> Scrittura di query MDX contenenti valori di data e ora  
 Di seguito sono riportati alcuni suggerimenti per aumentare la portabilità delle query MDX basate su data e ora tra le diverse lingue:  
  
1.  **Usare le parti numeriche per confronti e operazioni**  
  
     Quando si eseguono confronti e operazioni basati su mesi e giorni della settimana, usare le parti numeriche di data e ora anziché valori equivalenti in formato stringa, ad esempio usare MonthNumberofYear anziché MonthName. I valori numerici sono meno interessati da differenze nelle traduzioni delle lingue.  
  
2.  **Usare valori equivalenti in formato stringa in un set di risultati**  
  
     Per la creazione di set di risultati visualizzati dagli utenti finali, provare a usare la stringa, ad esempio MonthName, in modo che i destinatari multilingue possano trarre vantaggio dalle traduzioni fornite.  
  
3.  **Usare i formati di data ISO per informazioni di data e ora universali**  
  
     Uno [esperto di Analysis Services](http://geekswithblogs.net/darrengosbell/Default.aspx) consiglia: "Usare sempre il ISO Data formato aaaa-mm-gg per tutte le stringhe di data che passo nelle query in SQL o MDX perché non è ambiguo e funziona indipendentemente dalle impostazioni internazionali del server o client. Potrei essere d'accordo sul fatto che il server debba basarsi sulle proprie impostazioni internazionali durante l'analisi di un formato di data ambiguo, ma credo anche che se si ha un'opzione non aperta all'interpretazione il formato ISO rappresenta comunque la scelta migliore".  
  
4.  **Usare la funzione Format per applicare un formato specifico, indipendentemente dalle impostazioni locali della lingua**  
  
     La query MDX seguente, presa in prestito da un post del forum, illustra come usare la funzione Format per restituire le date in un formato specifico, indipendentemente dalle impostazioni internazionali sottostanti.  
  

    ```  
    WITH MEMBER [LinkTimeAdd11Date_Manual] as Format(dateadd("d",15,"2014-12-11"), "mm/dd/yyyy")  
    member [LinkTimeAdd15Date_Manual] as Format(dateadd("d",11,"2014-12-13"), "mm/dd/yyyy")  
    SELECT  
    { [LinkTimeAdd11Date_Manual]  
    ,[LinkTimeAdd15Date_Manual]  
    }  
    ON COLUMNS   
    FROM [Adventure Works]  
  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Scenari di globalizzazione per Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Scrittura di istruzioni Transact-SQL internazionali](../relational-databases/collations/write-international-transact-sql-statements.md)  
  
  
