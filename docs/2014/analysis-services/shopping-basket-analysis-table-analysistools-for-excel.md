---
title: Shopping Basket Analysis (tabella AnalysisTools per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- shopping basket analysis
- mining model, association
- Table Analysis tools
- association [data mining]
- market basket analysis
ms.assetid: ba40cf43-f286-49ad-8316-70f5b11f1dae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dadc054a3f9927c09e9e236044dd5ddee7f3a9a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068682"
---
# <a name="shopping-basket-analysis-table-analysistools-for-excel"></a>Market basket analysis (Strumenti di analisi tabelle per Excel)
  ![Strumento per gli acquisti](media/tat-shopbskt.gif "Strumento per gli acquisti")  
  
 Lo strumento Market **Basket Analysis** consente di trovare `associations` i dati. Un'associazione può indicare quali elementi vengono frequentemente acquistati insieme. In data mining, questa tecnica è un metodo noto noto come *Market Basket Analysis*, usato per analizzare il comportamento di acquisto dei clienti in set di dati di grandi dimensioni. Gli esperti di marketing possono utilizzare le informazioni per consigliare prodotti correlati ai clienti e promuovere i prodotti correlati posizionandoli in prossimità nelle pagine Web, nei cataloghi o sugli scaffali.  
  
 Per utilizzare l'analisi di tipo Market basket analysis, gli elementi che si desidera analizzare devono essere correlati da un ID di transazione. Se, ad esempio, si analizzano tutti gli ordini ricevuti tramite un sito Web, ogni ordine dispone di un ID di ordine o di un ID di transazione associato a uno o più elementi acquistati.  
  
 Al termine dell'analisi dei dati da parte della procedura guidata, vengono creati due nuovi fogli di dati, **gruppi di elementi** del carrello acquisti e regole del carrello **acquisti**.  
  
 Il foglio di file dei **gruppi di elementi del carrello acquisti** contiene un elenco degli elementi che compaiono spesso insieme nelle transazioni. Questi raggruppamenti comuni sono denominati *set*di elementi. Il foglio di file contiene anche le statistiche, ad esempio il *supporto* e l' *accuratezza*, per facilitare la comprensione dell'importanza del set di elementi. Se sono disponibili informazioni sui prezzi, nel foglio di lavoro viene inoltre calcolata la somma del valore di tutti gli elementi correlati, per fornire un'indicazione del valore totale delle transazioni.  
  
 È possibile filtrare e ordinare le colonne nel report. Ad esempio, è possibile visualizzare solo i set di elementi con due o più prodotti oppure ordinare i set di elementi in base al **valore medio del cestino**.  
  
 Il foglio di riferimento Market **basket Rules** usa le statistiche derivate dall'analisi per creare regole sulle modalità di correlazione degli elementi. Ad esempio, una regola potrebbe essere che se i clienti acquistano il prodotto A, è molto probabile che acquistino il prodotto B. Le regole possono essere utilizzate per creare indicazioni. Per ogni regola sono presenti statistiche di supporto che consentono di valutare la forza potenziale della regola, in modo da poter creare un'indicazione solo se la regola supera una determinata soglia di probabilità.  
  
## <a name="using-the-shopping-basket-analysis-tool"></a>Utilizzo dello strumento Market basket analysis  
  
1.  Aprire una tabella di Excel contenente i dati appropriati. Nella cartella di lavoro di esempio fare clic sul foglio di lavoro Associazione.  
  
2.  Fare clic su **Shopping Basket Analysis**.  
  
3.  Nella finestra di dialogo Market **Basket Analysis** selezionare la colonna contenente l'ID della transazione, quindi scegliere la colonna che contiene gli elementi o i prodotti che si desidera analizzare.  
  
4.  È possibile aggiungere una colonna contenente i valori dei prodotti.  
  
5.  Fare clic su**Avanzate**per aprire la finestra di dialogo **impostazione parametri avanzati** . Aumentare il valore di **supporto minimo** per ridurre il numero di prodotti raggruppati come set di elementi. Aumentare la **probabilità minima della regola** per filtrare i set di elementi molto comuni.  
  
### <a name="requirements"></a>Requisiti  
 Per utilizzare lo strumento Market **Basket Analysis** , i dati devono essere archiviati in una tabella di Excel e devono contenere le colonne seguenti:  
  
-   Colonna contenente un ID univoco che rappresenta la transazione. L'ID può essere numerico o di testo, con una lunghezza tale da garantire che il valore in ogni riga sia univoco.  
  
-   Colonna contenente l'elemento o il prodotto che si sta analizzando.  
  
-   Colonna numerica facoltativa che rappresenta il prezzo o il valore di ogni elemento. Questa colonna viene utilizzata per aggregare il valore dei set di elementi in cui si trova ogni prodotto e può aiutare a comprendere il valore totale di determinate transazioni.  
  
## <a name="how-items-are-associated"></a>Modalità di associazione degli elementi  
 I singoli elementi analizzati devono essere raggruppati da un identificatore che rappresenta il case, la transazione o la circostanza. Come identificatore è pertanto necessario scegliere la colonna con l'ID di transazione e non il numero ID del cliente o del prodotto.  
  
 Quando lo strumento esamina i prodotti inclusi in ogni transazione, viene creato un set di elementi per ogni combinazione di elementi trovata. Se, ad esempio, un cliente ha acquistato tre elementi in una singola visita, vi sono sette possibili set di elementi: ogni prodotto considerato singolarmente, ogni prodotto raggruppato con uno degli altri prodotti e la combinazione di tutti e tre i prodotti.  
  
> [!NOTE]  
>  È possibile escludere tramite filtro i set di elementi che contengono singoli elementi, ma per generare statistiche significative per il set di dati è necessario che anche questi set vengano analizzati dallo strumento.  
  
 Il supporto per ogni set di elementi viene calcolato come numero di clienti che acquistano un set di elementi. Nell'esempio precedente se vi è un solo cliente che ha acquistato tre elementi, con sette possibili set di elementi, ognuno dei sette set di elementi ha un valore del supporto di 1. Come l'aumentare del numero di clienti e man mano che il numero di possibili combinazioni aumenta, potrebbe essere necessario molto più tempo per elaborare il report. Alcuni set di elementi potrebbero tuttavia disporre di supporto molto piccolo. Si potrebbe pertanto decidere di ridurre il tempo necessario per generare il report limitando il numero di elementi in ogni set a tre o meno elementi. In genere, i set di elementi più grandi hanno un supporto notevolmente inferiore, pertanto il compromesso è accettabile.  
  
## <a name="specifying-minimum-support-and-rule-probability"></a>Impostazione del supporto minimo e della probabilità delle regole  
 Con l'aumentare delle dimensioni del set di dati, il numero di possibili raggruppamenti di elementi e regole può diventare eccessivo. È tuttavia possibile controllare il numero di risultati restituiti dallo strumento, per concentrarsi solo sulle regole e sui set di elementi più importanti. È possibile impostare queste opzioni nella finestra di **dialogo parametri avanzati del carrello acquisti**.  
  
### <a name="minimum-support"></a>Supporto minimo  
 Il *supporto minimo* indica il numero di transazioni che devono contenere un particolare set di elementi affinché il set di elementi venga considerato significativo. Si potrebbe ad esempio essere interessati solo ai set di elementi acquistati in almeno dieci transazioni diverse. Esistono due modi per controllare la soglia per il significato del set di elementi ed entrambi utilizzano il parametro di **supporto minimo** .  
  
 **Come valore assoluto:** Immettere un numero che rappresenta il numero di transazioni contenenti gli elementi di destinazione. Se, ad esempio, si immette 10, nei risultati vengono inclusi tutti i set di elementi presenti in almeno dieci carrelli acquisti.  
  
 **Come percentuale:** Immettere un numero che rappresenta una percentuale dell'intera raccolta di set di elementi. Se, ad esempio, si specifica 10, tutti i set di elementi vengono contati e i set di elementi di destinazione che devono essere presenti costituiscono almeno il 10% del numero totale di set di elementi. Se si dispone di un set di dati di dimensioni molto grandi, l'utilizzo di una percentuale anziché di un numero può consentire di concentrarsi sui raggruppamenti di elementi più importanti.  
  
> [!NOTE]  
>  Tenere presente che il numero di set di elementi è diverso dal numero di transazioni nei dati. Ogni transazione può contenere più set di elementi, tuttavia la maggior parte dei set di elementi si ripete diverse volte nel set di dati.  
  
### <a name="rule-probability-and-rule-importance"></a>Probabilità e importanza delle regole  
 La probabilità di una regola descrive la possibilità di occorrenza del risultato della regola. La probabilità della regola viene calcolata utilizzando la frequenza dei set di elementi che supportano una regola. Se un set di elementi è presente molto raramente, la relativa probabilità sarà bassa.  
  
 Le regole con una probabilità elevata potrebbero tuttavia non essere sempre utili. Tali regole potrebbero indicare set di elementi acquistati frequentemente e che pertanto non è necessario promuovere ulteriormente. La priorità viene designata per misurare l'utilità di una regola. A volte una regola può avere una probabilità molto alta ma importanza bassa, perché la stima non fornisce nuove informazioni. Se, ad esempio, ogni set di elementi contiene uno stato specifico di un attributo, una regola che consente di eseguire la stima di tale stato è superflua, anche se la probabilità è estremamente alta.  
  
 Provare a utilizzare diverse impostazioni per vedere i diversi risultati e determinare quale impostazione consente di ottenere le regole più interessanti.  
  
## <a name="understanding-the-reports"></a>Informazioni sui report  
 Lo strumento Market **Basket Analysis** crea due report complementari. Il primo report, denominato **gruppi significativi di elementi identificati durante l'analisi**, fornisce un elenco di tutti i set di elementi trovati. È possibile utilizzare i nuovi strumenti per le tabelle in Microsoft Excel per ordinare, filtrare ed esplorare i dati.  
  
 Il secondo report, denominato Market **basket Rules**, indica il tipo di inferenza che può essere eseguito in base ai set di elementi elencati nel primo report. Mentre l'elenco di set di elementi è più utile per l'esplorazione e la comprensione dei dati, l'elenco di regole è più utile per l'esecuzione di stime e la creazione di indicazioni.  
  
### <a name="shopping-basket-item-groups-report"></a>Report Elementi nel pacchetto acquisti  
 Questo report contiene un elenco di tutte le combinazioni possibili di elementi individuate nel set di dati. Se, ad esempio, i dati della transazione contengono ordini, per ogni ordine lo strumento Market **Basket Analysis** calcola quante volte il singolo elemento è stato ordinato, quindi calcola tutte le combinazioni di tale elemento con altri elementi.  
  
 Nel report sono elencati i set di elementi individuati in ordine di accuratezza. L'accuratezza è un punteggio che indica l'importanza del set di elementi.  
  
|Colonna nel report|Informazioni contenute|  
|----------------------|-----------------------|  
|Pacchetto di elementi|Elenco dei set di elementi o combinazione di elementi.|  
|Dimensioni pacchetto|Numero di elementi inclusi nel set di elementi. È possibile applicare un filtro in questo campo per vedere solo le coppie di elementi, i singoli elementi e così via.|  
|Supporto|Numero di case in cui è presente la combinazione. È possibile ordinare questa colonna per visualizzare i set di elementi più comuni.|  
|Valore medio per vendita|Somma del valore degli elementi presenti solo in questo set di elementi, divisa per il supporto. È possibile ordinare e filtrare questa colonna per analizzare i prodotti in intervalli di prezzo diversi.|  
|Valore medio acquisti|Somma dei valori di tutti gli elementi negli ordini che contengono questo set di elementi, divisa per il supporto. Questa statistica è interessante quando abbinata al valore medio del set di elementi.|  
|Accuratezza|Punteggio che rappresenta il livello di interesse del set di elementi nell'intero set di dati. L'accuratezza viene calcolata determinando la probabilità con cui due elementi compaiono insieme e dividendo il valore trovato per la probabilità con cui due elementi compaiono indipendentemente. Se pertanto vi è una stretta correlazione tra gli elementi, il punteggio di accuratezza sarà più elevato.|  
  
### <a name="shopping-basket-rules-report"></a>Report Indicazioni sugli acquisti  
 Questo report contiene un set di regole generate analizzando i set di elementi trovati. Se, ad esempio, i dati della transazione indicano che i Prodotti A e B vengono spesso acquistati insieme, tramite lo strumento Market basket analysis viene creata una regola che consente di stimare A in base all'esistenza di B o B in base all'esistenza di A.  
  
 Ogni regola è associata a una probabilità, derivata dai dati di supporto. Queste probabilità sono utili quando si creano indicazioni. È ad esempio possibile visualizzare solo le regole con una probabilità di accuratezza del 50%, in base ai dati esistenti.  
  
 Nel report sono elencati i set di elementi individuati in ordine di accuratezza. L'accuratezza è un punteggio che indica l'importanza del set di elementi.  
  
|Colonna nel report|Informazioni contenute|  
|----------------------|-----------------------|  
|Elemento selezionato|Sono elencati gli elementi necessari per creare un'indicazione.<br /><br /> In data mining, questi elementi si dicono che si trovano sul *lato sinistro* della regola di associazione.|  
|Indicazione|È indicato l'elemento consigliato.<br /><br /> In data mining, questi elementi sono detti sul *lato destro* della regola di associazione.|  
|Probabilità|È indicata la probabilità di correttezza della regola.|  
|Supporto|È indicato il numero di case nei dati esistenti a sostegno della regola.|  
|Valore medio indicazione|Se si fornisce un valore per gli elementi nel carrello acquisti, in questa colonna viene calcolato il valore della stima, in base al costo degli elementi.|  
|Accuratezza|È indicata la forza della correlazione tra gli elementi nella prima colonna e quelli nella seconda colonna. Noto anche come *importanza*.<br /><br /> Un'accuratezza pari a 0 indica l'assenza di correlazione. Un valore positivo indica che gli elementi nella prima colonna consentono di stimare l'elemento nella seconda colonna. Più elevato è il numero, più forte è la correlazione.|  
  
## <a name="related-tools"></a>Strumenti correlati  
 Client di data mining per Excel è un componente aggiuntivo separato che fornisce funzionalità di data mining più avanzate e una procedura guidata per l'analisi delle associazioni. Per ulteriori informazioni, vedere [associazione guidata &#40;client di data mining per&#41;Excel ](associate-wizard-data-mining-client-for-excel.md).  
  
 Per ulteriori informazioni sull'algoritmo utilizzato per eseguire questa analisi, vedere l'argomento "Algoritmo Microsoft Association Rules" nella documentazione online di SQL Server.  
  
## <a name="see-also"></a>Vedi anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)  
  
  
