---
title: Parametri report (Generatore report e Progettazione report) | Microsoft Docs
description: Questo argomento descrive le modalità d'uso comuni per i parametri report di Reporting Services, le proprietà impostabili e altre informazioni.
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.custom: ''
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.date: 12/06/2018
ms.openlocfilehash: 8592d3dfc16f0dd9d13a6445f0d8290f9ad507e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66499622"
---
# <a name="report-parameters-report-builder-and-report-designer"></a>Parametri report (Generatore report e Progettazione report)

::: moniker range="<=sql-server-2016||=sqlallproducts-allversions"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]

::: moniker-end

Questo argomento descrive gli usi comuni per i parametri di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , le proprietà che è possibile impostare e altre informazioni. I parametri del report consentono di controllare i dati del report, connettere report correlati e variare la presentazione del report. È possibile usare i parametri del report in report impaginati creati in [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] e Progettazione report, nonché in report per dispositivi mobili creati in [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]. Altre informazioni sui [Concetti relativi ai parametri di report](../../reporting-services/report-design/report-parameters-concepts-report-builder-and-ssrs.md).  

Per provare ad aggiungere un parametro a un report manualmente, vedere [Esercitazione: Aggiungere un parametro al report &#40;Generatore report&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md).  

## <a name="bkmk_Common_Uses_for_Parameters"></a> Utilizzi comuni per i parametri

 Di seguito sono elencate alcune delle modalità più comuni in cui è possibile usare i parametri.  
  
**Controllare i dati dei report per dispositivi mobili e impaginati**
  
- Filtrare i dati del report impaginato nell'origine dati scrivendo query del set di dati contenenti variabili.  
  
- Filtrare i dati da un set di dati condiviso. Quando si aggiunge un set di dati condiviso a un report impaginato, non è possibile modificare la query. Nel report è possibile aggiungere un filtro del set di dati che include un riferimento a un parametro di report creato.  
  
- Filtrare i dati da un set di dati condiviso in un report per dispositivi mobili di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per ulteriori informazioni, vedere [Create mobile reports with SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) .  
  
- Consentire agli utenti di specificare i valori per personalizzare i dati di un report impaginato. È ad esempio possibile fornire due parametri per la data di inizio e la data di fine dei dati di vendita.  
  
**Connettere report correlati**
  
- Usare parametri per correlare report principali a report drill-through, sottoreport e report collegati. Durante la progettazione di un set di report, ogni report viene progettato in modo da rispondere a domande specifiche. In particolare, ogni report è in grado di offrire una vista diversa o un livello di dettaglio diverso per le informazioni correlate. Per ottenere un set di report correlati tra loro, creare i parametri per i dati correlati nei report di destinazione.  
  
    Per altre informazioni, vedere [Report drill-through &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/drillthrough-reports-report-builder-and-ssrs.md), [Sottoreport &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md) e [Creare un report collegato](../../reporting-services/reports/create-a-linked-report.md).  

- Personalizzare set di parametri per più utenti. Creare due report collegati basati su un report relativo alle vendite sul server di report. In un report collegato vengono usati i valori di parametro predefiniti per i venditori mentre nel secondo report collegato vengono usati i valori di parametro predefiniti per i responsabili vendite. In entrambi i report viene usata la stessa definizione report.  
  
**Variare la presentazione del report**
  
- Inviare comandi a un server di report tramite una richiesta URL, per personalizzare il rendering di un report. Per altre informazioni, vedere [Accesso con URL &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md) e [Passare un parametro del report in un URL](../../reporting-services/pass-a-report-parameter-within-a-url.md).  
  
- Consentire agli utenti di specificare valori per personalizzare l'aspetto di un report. È ad esempio possibile fornire un parametro booleano per indicare se espandere o comprimere tutti i gruppi di righe nidificati in una tabella.  
  
- Consentire agli utenti di personalizzare l'aspetto e i dati del report includendo parametri in un'espressione.  
  
    Per altre informazioni, vedere [Riferimenti alla raccolta dei parametri &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md).  
  
## <a name="UserInterface"></a> Visualizzazione di un report con parametri

Quando si visualizza un report con parametri, ogni parametro viene visualizzato nella barra degli strumenti del visualizzatore di report in modo che gli utenti possano specificarne i valori in modo interattivo. La figura seguente illustra l'area dei parametri di un report contenente i parametri @ReportMonth, @ReportYear, @EmployeeID, @ShowAll, @ExpandTableRows, @CategoryQuota e @SalesDate.  

![Visualizzare report con parametri](../../reporting-services/report-design/media/ssrb-rptparamviewrpt.png "Visualizzare report con parametri")  
  
1. **Riquadro Parametri** Nella barra degli strumenti del visualizzatore di report vengono visualizzati un messaggio di richiesta e un valore predefinito per ogni parametro. È possibile personalizzare il layout dei parametri nel riquadro Parametri. Per altre informazioni, vedere [Personalizzare il riquadro dei parametri in un report &#40;Generatore report&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md).  
  
2. Parametro **@SalesDate**  Il parametro @SalesDate ha il tipo di dati **DateTime**. Accanto alla casella di testo viene visualizzata la richiesta di selezionare la data. Per modificare la data, digitare una nuova data nella casella di testo o usare il controllo calendario.  
  
3. Parametro **@ShowAll**  Il parametro @ShowAll ha il tipo di dati **Boolean**. Usare i pulsanti di opzione per specificare **True** o **False**.  
  
4. **Handle Mostra o nasconde l'area dei parametri** Nella barra degli strumenti del visualizzatore di report fare clic su questa freccia per mostrare o nascondere il riquadro dei parametri.  
  
5. Parametro **@CategoryQuota**  Il parametro @CategoryQuota ha il tipo di dati **Float** e di conseguenza accetta un valore numerico.  @CategoryQuota è impostato per consentire più valori.  
  
6. **Visualizza report**  Dopo aver immesso i valori dei parametri, fare clic su **Visualizza report** per eseguire il report. Se tutti i parametri hanno valori predefiniti, il report viene eseguito automaticamente a prima vista.  
  
## <a name="bkmk_Create_Parameters"></a> Creazione di parametri

È possibile creare i parametri dei report in alcuni modi diversi.
  
> [!NOTE]
>  Non tutte le origini dati supportano i parametri.
  
**Query o stored procedure del set di dati con parametri**
  
 Aggiungere una query del set di dati contenente variabili o una stored procedure del set di dati contenente parametri di input. Verrà creato un parametro del set di dati per ogni variabile o parametro di input e verrà creato un parametro di report per ogni parametro del set di dati.  
  
 ![Proprietà dei set di dati di parametri di Generatore report](../../reporting-services/report-design/media/ssrb-paramdatasetprops.png "Proprietà dei set di dati di parametri di Generatore report")  
  
 Questa immagine di Generatore report mostra:  
  
1.  I parametri del report nel riquadro dei dati del report.  
  
2.  Il set di dati con i parametri.  
  
3.  Il riquadro Parametri.  
  
4.  I parametri elencati nella finestra di dialogo Proprietà set di dati.  
  
 Il set di dati può essere incorporato o condiviso. Quando si aggiunge un set di dati condiviso a un report, non è possibile eseguire l'override dei parametri del set di dati contrassegnati come interni nel report. È possibile eseguire l'override dei parametri del set di dati che non sono contrassegnati come interni.  
  
 Per altre informazioni, vedere [Query del set di dati](#bkmk_Dataset_Parameters) più avanti in questo argomento.  
  
**Creare un parametro manualmente**
  
Creare manualmente un parametro dal riquadro dei dati del report. È possibile configurare i parametri del report in modo che un utente possa immettere in modo interattivo i valori per personalizzare il contenuto o l'aspetto di un report. È inoltre possibile configurare i parametri del report in modo che un utente non possa modificare i valori preconfigurati.  
  
> [!NOTE]  
>  Poiché i parametri vengono gestiti in modo indipendente nel server, la ripubblicazione di un report principale con nuove impostazioni dei parametri non implica la sovrascrittura delle impostazioni dei parametri esistenti per il report principale o per quello collegato.  
  
 **Parte del report con un parametro**
  
 Aggiungere una parte del report in cui siano inclusi riferimenti a un parametro o a un set di dati condiviso contenente variabili.  
  
 Le parti di report vengono archiviate sul server di report e possono quindi essere usate da altri utenti nei propri report. Le parti di report corrispondenti a parametri non possono essere gestite dal server di report. È possibile cercare i parametri in Raccolta parti del report e configurarli nel report dopo averli aggiunti. Per altre informazioni, vedere [Parti del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  I parametri possono essere pubblicati come parte del report separata per aree dati che dispongono di set di dati dipendenti con parametri. Sebbene i parametri siano elencati come parte del report, non è possibile aggiungere un parametro della parte del report direttamente a un report. Aggiungere invece la parte del report e tutti i parametri del report necessari vengono generati automaticamente da query del set di dati contenute o a cui fa riferimento la parte del report. Per altre informazioni sulle parti del report, vedere [Parti del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md) e [Parti del report in Progettazione report &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md).  
  
### <a name="parameter-values"></a>Valori di parametri

 Di seguito sono riportate le opzioni per selezionare i valori di parametri nel report.  
  
- Selezionare un singolo valore di parametro da un elenco a discesa.  
  
- Selezionare più valori di parametro da un elenco a discesa.  
  
- Selezionare un valore da un elenco a discesa per un parametro, che determina i valori disponibili nell'elenco a discesa per un altro parametro. Tali parametri sono definiti di propagazione. I parametri di propagazione consentono di filtrare successivamente i valori di parametro da migliaia di valori a un numero gestibile.  
  
     Per altre informazioni, vedere [Aggiungere parametri di propagazione a un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md).  
  
- Eseguire il report senza dovere selezionare prima un valore di parametro poiché per il parametro è stato creato un valore predefinito.  
  
## <a name="bkmk_Report_Parameters"></a> Proprietà dei parametri di report

 È possibile modificare le proprietà dei parametri di report mediante la finestra di dialogo Proprietà report. Nella tabella riportata di seguito vengono riepilogate le proprietà che è possibile impostare per ogni parametro.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|nome|Digitare un nome con distinzione tra maiuscole e minuscole per il parametro. Il nome deve iniziare con una lettera e contenere lettere, numeri e un carattere di sottolineatura (_). Il nome non può contenere spazi. Per i parametri generati automaticamente, il nome corrisponde al parametro nella query del set di dati. Per impostazione predefinita, i parametri creati manualmente sono simili a ParametroReport1.|  
|Messaggio di richiesta|Il testo che viene visualizzato accanto al parametro nella barra degli strumenti del visualizzatore di report.|  
|Tipo di dati|Un parametro di report deve corrispondere a uno dei seguenti tipi di dati:<br /><br /> Valore**booleano**. L'utente seleziona True o False mediante un pulsante di opzione.<br /><br /> **DateTime**. L'utente seleziona una data da un controllo calendario.<br /><br /> **Integer**. L'utente digita valori in una casella di testo.<br /><br /> **Float**. L'utente digita valori in una casella di testo.<br /><br /> **Text**. L'utente digita valori in una casella di testo.<br /><br /> Quando sono definiti valori disponibili per un parametro, l'utente seleziona i valori in un elenco a discesa, anche quando il tipo di dati corrisponde a **DateTime**.<br /><br /> Per altre informazioni sui tipi di dati di report, vedere [RDL Data Types](../../reporting-services/reports/report-definition-language-ssrs.md#bkmk_RDL_Data_Types).|  
|Consenti nessun valore|Selezionare questa opzione se il valore del parametro può corrispondere a una stringa vuota o a un valore vuoto.<br /><br /> Se si specificano valori validi per un parametro e si desidera che uno di essi sia un valore vuoto, è necessario includere tale valore come uno dei valori specificati. La selezione di questa opzione non include automaticamente un valore vuoto tra i valori disponibili.|  
|Consenti valore Null|Selezionare questa opzione se il valore del parametro può essere un valore Null.<br /><br /> Se si specificano valori validi per un parametro e si desidera che uno dei valori sia Null, è necessario includere tale valore come uno dei valori specificati. La selezione di questa opzione non include automaticamente un valore Null tra i valori disponibili.|  
|Consenti più valori|Fornire i valori disponibili per creare un elenco a discesa dal quale gli utenti possono scegliere. Si tratta di un metodo efficace per assicurarsi che nella query del set di dati vengano inviati solo valori validi.<br /><br /> Selezionare questa opzione se il valore per il parametro può essere costituito da più valori visualizzati in un elenco a discesa. I valori Null non sono consentiti. Se questa opzione è selezionata, verranno aggiunte caselle di controllo all'elenco di valori disponibili nell'elenco a discesa dei parametri. Nella parte superiore dell'elenco è inclusa una casella di controllo **Seleziona tutto**. Gli utenti possono selezionare i valori desiderati.<br /><br /> Se i dati che forniscono i valori cambiano rapidamente, l'utente potrebbe non visualizzare l'elenco più recente.|  
|Visibile|Selezionare questa opzione per visualizzare il parametro nella parte superiore del report durante l'esecuzione. Questa opzione consente agli utenti di selezionare i valori del parametro in fase di esecuzione.|  
|Hidden|Selezionare questa opzione per nascondere il parametro nel report pubblicato. I valori dei parametri di report possono comunque essere impostati su un URL del report, nella definizione di una sottoscrizione oppure nel server di report usando Gestione report.|  
|Interno|Selezionare questa opzione per nascondere il parametro di report. Nel report pubblicato, il parametro di report potrà essere visualizzato solo nella relativa definizione.|  
|Valori disponibili|Se sono stati specificati valori disponibili per un parametro, tali valori vengono sempre visualizzati sotto forma di elenco a discesa. Se si forniscono i valori disponibili per un parametro **DateTime** , ad esempio, nel riquadro del parametro viene visualizzato un elenco a discesa per le date invece di un controllo calendario.<br /><br /> Per assicurarsi che un elenco di valori sia coerente fra report e sottoreport, è possibile impostare un'opzione sull'origine dati per usare una sola transazione per tutte le query nei set di dati associati a un'origine dati.<br /><br /> **Nota sulla sicurezza** In qualsiasi report che includa un parametro con il tipo di dati **Text**, assicurarsi di usare un elenco di valori disponibili, noto anche come elenco di valori validi, e verificare che ogni utente che esegue il report abbia solo le autorizzazioni necessarie per visualizzare i dati del report. Per altre informazioni, vedere [Sicurezza &#40;Generatore report&#41;](../../reporting-services/report-builder/security-report-builder.md).|  
|Valori predefiniti|Impostare i valori predefiniti da una query o da un elenco statico.<br /><br /> Il report viene eseguito automaticamente a prima vista quando ogni parametro ha un valore predefinito.|  
|Advanced|Impostare l'attributo di definizione del report **UsedInQuery**, un valore che indica se questo parametro influisce direttamente o indirettamente sui dati di un report.<br /><br /> **Determina automaticamente quando eseguire l'aggiornamento**<br /> Scegliere questa opzione se si desidera che l'impostazione per questo valore venga determinata dal componente Elaborazione report. Questo valore è **True** se il componente Elaborazione report rileva una query del set di dati con un riferimento diretto o indiretto a questo parametro oppure se il report contiene sottoreport.<br /><br /> **Aggiorna sempre**<br /> Scegliere questa opzione quando il parametro di report viene usato direttamente o indirettamente in una query del set di dati o in un'espressione del parametro. Questa opzione determina l'impostazione di **UsedInQuery** su True.<br /><br /> **Non aggiornare mai**<br /> Scegliere questa opzione quando il parametro di report non viene usato direttamente o indirettamente in una query del set di dati o in un'espressione del parametro. Questa opzione determina l'impostazione di **UsedInQuery** su False.<br /><br /> **Attenzione** Usare **Non aggiornare mai** con cautela. Nel server di report **UsedInQuery** viene usato per consentire il controllo delle opzioni della cache per i dati dei report sottoposti a rendering e delle opzioni di parametro per i report snapshot. L'impostazione non corretta dell'opzione **Non aggiornare mai** potrebbe determinare la memorizzazione nella cache di report o dati del report non corretti o la presenza di dati non coerenti in un report snapshot. Per altre informazioni, vedere [Report Definition Language &#40;SSRS&#41;](../../reporting-services/reports/report-definition-language-ssrs.md).|  
  
##  <a name="bkmk_Dataset_Parameters"></a> Query del set di dati  
 Per filtrare i dati nella query del set di dati è possibile includere una clausola di restrizione che limita i dati recuperati specificando i valori da includere o escludere dal set dei risultati.  
  
 Usare Progettazione query per l'origine dati per compilare una query con parametri.  
  
-   Per query [!INCLUDE[tsql](../../includes/tsql-md.md)] , origini dati diverse supportano una sintassi diversa per i parametri. Supportare gli intervalli dei parametri identificati nella query in base alla posizione o al nome. Per altre informazioni, vedere gli argomenti sui tipi specifici di origini dati esterne in [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md). Nella finestra Progettazione query relazionale, è necessario selezionare l'opzione del parametro di filtro per creare una query con parametri. Per altre informazioni, vedere [Interfaccia utente di Progettazione query relazionale &#40;Generatore report&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md).  
  
-   Per query basate su un'origine di dati multidimensionale quale Microsoft SQL Server Analysis Services, SAP NetWeaver BI o Hyperion Essbase, è possibile specificare se creare un parametro basato su un filtro specificato in Progettazione query. Per altre informazioni, vedere l'argomento relativo alla progettazione query corrispondente all'estensione per i dati in [Strumenti di progettazione query &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md).  
  
##  <a name="bkmk_Manage_Parameters"></a> Gestione di parametri per un report pubblicato  
 Quando si progetta un report, i parametri corrispondenti vengono salvati nella definizione del report. Quando si pubblica un report, i parametri corrispondenti vengono salvati e gestiti separatamente della definizione del report.  
  
 Per un report pubblicato, è possibile usare gli elementi seguenti:  
  
-   **Proprietà del parametro di report.** Modificare i valori dei parametri del report direttamente nel server di report indipendentemente dalla definizione del report.  
  
-   **Report memorizzati nella cache.** Per creare un piano della cache per un report, ogni parametro deve avere un valore predefinito. Per altre informazioni, vedere [Memorizzazione dei report nella cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
-   **Set di dati condivisi memorizzati nella cache.** Per creare un piano della cache per un set di dati condiviso, ogni parametro deve avere un valore predefinito. Per altre informazioni, vedere [Memorizzazione dei report nella cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
-   **Report collegati.** È possibile creare report collegati con valori di parametri preimpostati per filtrare i dati per diverse tipologie di pubblico. Per altre informazioni, vedere [Creare un report collegato](../../reporting-services/reports/create-a-linked-report.md).  
  
-   **Sottoscrizioni di report.** È possibile specificare valori di parametri per filtrare i dati e recapitare report tramite sottoscrizioni. Per altre informazioni, vedere [Sottoscrizioni e recapito &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
-   **Accesso con URL.** È possibile specificare valori del parametro in un URL di un report. Inoltre è possibile eseguire report e specificare valori di parametri usando l'accesso a URL. Per altre informazioni, vedere [Accesso con URL &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md).  
  
 Le proprietà dei parametri per un report pubblicato vengono mantenute se si pubblica nuovamente la definizione del report. Se la definizione del report viene ripubblicata senza modifiche e i nomi dei parametri e i tipi di dati rimangono invariati, le impostazioni delle proprietà verranno mantenute. Se si aggiungono o eliminano parametri nella definizione del report oppure si modifica il tipo di dati o il nome di un parametro esistente, potrebbe essere necessario modificare le proprietà dei parametri nel report pubblicato.  
  
 Non è sempre possibile modificare tutti i parametri. Se un parametro di report ottiene un valore predefinito da una query del set di dati, non sarà possibile modificare tale valore per un report pubblicato né sarà possibile modificarlo nel server di report. Il valore usato in fase di esecuzione viene determinato al momento dell'esecuzione della query oppure, nel caso di parametri basati su espressioni, al momento della valutazione dell'espressione.  
  
 Le opzioni di esecuzione del report possono influire sulle modalità di elaborazione dei parametri. Per un report che viene eseguito come snapshot non è possibile usare parametri derivati da una query, a meno che la query non includa valori predefiniti per i parametri.  
  
##  <a name="bkmk_Parameters_Subscription"></a> Parametri per una sottoscrizione  
 È possibile definire una sottoscrizione per un report su richiesta o snapshot e specificare valori di parametri da usare durante l'elaborazione della sottoscrizione.  
  
-   **Report su richiesta.**  Per un report su richiesta, è possibile specificare un valore del parametro diverso dal valore pubblicato per ogni parametro elencato per il report. Si supponga, ad esempio, di usare il report delle chiamate al servizio di assistenza, per il quale viene usato un parametro *periodo di tempo* che consente di restituire i dati sulle richieste pervenute al servizio di assistenza ai clienti in un determinato giorno, settimana o mese. Se il valore predefinito del parametro per il report è impostato su **oggi**, la sottoscrizione può usare un valore diverso, ad esempio **settimana** o **mese**, per generare un report contenente dati settimanali o mensili.  
  
-   **Snapshot.**  La sottoscrizione deve usare i valori del parametro definiti per lo snapshot. Nella sottoscrizione non è possibile definire un valore di parametro per sostituire il valore di parametro definito per uno snapshot. Si supponga, ad esempio, di sottoscrivere un report delle vendite per le regioni meridionali che viene eseguito come snapshot del report e che per lo snapshot sia specificato **sud** come valore di parametro relativo alle regioni. In questo caso, se si crea una sottoscrizione di questo report, è necessario usare il valore di parametro **sud** nella sottoscrizione. Per consentire di individuare immediatamente i parametri che non possono essere modificati, i campi corrispondenti nella pagina di sottoscrizione sono di sola lettura.  
  
     Le opzioni di esecuzione del report possono influire sulle modalità di elaborazione dei parametri. Un report con parametri che viene eseguito come snapshot del report usano i valori dei parametri definiti per lo snapshot del report. I valori dei parametri vengono definiti nella pagina delle proprietà dei parametri del report. Per un report che viene eseguito come snapshot non è possibile usare parametri derivati da una query, a meno che la query non includa valori predefiniti per i parametri.  
  
     Se si modifica un valore di parametro nello snapshot del report dopo aver definito la sottoscrizione, questa viene disattivata dal server di report. La disattivazione della sottoscrizione indica che il report è stato modificato. Per attivare la sottoscrizione, aprirla e salvarla.  
  
> [!NOTE]  
>  Per le sottoscrizioni guidate dai dati è possibile usare valori di parametri ottenuti da un'origine dei dati del Sottoscrittore. Per altre informazioni, vedere [Usare un'origine dati esterna per i dati del Sottoscrittore &#40;sottoscrizione guidata dai dati&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
 Per altre informazioni, vedere [Sottoscrizioni e recapito &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
##  <a name="bkmk_Parameters_Security"></a> Parametri e sicurezza dei dati  
 Quando si distribuiscono report con parametri che contengono informazioni riservate è necessario fare attenzione. Un utente può facilmente sostituire un parametro di report con un valore diverso, con la conseguente diffusione di informazioni potenzialmente riservate.  
  
 Un'alternativa più sicura all'utilizzo di parametri per i dati personali o relativi ai dipendenti consiste nel selezionare i dati basati su espressioni che includono il campo **UserID** dalla raccolta Users. La raccolta Users consente di ottenere l'identità dell'utente che esegue il report e di usarla per recuperare i dati specifici per l'utente.  
  
> [!IMPORTANT]  
>  In qualsiasi report che includa un parametro di tipo **String**, accertarsi di usare un elenco di valori disponibili, noto anche come elenco di valori validi, e assicurarsi che ogni utente che esegue il report disponga solo delle autorizzazioni necessarie per visualizzare i dati del report. Quando si definisce un parametro di tipo **String**, viene visualizzata una casella di testo che può accettare qualsiasi valore. Un elenco di valori disponibili consente di limitare i valori che è possibile immettere. Se un parametro di report è correlato a un parametro del set di dati e non si usa un elenco di valori disponibili, un utente potrebbe digitare nella casella di testo sintassi SQL, esponendo il report e il server a un potenziale attacco intrusivo nel codice SQL. Se l'utente dispone di autorizzazioni sufficienti per eseguire la nuova istruzione SQL, è possibile che nel server si verifichino risultati non desiderati.  
>   
>  Se un parametro di report non è correlato a un parametro del set di dati e i valori del parametro sono inclusi nel report, un utente potrebbe digitare nel valore del parametro un URL o la sintassi di un'espressione ed eseguire il rendering del report in formato Excel o HTML. Se il report viene in seguito visualizzato da un altro utente che fa clic sul contenuto dei parametri di cui è stato eseguito il rendering, è possibile che venga inavvertitamente eseguito il collegamento o lo script dannoso.  
>   
>  Per ridurre il rischio di eseguire inavvertitamente script dannosi, aprire i report visualizzabili solo da origini attendibili. Per altre informazioni sulla sicurezza dei report, vedere [Garantire la sicurezza di report e risorse](../../reporting-services/security/secure-reports-and-resources.md).  

##  <a name="bkmk_Related_Topics"></a> Sezioni correlate  

 [Esercitazione: Aggiungere un parametro al report &#40;Generatore report&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)  
  
[Concetti relativi ai parametri di report](../../reporting-services/report-design/report-parameters-concepts-report-builder-and-ssrs.md)  
  
 [Esempi di report (Generatore report e SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
 [Uso delle espressioni nei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)  
  
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
 [Filtrare, raggruppare e ordinare i dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
 [Sicurezza &#40;Generatore report&#41;](../../reporting-services/report-builder/security-report-builder.md)  
  
 [Ordinamento interattivo, mappe documento e collegamenti &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)  
  
 [Drill-through, drill-down, sottoreport e aree dati annidate &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  
