---
title: Suggerimenti relativi alla progettazione di report (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c1490ff0-5b8a-43c1-8d22-e459395db4f6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e527b4059e225b012a2fa39cf21033b8af5ab9e2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081094"
---
# <a name="report-design-tips-report-builder-and-ssrs"></a>Suggerimenti relativi alla progettazione di report (Generatore report e SSRS)
  Usare i suggerimenti seguenti per progettare report impaginati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DesigningReports"></a> Progettazione di report  
  
-   Un report ben progettato fornisce le informazioni che determinano un'azione. Identificare le domande che potranno essere risposte mediante il report. Tenere presenti tali domande durante la progettazione del report.  
  
-   Per progettare visualizzazioni di dati efficienti, è importante visualizzare informazioni che siano di facile comprensione per l'utente del report. Scegliere un'area dati appropriata ai dati da visualizzare. Ad esempio, un grafico fornisce le informazioni aggregate e di riepilogo in modo più efficiente rispetto a una tabella che si estende su molte pagine contenenti informazioni dettagliate. È possibile visualizzare i dati di un relativo set in qualsiasi area dati, inclusi grafici, mappe, indicatori, grafici sparkline, barre dei dati e dati tabulari in vari layout griglia basati su una Tablix.  
  
-   Se si intende recapitare il report in un formato di esportazione specifico, testare il formato di esportazione quanto prima nella progettazione. Il supporto della funzionalità varia in base al renderer che si sceglie.  
  
-   Se si intende recapitare il report come sottoscrizione, testare la sottoscrizione quanto prima nella progettazione. Il supporto del parametro varia in base alla sottoscrizione che si crea.  
  
-   In caso di layout complessi è consigliabile compilarli in fasi. È possibile utilizzare i rettangoli come contenitori per organizzare gli elementi del report. Le aree dati possono essere compilate direttamente nell'area di progettazione per ingrandire l'area di lavoro e, non appena ogni area viene completata, è possibile trascinarla nel contenitore rettangolare. Utilizzando i rettangoli come contenitori, è possibile posizionare tutto il relativo contenuto in un unico passaggio. I rettangoli consentono inoltre di controllare il modo in cui viene eseguito il rendering degli elementi del report in ogni pagina.  
  
-   Per ridurre il disordine in un report, si consideri l'utilizzo della visibilità condizionale per elementi specifici del report e consentire all'utente di scegliere se mostrare gli elementi. La visibilità può essere impostata in base a un parametro o a un elemento Toggle della casella di testo. È possibile aggiungere in modo condizionale caselle di testo nascoste per mostrare risultati dell'espressione provvisori. Quando in un report vengono visualizzati dati imprevisti, la visualizzazione di questi risultati provvisori può facilitare il debug delle espressioni.  
  
-   Quando si usano elementi nidificati in rettangoli o celle della Tablix, è possibile impostare colori di sfondo diversi per il contenitore e gli elementi contenuti. Per impostazione predefinita, il colore di sfondo è impostato su **Nessun colore**. Gli elementi con un colore di sfondo specifico sono visibili attraverso gli elementi con un colore di sfondo impostato su **Nessun colore**. Questa tecnica agevola la selezione dell'elemento appropriato per l'impostazione delle proprietà di visualizzazione come la visibilità dei bordi per le celle della Tablix.  
  
 Per altre informazioni sui fattori da considerare per la progettazione di un report, vedere [Pianificazione di un report &#40;Generatore report&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md).  
  
##  <a name="NamingConventions"></a> Convenzioni di denominazione per report, origini dati e set di dati  
  
-   Usare convenzioni di denominazione per le origini dati e i set di dati che documentano l'origine dei dati.  
  
    1.  **Origini dati.** Se non si desidera usare un database o un server effettivo per motivi di sicurezza, usare un alias che indichi all'utente l'origine dei dati.  
  
    2.  **Set di dati.** Usare un nome che indichi su quale origine dati è basato.  
  
    3.  **Aree dati.** Indicare il tipo di area dati e i dati che vengono visualizzati. I nomi delle aree dati sono utili negli scenari seguenti:  
  
        1.  **Area dati come parte del report.** Quando gli autori di report sfogliano la Raccolta parti del report, un nome descrittivo agevola l'individuazione delle parti di cui sono alla ricerca.  
  
        2.  **Area dati come feed di dati.** Con le autorizzazioni appropriate, un lettore di report può creare un feed di dati ATOM da un'area dati.  
  
-   Utilizzare i caratteri di sottolineatura anziché gli spazi nei nomi dei report. Se si scarica un report da un portale Web [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , gli spazi vengono sostituiti da caratteri di sottolineatura. Se si usa la funzionalità di download per salvare i report in modalità locale, includendoli quindi in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], l'utilizzo dei caratteri di sottolineatura consente di preservare le dipendenze del report per i sottoreport e i collegamenti drill-through.  
  
##  <a name="Data"></a> Utilizzo dei dati  
  
-   Come primo passaggio, visualizzare nel riquadro dei dati del report tutti i dati che si desidera utilizzare. Man mano che si ridefiniscono le domande a cui il report dovrà fornire le risposte, limitare i dati presenti nei set di dati del report solo a quelli necessari.  
  
-   In generale, includere solo i dati che verranno visualizzati in un report. Utilizzare le variabili di query nelle query del set di dati per consentire all'utente di scegliere i dati che desidera visualizzare nel report. Se si creano set di dati condivisi, utilizzare filtri in base ai parametri del report per fornire la stessa funzionalità.  
  
-   Gli utenti esperti nella creazione di query potrebbero raggruppare i dati nel report anziché nella query per quantità di dati di medie dimensioni. Se si raggruppano tutti i dati nella query, il report tenderà a essere una presentazione del set di risultati della query. D'altra parte, per visualizzare valori aggregati per grandi quantità di dati in un grafico o in una matrice, non è necessario includere dati di dettaglio.  
  
-   A seconda dei requisiti è possibile visualizzare nomi e percorsi delle origini dati del report, testo di comandi di query del set di dati e valori di parametri nel report. La prima domanda che molti nuovi utenti si pongono riguarda l'origine dei dati. Per ridurre il disordine nel report, è possibile nascondere in modo condizionale le caselle di testo con questo tipo di informazioni e consentire agli utenti di scegliere se visualizzarle o meno. Provare ad aggiungere queste informazioni nell'ultima pagina del report. Impostare la visibilità delle caselle di testo in base a un parametro modificabile dall'utente.  
  
##  <a name="DesignSurface"></a> Interazione con l'area di progettazione del report  
 L'area di progettazione del report non è WYSIWIG. Quando si posizionano gli elementi del report nell'area di progettazione, la posizione relativa influisce sulla modalità di visualizzazione degli elementi nella pagina del report visualizzabile. Lo spazio vuoto viene mantenuto.  
  
-   Utilizzare le guide di allineamento e i pulsanti di layout per allineare e disporre gli elementi nell'area di progettazione del report. È ad esempio possibile allineare le parti superiori o i bordi degli elementi selezionati, espandere un elemento affinché corrisponda alle dimensioni di un altro elemento oppure regolare la spaziatura tra gli elementi.  
  
-   Utilizzare i tasti di direzione per regolare la posizione e le dimensioni degli elementi selezionati nell'area di progettazione. Ad esempio, le combinazioni di tasti seguenti sono molto utili:  
  
    -   **Tasti di direzione** Per spostare l'elemento del report selezionato.  
  
    -   **CTRL+Tasti di direzione** Per spostare l'elemento del report selezionato.  
  
    -   **CTRL+MAIUSC+Tasti di direzione** Per aumentare o diminuire le dimensioni dell'elemento del report selezionato.  
  
-   Per aggiungere un elemento a un rettangolo, utilizzare la punta superiore sinistra del mouse per puntare alla posizione iniziale dell'elemento nel contenitore rettangolare. Utilizzare le scelte rapide da tastiera per posizionare gli oggetti selezionati. Il rettangolo si espande automaticamente in base alle dimensioni degli elementi contenuti.  
  
-   Per aggiungere più elementi a una cella della Tablix, aggiungere prima un rettangolo e successivamente gli elementi.  
  
     Per impostazione predefinita, in ogni cella della Tablix è contenuta una casella di testo. Quando si aggiunge un rettangolo a una cella, il rettangolo sostituisce la casella di testo. Ad esempio, posizionare gli indicatori nidificati in un rettangolo di una cella della Tablix per controllare più facilmente l'espansione delle dimensioni di un grafico o di un indicatore quando si modifica l'altezza della riga in cui si trova la cella.  
  
-   Usare il controllo **Zoom** per regolare la vista dell'area di progettazione. È possibile usare la pagina intera o sezioni più piccole della pagina.  
  
-   Per trascinare i campi dal riquadro dei dati del report nel riquadro di raggruppamento, evitare di trascinare il campo attraverso altri elementi del report nell'area di progettazione perché in questo modo vengono selezionati gli altri elementi e viene deselezionata l'area dati Tablix. Trascinare il campo nel riquadro dei dati del report e successivamente nel riquadro di raggruppamento.  
  
###  <a name="Selecting"></a> Selezione degli elementi  
 Per agevolare la selezione dell'oggetto desiderato nell'area di progettazione del report, utilizzare il tasto ESC, il menu di scelta rapida visualizzato facendo clic con il pulsante destro del mouse su un elemento, il riquadro Proprietà e il riquadro di raggruppamento.  
  
-   -   Premere ESC per scorrere l'insieme di elementi del report che occupano lo stesso spazio nell'area di progettazione.  
  
    -   In alcuni elementi del report provare a utilizzare il menu di scelta rapida visualizzato facendo clic con il pulsante destro del mouse per selezionare l'elemento del report o la parte dell'elemento del report desiderata.  
  
    -   Nel riquadro Proprietà vengono visualizzate le proprietà relative alla selezione corrente.  
  
    -   Per utilizzare i gruppi di righe e i gruppi di colonne di un'area dati Tablix, selezionare il gruppo dal riquadro di raggruppamento.  
  
 In Progettazione report di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], è possibile effettuare una selezione da un elenco a discesa di oggetti sulla barra degli strumenti del riquadro Proprietà o dalla vista gerarchica di elementi del report nella finestra Struttura documento. È possibile selezionare gli elementi in questo riquadro e visualizzare quali elementi sono selezionati nell'area di progettazione. Per aprire la finestra Struttura documento, scegliere **Altre finestre** dal menu **Visualizza**, quindi fare clic su **Struttura documento**.  
  
##  <a name="ReportItems"></a> Utilizzo di tipi specifici di elementi del report  
  
###  <a name="Parameters"></a> Utilizzo dei parametri  
  
-   Lo scopo principale dei parametri del report è filtrare dati nell'origine dati e recuperare solo quelli necessari per il report.  
  
-   Per i parametri del report, trovare un equilibrio tra interattività e possibilità per un utente di ottenere i risultati desiderati. È possibile ad esempio impostare i valori predefiniti di un parametro sui valori che vengono utilizzati più di frequente.  
  
###  <a name="Text"></a> Utilizzo del testo  
  
-   Quando viene incollato in una casella di testo, il testo su più righe viene aggiunto come un'unica sequenza. Ogni sequenza di testo può essere solo formattata come unità. Per formattare ogni riga in modo indipendente, inserirne una nuova premendo INVIO nella sequenza di testo in base alle esigenze. La formattazione e gli stili possono essere applicati a ogni riga indipendente del testo nella casella di testo.  
  
-   È possibile impostare proprietà e azioni del formato in una casella di testo o in un testo segnaposto della casella di testo. Se è presente una sola riga di testo, risulta più efficace impostare le proprietà nella casella di testo anziché nel testo.  
  
###  <a name="Expressions"></a> Utilizzo delle espressioni  
  
-   Conoscere i formati di espressioni semplici e complesse. È possibile digitare il formato di espressioni semplici direttamente nelle caselle di testo, le proprietà nel riquadro Proprietà o in percorsi in finestre di dialogo che accettano un'espressione. Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
-   Quando si crea un'espressione, può essere opportuno creare ogni parte indipendentemente e verificarne il valore. È possibile quindi combinare tutte le parti in un'espressione finale. Una tecnica utile è aggiungere una casella di testo in una cella di matrice, visualizzare ogni parte dell'espressione e impostare la visibilità condizionale nella casella di testo. Per controllare il colore e lo stile del bordo quando la casella di testo è nascosta, posizionare innanzitutto la casella di testo in un rettangolo, quindi impostare il colore e lo stile del bordo del rettangolo in modo da corrispondere alla matrice.  
  
###  <a name="Indicators"></a> Utilizzo di indicatori  
  
-   Per impostazione predefinita, un indicatore mostra almeno tre stati. Dopo avere aggiunto un indicatore a un report, è possibile configurarlo aggiungendo o rimuovendo stati. Per agevolare la visualizzazione agli utenti, scegliere un indicatore che possa variare in base al colore e alla forma.  
  
##  <a name="Rendering"></a> Controllo del rendering degli elementi del report nella pagina del report  
  
-   Nell'area di progettazione del report le dimensioni degli elementi del report aumentano per adattarsi al contenuto su cui viene eseguito il mapping a l set di dati, all'espressione, al sottoreport o al testo associati.  
  
    -   Quando si posiziona un elemento nella pagina del report, la distanza tra l'elemento e tutti gli elementi che iniziano a destra di tale elemento diventa la distanza minima da mantenere quando le dimensioni di un elemento del report aumentano in orizzontale. Allo stesso modo, la distanza tra un elemento e l'elemento che si trova al di sopra diventa la distanza minima da mantenere quando le dimensioni dell'elemento che si trova nella parte superiore aumentano in verticale.  
  
    -   Le dimensioni di un elemento in un report aumentano in base ai dati da ricevere e tale elemento elimina gli elementi peer, ovvero gli elementi all'interno dello stesso contenitore padre, utilizzando le regole seguenti:  
  
    -   Ogni elemento viene spostato verso il basso in modo da mantenere lo spazio minimo tra l'elemento e gli elementi che terminano sopra di esso.  
  
    -   Ogni elemento viene spostato verso destra in modo da mantenere lo spazio minimo tra l'elemento e gli elementi che terminano alla sua sinistra. Per sistemi con layout da destra verso sinistra, ogni elemento viene spostato verso sinistra in modo da mantenere lo spazio minimo tra l'elemento e gli elementi che terminano alla sua destra.  
  
    -   I contenitori si espandono per adattarsi alle dimensioni degli elementi figlio. Per un elemento selezionato, la proprietà padre nel riquadro Proprietà consente di identificare il contenitore per l'elemento. È possibile usare anche il riquadro Struttura documento per visualizzare la gerarchia di contenimento degli elementi del report.  
  
    -   La barra degli strumenti **Layout** dispone di più pulsanti per facilitare l'allineamento di bordi, centri e spaziatura per gli elementi del report. Per abilitare la barra degli strumenti **Layout** , scegliere **Barre degli strumenti** dal menu **Visualizza**, quindi fare clic su **Layout**.  
  
-   Se si intende salvare il report come file pdf, è necessario impostare in modo esplicito la larghezza del report su un valore che fornisca i risultati desiderati nel formato del file di esportazione. Impostare, ad esempio, la larghezza della pagina del report esattamente su 7,9375 pollici e i margini sinistro e destro su 0,5 pollici.  
  
-   Usare le opzioni **Layout di stampa** e **Imposta pagina** nella barra degli strumenti del visualizzatore di report per eseguire il rendering di un report in una vista compatibile con la stampa. Per rimuovere le pagine orizzontali indesiderate, effettuare le operazioni seguenti:  
  
    1.  Rimuovere ogni spazio vuoto aggiuntivo tra le aree dati e sui bordi del report.  
  
    2.  Ridurre i margini della pagina nella finestra di dialogo **Proprietà report** .  
  
    3.  Usare i **Rettangoli** come contenitori per facilitare il controllo del rendering degli elementi del report.  
  
    4.  Nelle intestazioni di colonna modificare la proprietà della casella di testo WritingMode per usare il testo verticale.  
  
 La combinazione di questo comportamento, ovvero le proprietà relative alla larghezza e all'altezza degli elementi del report, le dimensioni del corpo del report, la definizione dell'altezza e della larghezza di pagina, le impostazioni dei margini del report padre e il supporto specifico del renderer per paging, consente di determinare quali elementi del report disporre in una pagina di cui è stato eseguito il rendering. Per altre informazioni, vedere [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Generatore report in SQL Server](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [Esercitazioni su Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)   
 [Esercitazioni di Generatore report](../../reporting-services/report-builder-tutorials.md)  
  
  
