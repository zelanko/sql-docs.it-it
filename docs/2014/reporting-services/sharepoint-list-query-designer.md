---
title: Progettazione query di elenco SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 593de30c-69f0-42a8-8467-16e78647b74c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 62428860419dd42b263b9408bb2c0d39514ca0e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101191"
---
# <a name="sharepoint-list-query-designer"></a>Progettazione query di elenco di SharePoint
  In Progettazione report sono disponibili due finestre Progettazione query, una con interfaccia grafica e una basata su testo, per la creazione di query in cui vengono specificati i dati da recuperare da un sito di SharePoint per un set di dati del report. Utilizzare la finestra Progettazione query con interfaccia grafica per esplorare i metadati dell'elenco SharePoint, compilare in modo interattivo una query e visualizzarne i risultati. Utilizzare Progettazione query basata su testo per visualizzare la query compilata nella finestra Progettazione query con interfaccia grafica, modificare una query o digitare i comandi della query. È inoltre possibile importare una query esistente da un file o un report.  
  
> [!IMPORTANT]  
>  Gli utenti accedono alle origini dati quando creano ed eseguono query. È necessario concedere autorizzazioni minime per le origini dati, ad esempio autorizzazioni di sola lettura.  
  
## <a name="graphical-query-designer"></a>Finestra Progettazione query con interfaccia grafica  
 Nella finestra Progettazione query con interfaccia grafica è possibile esploratore il sito di SharePoint, compilare in modo interattivo il comando che recupera dati dell'elenco SharePoint per un set di dati. È possibile scegliere i campi da includere nel set di dati e, facoltativamente, specificare filtri che limitano i dati nel set di dati. È possibile specificare che i filtri vengono utilizzati come parametri e forniscono il valore del filtro in fase di esecuzione.  
  
 Gli elenchi SharePoint includono numerosi campi specifici di SharePoint che potrebbero non essere utili nei report. La finestra Progettazione query fornisce un'opzione che consente di nascondere questi campi e rendere più semplice e veloce l'individuazione di quelli da utilizzare.  
  
 La finestra Progettazione query con interfaccia grafica è suddivisa in tre aree.  
  
-   Il riquadro di esplorazione nel quale si selezionano gli elementi dell'elenco e i campi da utilizzare.  
  
-   L'area di progettazione nella quale si compila la query.  
  
-   Il riquadro dei risultati nel quale si visualizzano i risultati della query.  
  
 Nella figura seguente è illustrata la finestra Progettazione query con interfaccia grafica quando è utilizzata con gli elenchi SharePoint.  
  
 ![rsQD_Relational_Graphical_SharePoint](media/rsqd-relational-graphical-sharepoint.gif "rsQD_Relational_Graphical_SharePoint")  
  
 Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
 [Elenchi SharePoint](#DatabaseView)  
 Visualizza elenchi SharePoint e i campi all'interno di ogni elemento nell'elenco.  
  
 [Campi selezionati](#SelectedFields)  
 Visualizza l'elenco dei nomi di campo dell'elenco SharePoint dagli elementi selezionati nel riquadro Elenchi SharePoint. Questi campi diventano la raccolta dei campi per il set di dati del report.  
  
 [Filtri applicati](#AppliedFilters)  
 Visualizza l'elenco dei campi e i criteri di filtro per tabelle o viste presenti nella Vista di database.  
  
 [Risultati query](#QueryResults)  
 Visualizza i dati di esempio per il set di risultati per la query generata automaticamente.  
  
###  <a name="DatabaseView"></a>Riquadro Elenchi SharePoint  
 Nel riquadro Elenchi SharePoint vengono visualizzati i metadati per gli oggetti di database per cui si dispone delle autorizzazioni per la visualizzazione. Tali oggetti sono determinati dalla connessione all'origine dati e dalle credenziali. Nella visualizzazione gerarchica, gli oggetti di database sono organizzati in base allo schema del database. Espandere il nodo di ogni schema per visualizzare tabelle, viste, stored procedure e funzioni con valori di tabella. Espandere la tabella o la vista per visualizzare le colonne.  
  
###  <a name="SelectedFields"></a>Riquadro campi selezionati  
 Il riquadro Campi selezionati visualizza i campi dell'elemento dell'elenco che si selezionano per gli elementi dell'elenco SharePoint. I campi visualizzati in questo riquadro diventano la raccolta dei campi per il set di dati del report. Dopo aver creato un set di dati e una query, utilizzare il riquadro dei dati del report per visualizzare la raccolta dei campi per un set di dati del report. Questi campi rappresentano i dati che si possono visualizzare in tabelle, grafici e altri elementi del report quando si visualizza un report.  
  
 Per aggiungere o rimuovere campi in questo riquadro, selezionare o deselezionare le caselle di controllo relative ai campi della tabella o della vista nel riquadro Elenchi SharePoint.  
  
###  <a name="AppliedFilters"></a>Riquadro filtri applicati  
 Nel riquadro Filtri applicati vengono visualizzati i criteri utilizzati per limitare il numero delle righe di dati recuperate in fase di esecuzione. I criteri specificati in questo riquadro sono usati per generare una clausola WHERE di [!INCLUDE[tsql](../includes/tsql-md.md)] . Quando si seleziona l'opzione di parametro, viene creato automaticamente un parametro del report. I parametri del report basati sui parametri di query consentono all'utente di specificare i valori affinché la query controlli i dati nel report.  
  
 Vengono visualizzate le colonne seguenti:  
  
-   **Nome campo** Consente di visualizzare il nome del campo a cui applicare i criteri.  
  
-   **Operatore** di Consente di visualizzare l'operazione da utilizzare nell'espressione di filtro.  
  
-   **Valore** di Consente di visualizzare il valore da utilizzare nell'espressione di filtro.  
  
-   **Parametro** di Consente di visualizzare l'opzione per l'aggiunta di un parametro di query alla query. Per visualizzare la relazione tra il parametro del report e il parametro della query, utilizzare Proprietà set di dati.  
  
###  <a name="QueryResults"></a>Riquadro risultati query  
 Nel riquadro Risultati query vengono visualizzati i risultati della query generata automaticamente in base alle selezioni negli altri riquadri. Le colonne nel set di risultati sono costituite dai campi che si specificano nel riquadro Campi selezionati e i dati di riga sono limitati dai filtri che si specificano nel riquadro Filtri applicati.  
  
 Questi dati rappresentano i valori dell'origine dati al momento dell'esecuzione della query. I dati non sono salvati nella definizione del report. I dati effettivi del report vengono recuperati quando il report viene elaborato.  
  
 L'ordinamento nel set dei risultati è determinato dall'ordine in base al quale i dati vengono recuperati dall'origine dati. L'ordinamento può essere cambiato tramite la modifica della query oppure dopo il recupero dei dati per il report.  
  
### <a name="graphical-query-designer-toolbar"></a>Barra degli strumenti della finestra Progettazione query con interfaccia grafica  
 Nella barra degli strumenti di Progettazione query relazionale sono disponibili i pulsanti seguenti, che consentono di specificare o visualizzare i risultati di una query.  
  
|Pulsante|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Consente di passare alla finestra Progettazione query basata su testo per visualizzare la query generata automaticamente o per modificare la query.|  
|**Importa**|Consente di importare una query esistente da un file o un report. Sono supportati i tipi di file con estensione sql e rdl.|  
|**Eseguire la query**|Consente di eseguire la query. Il set di risultati viene visualizzato nel riquadro Risultati query.|  
|**Mostra campi nascosti**|Consente di mostrare o nascondere i campi che sono stati generati automaticamente da SharePoint, quali ProgId e Level per gli elementi collegamento di SharePoint, ma che in genere non sono utilizzati nei report. Nascondendo questi campi, l'elenco dei campi diventa più breve e più facile da utilizzare.|  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di progettazione query in Reporting Services](../../2014/reporting-services/reporting-services-query-designers.md)  
  
  
