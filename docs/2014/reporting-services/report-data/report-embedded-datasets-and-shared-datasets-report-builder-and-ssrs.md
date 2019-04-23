---
title: Set di dati condivisi e incorporati del report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10420"
ms.assetid: c5852c8a-40e4-424d-a847-64eb151448ff
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea3e991cc936aed41350347f095f8e69d5025450
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59936129"
---
# <a name="report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs"></a>Set di dati condivisi e incorporati del report (Generatore report e SSRS)
  Un set di dati consente di specificare i dati che si desidera utilizzare da una connessione dati. È basato su una connessione dati salvata nel report come origine dati incorporata o come riferimento a un'origine dati condivisa su un server di report. Nel set di dati è inclusa una query che specifica un set di campi. Quando si trascinano questi campi nell'area di progettazione, è possibile creare espressioni che restituiscono i dati effettivi quando si esegue il report.  
  
 Esistono due tipi di set di dati:  
  
-   **Set di dati condivisi.** Un set di dati condiviso viene definito nel server di report. È possibile individuare il server per creare un set di dati condiviso o per selezionarne uno predefinito da aggiungere al report. Utilizzare un set di dati condiviso per fornire una query che può essere utilizzata da più report. I set di dati condivisi vengono archiviati nel server di report e possono essere gestiti separatamente dai report o dalle origini dati condivise. Ad esempio, un amministratore del server di report potrebbe aggiornare la query per sfruttare l'indicizzazione avanzata o un'altra ottimizzazione delle prestazioni di esecuzione delle query.  
  
-   **Set di dati incorporato.** Un set di dati incorporato viene definito e usato esclusivamente dal report in cui è incorporato. Utilizzare un set di dati incorporato quando si desidera ottenere dati da un'origine dati esterna da utilizzare solo in un unico report. I set di dati incorporati risultano utili quando si desidera creare una query senza altre dipendenze che non sia necessario utilizzare per più report.  
  
 In un set di dati sono inclusi anche parametri, filtri e opzioni dati che consentono di specificare informazioni sui caratteri in materia di distinzione tra maiuscole e minuscole, distinzione Kana, distinzione larghezza, distinzione tra caratteri accentati e non accentati e sensibilità alle regole di confronto.  
  
 ![rs_DatasetStory](../media/rs-datasetstory.gif "rs_DatasetStory")  
  
1.  **Set di dati nel riquadro dei dati del report** Un set di dati viene visualizzato nel riquadro dei dati del report in seguito alla creazione di un set di dati incorporato o l'aggiunta di un set di dati condiviso. Un set di dati è basato su un'origine dati.  
  
2.  **Progettazione query** Quando si progetta una query di database, viene visualizzata la finestra Progettazione query che è associata al tipo di origine dati.  
  
3.  **Comando di query** La finestra Progettazione query consente di compilare un comando di query. La sintassi del comando è determinata dal provider di dati.  
  
4.  **Estensione per i dati/Provider di dati** La connessione ai dati può avvenire attraverso più livelli di accesso ai dati.  
  
5.  **Origini dati esterne** È possibile recuperare dati da database relazionali, database multidimensionali, elenchi SharePoint, servizi Web o modelli di report.  
  
6.  **Risultati della query** È possibile eseguire la query e vedere un set di risultati di esempio. Per eseguire una query, è necessario disporre di credenziali per la fase di progettazione.  
  
7.  **Metadati da schema** Il provider di dati esegue un comando di query dello schema separato dalla query per recuperare metadati per la raccolta di campi dei set di dati. Ad esempio, un'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] `SELECT` restituisce i nomi di colonna per una tabella di database. Usare il riquadro dei dati del report per espandere il set di dati per visualizzare la raccolta di campi di un set di dati.  
  
 I dati inoltre possono essere inclusi in un report utilizzando set di dati condivisi predefiniti e parti del report. Tali elementi dispongono già delle informazioni necessarie sulla connessione dati. Per altre informazioni, vedere [aggiungere dati a un Report &#40;Generatore Report e SSRS&#41; ](report-datasets-ssrs.md) e [parti del Report &#40;Generatore Report e SSRS&#41;](../report-parts-report-builder-and-ssrs.md).  
  
 Per altre informazioni sui tipi di origini dati incorporati e sulle estensioni per i dati, vedere [Aggiunta di dati da origini dati esterne &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Overview"></a> Informazioni sui set di dati del report e sulle query  
 In un set di dati del report è contenuto un comando di query che viene eseguito sull'origine dati esterna e consente di specificare i dati da recuperare. Per compilare il comando di query, è possibile utilizzare la finestra Progettazione query associata all'estensione per i dati per l'origine dati esterna. In questa finestra è possibile eseguire il comando di query e visualizzare un set di risultati. Il set di risultati è un set di righe rettangolare che dispone di nomi di colonna e di righe con lo stesso numero di valori in ogni riga. I dati gerarchici, noti anche come *gerarchie incomplete*, non sono supportati. I nomi di colonna vengono salvati nella definizione del report come elenco di campi del set di dati.  
  
 Dopo avere aggiunto set di dati al report in uso, i campi dalle raccolte di campi del riquadro dei dati del report vengono trascinati nelle tabelle, nei grafici e in altri elementi del report utilizzati per progettare il layout del report. Per altre informazioni sull'utilizzo dei campi, vedere [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md).  
  
### <a name="understanding-data-from-a-report-dataset"></a>Informazioni sui dati da un set di dati del report  
 A seconda dell'estensione per i dati, un set di dati del report può essere costituito dai tipi di dati seguenti:  
  
-   Un set di risultati di un database relazionale restituito in seguito all'esecuzione di comandi di database, stored procedure o funzioni definite dall'utente. Se vengono recuperati più set di risultati tramite una singola query, solo il primo set di risultati viene elaborato e tutti gli altri vengono ignorati. Quando, ad esempio, si esegue la query riportata di seguito in Progettazione query basata su testo, nel riquadro dei risultati viene visualizzato solo il set di risultati per `Production.Product` :  
  
    ```  
    SELECT ProductID FROM Production.Product  
    GO  
    SELECT ContactID FROM Person.Contact  
    ```  
  
-   Un set di righe bidimensionale restituito da origini dati multidimensionali che utilizzano il protocollo XMLA (XML for Analysis). Alcuni provider di dati forniscono ulteriori proprietà di celle e dimensioni dall'origine dati, che non è possibile visualizzare nel set di risultati ma che sono disponibili nel report.  
  
-   Un set di risultati bidimensionale restituito da origini dati XML che includono elementi XML, con i relativi attributi ed elementi figlio.  
  
-   Un set di risultati restituito da qualsiasi provider di dati [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] registrato e configurato.  
  
-   Dati da un modello di report progettato per una specifica origine dati, con entità, relazioni di entità e campi predefiniti. Per altre informazioni, vedere la sezione relativa all'**uso di modelli di report** come origini dati della [documentazione di Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) nella documentazione online di SQL Server.  
  
 Quando il report viene elaborato in fase di esecuzione, il set di risultati effettivi restituito per una query può includere zero o più righe. È anche possibile che le colonne definite nella query non siano presenti nell'origine dati. Per i valori Null restituiti dall'origine dati viene eseguito il mapping al valore `System.DBNull.Value` di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
 Per altre informazioni sui campi del set di dati, vedere [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md).  
  
### <a name="dataset-query"></a>Query del set di dati  
 In fase di progettazione quando si esegue una query del set di dati in Progettazione query, viene visualizzato un set di righe dell'origine dati in cui sono riportati dati di esempio. In fase di esecuzione, quando un utente visualizza il report, la query del set di dati potrebbe produrre valori differenti in quanto i dati dell'origine dati sono stati modificati. Ogni volta che il report viene elaborato, potrebbero essere visualizzati nuovi dati.  
  
 Quando si definisce ciascun set di dati, in Generatore report si apre la Progettazione query che corrisponde al tipo di origine dati per consentire di progettare query. Per definire ad esempio una query per dati provenienti da un database relazionale di SQL Server, nelle procedure guidate relative a tabella, matrice, grafico e mappa viene visualizzata un'interfaccia grafica semplice che consente di compilare la query; infatti, si dovranno solo scegliere i campi desiderati nel set di dati.  
  
 In Progettazione query è possibile effettuare le seguenti operazioni:  
  
-   Passare dalla visualizzazione della query in formato grafico a quella basata su testo. Utilizzare l'interfaccia grafica per esplorare schemi, tabelle, viste e stored procedure sull'origine dati. Utilizzare la visualizzazione basata su testo per digitare, incollare o visualizzare una query esistente, utilizzata in genere per una query complessa che non può essere visualizzata nella finestra Progettazione query con interfaccia grafica. Ad esempio, è possibile importare una query da un file [!INCLUDE[tsql](../../../includes/tsql-md.md)] (con estensione sql), un report diverso sul server di report o un file di definizione del report (con estensione rdl) da una condivisione di file.  
  
-   Eseguire la query per visualizzare i dati. La query restituisce un set di risultati. Le colonne del set di risultati diventano la raccolta dei campi per il set di dati. Le righe del risultato diventano i dati per il set di dati. È possibile utilizzare la query fino a ottenere le colonne desiderate.  
  
-   Aggiungere parametri di query per recuperare solo i dati desiderati per il report. I parametri di query automaticamente generano i parametri del report corrispondenti. Per un'origine dati del modello di report, il filtro che si specifica automaticamente consente di generare un parametro del report corrispondente. I parametri del report consentono agli utenti di specificare i dati del report da visualizzare quando si esegue il report. Ad esempio, l'utente seleziona le categorie di prodotto per le quali si desiderano i dati e, quando si esegue il report, vengono visualizzati i dati solo per quelle categorie di prodotto nel report.  
  
-   Importare una query esistente da un altro report.  
  
 Le finestre Progettazione query possono fornire una modalità grafica o una modalità testo, a seconda del tipo di origine dati. Se si sceglie la modalità testo, è necessario utilizzare la sintassi di query adatta per l'origine dati.  
  
 Quando si definisce un set di dati del report, è possibile impostare le proprietà dei dati nella query oppure accettare quelle predefinite impostate dal provider di dati. È inoltre possibile modificare un tipo di dati mediante una delle strategie seguenti:  
  
-   Riscrivendo la query del set di dati in modo che converta un campo in un tipo di dati differente.  
  
-   Modificando il campo nel set di dati e specificando un formato personalizzato.  
  
-   Creando un nuovo campo personalizzato basato su un campo del database e specificando un formato personalizzato.  
  
 Per altre informazioni, vedere [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md).  
  
### <a name="importing-existing-queries-for-a-dataset"></a>Importazione delle query esistenti per un set di dati  
 Quando si crea un set di dati, è possibile creare una nuova query o importarne una esistente da un file o da un altro report. Quando si importa una query da un altro report, è possibile scegliere la query da importare dall'elenco di set di dati nel report.  
  
 Sono supportati solo i tipi di file con estensione sql e rdl. Le query MDX (Multidimensional Expression), DMX (Data Mining Prediction) e le query modelli (SMQL) possono essere generate solo dalla Progettazione query associata.  
  
##  <a name="Compare"></a> Confronto e creazione di set di dati condivisi e set di dati incorporati  
 Un set di dati incorporato è definito in un report o in una parte di report pubblicata. Le modifiche apportate a un set di dati incorporato influiscono solo su quel report o su quella parte di report.  
  
 Un set di dati condiviso è definito su un server di report o un sito di SharePoint, è basato su un'origine dati condivisa e può essere utilizzato da più report e parti di report. Le modifiche apportate a una definizione del set di dati condiviso influiscono su tutti i report e su tutte le parti di report che la utilizzano.  
  
 Quando si aggiunge un set di dati condiviso a un report, la raccolta campi del set di dati viene aggiornata alla definizione corrente sul server di report. Non si ricevono notifiche di aggiornamento quando le modifiche vengono apportate sul server di report. Per sincronizzare una copia locale della raccolta campi con le modifiche apportate alla definizione del set di dati condiviso sul server di report, è necessario aggiornare la raccolta campi locale. Per altre informazioni, vedere [Aggiunta, modifica e aggiornamento di campi nel riquadro dei dati del report &#40;Generatore report e SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
 Negli elementi del report pubblicati sono contenuti i set di dati incorporati e condivisi dai quali dipendono. Per altre informazioni, vedere [Parti del report e set di dati in Generatore report](report-parts-and-datasets-in-report-builder.md).  
  
 La differenza tra le origini dati incorporate e quelle condivise dipende dalle diverse modalità di creazione, archiviazione e gestione. Nella tabella seguente vengono riepilogate le differenze fra le origini dati incorporate e quelle condivise:  
  
|Descrizione|Origine dati<br /><br /> origine dati|Condivisa<br /><br /> origine dati|  
|-----------------|------------------------------|----------------------------|  
|La connessione dati è incorporata nella definizione del report.|![Disponibile](../media/greencheck.gif "Disponibile")||  
|Il puntatore alla connessione dati nel server di report è incorporato nella definizione del report.||![Disponibile](../media/greencheck.gif "Disponibile")|  
|Gestita nel server di report|![Disponibile](../media/greencheck.gif "Disponibile")|![Disponibile](../media/greencheck.gif "Disponibile")|  
|Richiesta per i set di dati condivisi||![Disponibile](../media/greencheck.gif "Disponibile")|  
|Richiesta per i componenti||![Disponibile](../media/greencheck.gif "Disponibile")|  
  
 In Progettazione report è possibile creare set di dati condivisi come parte di un progetto report e controllare se distribuirli a un server di report. Non è possibile accedere a un server di report e selezionare un set di dati condiviso da aggiungere al report in uso.  
  
 In Generatore report è possibile eseguire le operazioni seguenti:  
  
-   Per creare un set di dati condiviso, utilizzare visualizzazione di progettazione del set di dati condiviso. È possibile salvarlo in un server di report o in un sito di SharePoint per condividere con altri report. È inoltre possibile accedere al server di report e modificare il set di dati condiviso esistente. In questa visualizzazione è possibile compilare una query e impostare tutte le opzioni del set di dati. Per altre informazioni, vedere [Visualizzazione di progettazione set di dati condivisi &#40;Generatore report&#41;](../report-builder/shared-dataset-design-view-report-builder.md).  
  
-   Per aggiungere un set di dati condiviso al report, aprire Generatore report in visualizzazione di progettazione report. Nella procedura guidata o nel riquadro dei dati del report individuare il server di report e selezionare il set di dati condiviso da aggiungere al report. In questa visualizzazione non è possibile modificare la query eccetto per aggiungere campi. È possibile eseguire l'override di altre opzioni dei dati e aggiungere filtri. Non è possibile rimuovere filtri.  
  
 Nella tabella seguente vengono confrontate le proprietà configurabili per la definizione del set di dati condiviso nel server di report e quelle configurabili per l'istanza del set di dati condiviso nella definizione del report.  
  
|Proprietà|Note sulla configurazione per la definizione|Note sulla configurazione per l'istanza|  
|--------------|--------------------------------------------|------------------------------------------|  
|Testo della query|Configurare la query, anche definendola come espressione.|Impossibile modificare la query.|  
|Parametri della query|Non può fare riferimento ai parametri del report<br /><br /> Include valori predefiniti<br /><br /> Include un flag di sola lettura|Configurare parametri non contrassegnati come di sola lettura nella definizione|  
|Filtri|Definisci filtri|Impossibile visualizzare o modificare i filtri del set di dati che fanno parte della definizione<br /><br /> Può creare filtri aggiuntivi|  
|origine dati|Deve essere un'origine dati condivisa|Impossibile modificare l'origine dati condivisa|  
|Campi|Campi dal comando di query<br /><br /> I campi calcolati non fanno parte della definizione del set di dati|Visualizzare campi, ma non modificarli<br /><br /> La raccolta di campi è statica basata sulla query al momento dell'aggiunta del set di dati condiviso al report. Per aggiornare, fare clic su **Aggiorna campi** nella finestra di dialogo **Proprietà set di dati** . La raccolta di campi effettivi è qualsiasi risultato restituito dalla query corrente nella definizione.<br /><br /> Aggiungere campi calcolati|  
|Set di dati|Opzioni dei dati quale la distinzione tra maiuscole e minuscole|Eseguire l'override di opzioni dei dati nell'istanza|  
  
 Per altre informazioni sulla creazione di set di dati, vedere [Creazione di un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md) e la sezione dedicata agli [strumenti di Reporting Services](../tools/reporting-services-tools.md) nella [documentazione relativa a Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) inclusa nella documentazione online di SQL Server.  
  
##  <a name="SortGroupFilter"></a> Filtro, ordinamento e raggruppamento di dati in un set di dati  
 I dati in un set di dati provengono dall'esecuzione di un comando di query su un'origine dati esterna. La sintassi del comando di query per un'estensione per i dati consente di determinare se i dati possono essere ordinati o raggruppati. L'ordinamento e il raggruppamento vengono eseguiti nella query prima del recupero dei dati per un report. L'operazione di filtro viene eseguita invece dopo il recupero dei dati per un report.  
  
 Per altre informazioni, vedere [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
### <a name="filtering-data-in-a-dataset"></a>Filtro dei dati in un set di dati  
 I filtri del set di dati fanno parte della definizione del set di dati in un report. Utilizzare i filtri del set di dati per specificare quali dati di un set di dati includere in un report. Quando si specificano i filtri su un set di dati, in tutte le aree dati basate sul set di dati vengono visualizzati solo i dati che passano i filtri del set di dati.  
  
 I filtri fanno parte della definizione di un set di dati condiviso. I filtri del set di dati condiviso influiscono su tutti i report che includono il set di dati condiviso. Dopo avere aggiunto un set di dati condiviso al report o dopo avere aggiunto un componente con un set di dati condiviso dipendente, è possibile creare filtri del set di dati aggiuntivi. I filtri creati vengono utilizzati solo nel report in uso, non sono parte della definizione del set di dati condiviso sul server di report.  
  
 È possibile impostare filtri aggiuntivi su un'area dati o un gruppo di aree dati. Inoltre è possibile utilizzare una combinazione di parametri e filtri per consentire agli utenti di scegliere i dati che desiderano visualizzare nel report. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
### <a name="sorting-data-in-a-dataset"></a>Ordinamento dei dati in un set di dati  
 In un set di dati, l'ordinamento dei dati rappresenta l'ordine in base al quale i dati vengono recuperati dall'origine dati esterna. Si tratta dello stesso ordine che viene visualizzato quando si esegue la query in Progettazione query. Se la sintassi del comando di query supporta l'ordinamento, è possibile modificare la query per ordinare i dati nell'origine, prima che venga restituita come dati del report. Per una query [!INCLUDE[tsql](../../../includes/tsql-md.md)] , ad esempio, l'istruzione ORDER BY consente di controllare il tipo di ordinamento.  
  
 Per ordinare i dati dopo la restituzione al report, definire le espressioni di ordinamento su aree dati e gruppi di aree dati. Per altre informazioni, vedere l'argomento relativo al tipo specifico di area dati, ad esempio, [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
 Inoltre è possibile utilizzare una combinazione di parametri ed espressioni di ordinamento per consentire agli utenti di scegliere il tipo di ordinamento dei dati in un report. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
### <a name="grouping-data-in-a-dataset"></a>Raggruppamento di dati in un set di dati  
 Non è possibile raggruppare dati in un set di dati. Per l'aggregazione di dati in un set di dati, è possibile modificare il comando di query per calcolare le aggregazioni prima del recupero dei dati per un report. Tali valori sono noti come *aggregazioni server*. Nelle espressioni, per identificare questi valori come aggregazioni precalcolate, utilizzare la funzione Aggregate. Per altre informazioni, vedere [Funzione di aggregazione &#40;Generatore report e SSRS&#41;](../report-design/report-builder-functions-aggregate-function.md).  
  
##  <a name="Parameters"></a> Utilizzo di parametri e di set di dati  
 Per una query del set di dati incorporato contenente variabili di query, i parametri di query e i parametri del report corrispondenti vengono creati automaticamente. Durante l'esecuzione del report, il valore del parametro del report è collegato al parametro di query del set di dati. In questo modo, il comando di query che viene eseguito sull'origine dati esterna consente di includere i valori specificati per i parametri del report. I parametri del report consentono a un utente di scegliere i dati da visualizzare nel report. È possibile visualizzare in che modo i parametri di query e di report sono collegati nella pagina [Finestra di dialogo Proprietà set di dati, Parametri &#40;Generatore report&#41;](../dataset-properties-dialog-box-parameters-report-builder.md).  
  
 Per un set di dati condiviso, i parametri di query sono parte della definizione del set di dati condiviso che può essere gestita sul server di report indipendentemente da un report. Nell'elenco seguente viene descritto il supporto per i valori dei parametri di query:  
  
-   Può essere basato su un'espressione.  
  
-   Può includere valori predefiniti.  
  
-   Può essere impostato per la sola lettura. Non è possibile modificare i parametri di sola lettura in un'istanza del set di dati condiviso in un report.  
  
-   Non può includere riferimenti alla raccolta predefinita Parameters che rappresenta i parametri del report.  
  
 Per configurare i valori dei parametri di query per un set di dati condiviso, in modalità progettazione del set di dati, individuare e aprire un set di dati condiviso dal server di report e impostare le opzioni nella pagina [Finestra di dialogo Proprietà set di dati, Parametri &#40;Generatore report&#41;](../dataset-properties-dialog-box-parameters-report-builder.md). Per altre informazioni, vedere [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
 Per alcune origini dati multidimensionali, ad esempio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], la finestra Progettazione query con interfaccia grafica consente di specificare filtri query e di selezionare un'opzione per creare un parametro query corrispondente. Quando si seleziona l'opzione di parametro, l'estensione per i dati consente di creare automaticamente un set di dati del report separato per fornire valori disponibili per un elenco a discesa per quel parametro. Per impostazione predefinita, questi set di dati nascosti non vengono visualizzati nel riquadro dei dati del report.  
  
 I parametri del report collegati ai parametri di query consentono di filtrare i dati prima che questi vengano restituiti dall'origine dati esterna. È inoltre possibile filtrare i dati nel report creando filtri che sono parte della definizione del report. Per altre informazioni, vedere [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
### <a name="displaying-hidden-datasets"></a>Visualizzazione dei set di dati nascosti  
 Quando si crea una query con parametri per alcune origini dati multidimensionali, i set di dati che forniscono valori validi per il parametro vengono creati automaticamente. In alcune finestre Progettazione query, questa operazione viene eseguita specificando filtri e selezionando l'opzione per creare parametri. Per impostazione predefinita, tali set di dati, pur essendo visualizzabili, non vengono mostrati nel riquadro dei dati del report. Per altre informazioni, vedere [Visualizzazione di set di dati nascosti per i valori dei parametri di dati multidimensionali &#40;Generatore report e SSRS&#41;](show-hidden-datasets-for-parameter-values-multidimensional-data.md).  
  
##  <a name="Maps"></a> Utilizzo di mappe e di set di dati  
 Se si include una mappa nel report in uso, è necessario fornire dati spaziali. Questo tipo di dati può provenire da un set di dati del report, da una mappa nella raccolta mappe o dai file di forma ESRI. I dati spaziali provenienti da un report o da un file di forma ESRI non sono visualizzati come set di dati nel riquadro dei dati del report. Per altre informazioni, vedere [Mappe &#40;Generatore report e SSRS&#41;](../report-design/maps-report-builder-and-ssrs.md).  
  
##  <a name="Multiple"></a> Visualizzazione dei dati da più set di dati  
 Un report include in genere più set di dati. Nell'elenco seguente vengono descritte le diverse modalità di utilizzo dei set di dati presenti in un report:  
  
-   Per visualizzare i dati di ogni set di dati è necessario utilizzare un'area dati distinta. Per altre informazioni, vedere [Aree dati e mappe &#40;Generatore report e SSRS&#41;](../report-design/data-regions-and-maps-report-builder-and-ssrs.md).  
  
-   È possibile collegare più aree dati a un set di dati e fornire più viste degli stessi dati. Per altre informazioni, vedere [Collegamento di più aree dati allo stesso set di dati &#40;Generatore report e SSRS&#41;](../report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md).  
  
-   È possibile utilizzare i set di dati per fornire un elenco a discesa di valori o di valori predefiniti disponibili per un parametro del report. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
-   È possibile collegare dati correlati di più set di dati utilizzando parametri con report drill-through o sottoreport. Un report delle vendite può ad esempio mostrare dati riepilogativi per tutti i punti vendita e un collegamento drill-through può specificare l'identificatore del punto vendita come parametro di report con una query del set di dati che recupera le singole vendite per il punto vendita specificato. Per altre informazioni, vedere [Drill-through, drill-down, sottoreport e aree dati annidate &#40;Generatore report e SSRS&#41;](../report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md) e [Sottoreport &#40;Generatore report e SSRS&#41;](../report-design/subreports-report-builder-and-ssrs.md).  
  
-   Non è possibile visualizzare dati dettaglio di più set di dati in una singola area dati. È tuttavia, possibile visualizzare valori di funzioni predefinite o di aggregazione per più set di dati all'interno di un'area dati. Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../report-design/report-builder-functions-aggregate-functions-reference.md). Se è necessario combinare dati dettaglio di più set di dati in un'area dati, è necessario riscrivere la query in modo da recuperare i dati come singolo set di dati.  
  
##  <a name="NoRows"></a> Visualizzazione di un messaggio quando non sono disponibili righe di dati  
 Durante l'elaborazione del report, quando è in esecuzione la query di un set di dati, il set di risultati potrebbe non contenere righe. Nel report sottoposto a rendering un'area dati collegata a un set di dati vuoto viene visualizzata come area dati vuota. Al posto di tale area è possibile specificare il testo da visualizzare nel report sottoposto a rendering. È inoltre possibile specificare un messaggio per i sottoreport quando le query per tutti i set di dati non producono dati in fase di esecuzione. Per altre informazioni, vedere [Impostazione di una proprietà NoDataMessage per un'area dati &#40;Generatore report e SSRS&#41;](set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md).  
  
##  <a name="Options"></a> Impostazione delle opzioni del set di dati  
 Per le origini dati che supportano dati internazionali, potrebbe essere necessario impostare le proprietà di un set di dati che influiscono sull'ordinamento, le proprietà relative ai caratteri internazionali e la distinzione maiuscole/minuscole. Tali proprietà includono la distinzione tra maiuscole e minuscole, la larghezza, la distinzione dei caratteri accentati e le regole di confronto. Per altre informazioni, vedere "Considerazioni sul supporto internazionale per database e applicazioni di Motore di database" e "Utilizzo delle regole di confronto" nella [documentazione online di SQL Server](https://go.microsoft.com/fwlink/?linkid=98335). Per altre informazioni su come impostare queste proprietà, vedere [Finestra di dialogo Proprietà set di dati, Opzioni &#40;Generatore report&#41;](dataset-properties-dialog-box-options-report-builder.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-datasets-ssrs.md)  
  
  
