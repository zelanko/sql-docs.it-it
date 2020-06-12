---
title: Definizione di una vista origine dati (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- names [Analysis Services], data source views
- name matching criteria [Analysis Services]
- Data Source View Wizard
- data source views [Analysis Services], creating
ms.assetid: 0bae4ee4-1742-40e9-bebe-17c788854484
author: minewiskan
ms.author: owend
ms.openlocfilehash: 21c7dd1e5ebe5e7b860a3b1f6a375772f236839c
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546943"
---
# <a name="defining-a-data-source-view-analysis-services"></a>Definizione di una vista origine dati (Analysis Services)
  Una vista origine dati contiene il modello logico dello schema utilizzato dagli [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oggetti di database multidimensionali, ovvero cubi, dimensioni e strutture di data mining. Una vista origine dati è la definizione di metadati, in formato XML, degli elementi dello schema utilizzati dal modello UDM (Unified Dimensional Model) e dalle strutture di data mining. Una vista origine dati ha le caratteristiche seguenti:  
  
-   Include i metadati che rappresentano oggetti selezionati da una o più origini dati sottostanti oppure i metadati che verranno utilizzati per generare un archivio dati relazionale sottostante, se per la generazione dello schema viene seguito l'approccio dall'alto verso il basso.  
  
-   Può essere compilata sulla base di una o più origini dei dati e questo consente la definizione di oggetti multidimensionali e di data mining che integrino i dati di più origini.  
  
-   Può contenere relazioni, chiavi primarie, nomi degli oggetti, colonne calcolate e query non presenti nell'origine dei dati sottostante e che esistono indipendentemente dalle origini dei dati sottostanti.  
  
-   Non è visibile e non è possibile eseguire query al suo interno tramite applicazioni client.  
  
 Una vista origine dati è un componente obbligatorio di un modello multidimensionale. La maggior parte degli sviluppatori di Analysis Services crea una vista origine dati durante le fasi iniziali della progettazione dei modelli, generando almeno una vista origine dati basata su un database relazionale esterno che fornisce i dati sottostanti. È tuttavia possibile creare la vista origine dati anche in una fase successiva, generando lo schema e le strutture di database sottostanti dopo la creazione di dimensioni e cubi. Questo secondo approccio, talvolta chiamato progettazione dall'alto verso il basso, viene in genere utilizzato per prototipi e modelli di analisi. Con tale approccio viene utilizzata la Generazione guidata schema per creare la vista origine dati sottostante e gli oggetti origine dati in base agli oggetti OLAP definiti in un progetto o un database di Analysis Services. Indipendentemente da come e quando si crea una vista origine dati, è necessario che ne sia disponibile una per ogni modello prima che sia possibile elaborarlo.  
  
 Questo argomento include le sezioni seguenti:  
  
 [Composizione della vista origine dati](#bkmk_dsvdef)  
  
 [Creare una vista origine dati tramite la Creazione guidata vista origine dati](#bkmk_startWiz)  
  
 [Impostare i criteri di corrispondenza nomi per le relazioni](#bkmk_NameMatch)  
  
 [Aggiungere un'origine dati secondaria](#bkmk_secondaryDS)  
  
##  <a name="data-source-view-composition"></a><a name="bkmk_dsvdef"></a>Composizione della vista origine dati  
 Una vista origine dati contiene gli elementi seguenti:  
  
-   Un nome e una descrizione  
  
-   Una definizione di qualsiasi subset dello schema recuperato da una o più origini dei dati, fino all'intero schema, comprendente quanto segue:  
  
    -   Nomi di tabella.  
  
    -   Nomi di colonna.  
  
    -   Tipi di dati.  
  
    -   Supporto di valori Null.  
  
    -   Lunghezze di colonna.  
  
    -   Chiavi primarie.  
  
    -   Relazioni tra chiave primaria e chiave esterna.  
  
-   Annotazioni relative allo schema delle origini dei dati sottostanti, comprendenti quanto segue:  
  
    -   Nomi descrittivi di tabelle, viste e colonne.  
  
    -   Query denominate che restituiscono colonne di una o più origini dei dati (visualizzate come tabelle nello schema).  
  
    -   Calcoli denominati che restituiscono colonne di un'origine dei dati (visualizzate come colonne in tabelle o viste).  
  
    -   Chiavi primarie logiche, necessarie in assenza di una chiave primaria definita nella tabella sottostante o inclusa nella vista o nella query denominata.  
  
    -   Relazioni tra chiave esterna e chiave primaria logica tra tabelle, viste e query denominate.  
  
##  <a name="create-a-dsv-using-the-data-source-view-wizard"></a><a name="bkmk_startWiz"></a>Creare una vista origine dati utilizzando la creazione guidata vista origine dati  
 Per creare una vista origine dati, eseguire la Creazione guidata vista origine dati da Esplora soluzioni in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
> [!NOTE]  
>  In alternativa, è possibile creare inizialmente dimensioni e cubi e successivamente generare una vista origine dati per il modello tramite la Generazione guidata schema. Per altre informazioni, vedere [Generazione guidata schema &#40;Analysis Services&#41;](schema-generation-wizard-analysis-services.md).  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse sulla cartella Viste origine dati e quindi scegliere **Nuova vista origine dati**.  
  
2.  Specificare un oggetto origine dati nuovo o esistente per fornire informazioni di connessione a un database relazionale esterno (la creazione guidata consente di selezionare una sola origine dati).  
  
3.  Nella stessa pagina fare clic su **Avanzate** per selezionare schemi specifici, applicare un filtro o escludere informazioni sulla relazione tra tabelle.  
  
     **Selezione schemi**  
  
     Per le origini dati di grandi dimensioni contenenti più schemi è possibile selezionare quali schemi utilizzare mediante un elenco delimitato da virgole, senza spazi.  
  
     **Recupera relazioni**  
  
     È possibile omettere espressamente le informazioni sulla relazione tra tabelle deselezionando la casella di controllo **Recupera relazioni** nella finestra di dialogo Opzioni avanzate vista origine dati, consentendo di creare manualmente relazioni tra tabelle in Progettazione vista origine dati.  
  
4.  **Filtrare gli oggetti disponibili**  
  
     Se l'elenco Oggetti disponibili include un numero molto elevato di oggetti, è possibile ridurlo applicando un semplice filtro che consente di specificare una stringa come criteri di selezione. Ad esempio, se si digita **dbo** e si fa clic sul pulsante **Filtro** , nell'elenco **Oggetti disponibili** verranno visualizzati soltanto gli elementi che iniziano con "dbo". Il filtro può essere una stringa parziale, ad esempio "Sal" restituisce le vendite e lo stipendio, ma non può includere più stringhe o operatori.  
  
5.  Per le origini dati relazionali che non dispongono di relazioni tra tabelle definite, viene visualizzata una pagina **Corrispondenza nomi** che consente di selezionare il metodo di corrispondenza nomi appropriato. Per altre informazioni, vedere la sezione [Impostare i criteri di corrispondenza nomi per le relazioni](#bkmk_NameMatch) di questo argomento.  
  
##  <a name="add-a-secondary-data-source"></a><a name="bkmk_secondaryDS"></a>Aggiungere un'origine dati secondaria  
 Quando si definisce una vista origine dati contenente tabelle, viste o colonne di più origini dei dati, la prima origine dei dati da cui vengono aggiunti oggetti alla vista origine dati viene designata come origine dei dati primaria. Dopo che è stata definita, l'origine dei dati primaria non può essere modificata. Dopo aver definito una vista origine dati basata su oggetti di una singola origine dei dati, è successivamente possibile aggiungere oggetti di altre origini dei dati.  
  
 Se per una query di data mining o elaborazione OLAP sono necessari dati di più origini dei dati in una singola query, l'origine dei dati primaria deve supportare query remote tramite `OpenRowset`. Si tratterà in genere di un'origine dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se ad esempio si progetta una dimensione OLAP contenente attributi associati a colonne di più origini dei dati, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verrà costruita una query `OpenRowset` per popolare la dimensione durante l'elaborazione. Non verrà invece costruita una query `OpenRowset` se è possibile popolare un oggetto OLAP o risolvere una query di data mining da una singola origine dei dati. In determinate situazioni, è possibile eliminare l'esigenza di una query `OpenRowset` definendo relazioni tra attributi. Per altre informazioni sulle relazioni tra attributi, vedere [Relazioni tra attributi](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md), [Aggiunta o rimozione di tabelle o viste in una vista origine dati &#40;Analysis Services&#41;](adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md) e [Definire relazioni tra attributi](attribute-relationships-define.md).  
  
 Per aggiungere tabelle e colonne da un'origine dati secondaria, fare doppio clic sulla vista origine dati in Esplora soluzioni per aprirla in Progettazione vista origine dati, quindi utilizzare la finestra di dialogo Aggiungi/Rimuovi tabelle per includere oggetti di altre origini dati definite nel progetto. Per altre informazioni, vedere [Aggiunta o rimozione di tabelle o viste in una vista origine dati &#40;Analysis Services&#41;](adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md).  
  
##  <a name="specify-name-matching-criteria-for-relationships"></a><a name="bkmk_NameMatch"></a>Specificare i criteri di corrispondenza nomi per le relazioni  
 Durante la creazione di una vista origine dati, le relazioni tra tabelle vengono definite in base a vincoli di chiave esterna nell'origine dati. Tali relazioni sono necessarie per consentire al motore di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di costruire le query di data mining e di elaborazione OLAP appropriate. Talvolta, tuttavia, un'origine dei dati con più tabelle non include vincoli di chiave esterna. In tal caso, nella Creazione guidata vista origine dati viene richiesto di definire i criteri di corrispondenza nomi desiderati per colonne di tabelle diverse.  
  
> [!NOTE]  
>  Verrà richiesto di specificare i criteri di corrispondenza nomi solo se non vengono rilevate relazioni di chiave esterna nell'origine dei dati sottostante. In caso contrario, le relazioni rilevate verranno utilizzate e sarà necessario definire manualmente le eventuali relazioni aggiuntive che si desidera includere nella vista origine dati, incluse le chiavi primarie logiche. Per altre informazioni, vedere [Definire relazioni logiche in una vista origine dati &#40;Analysis Services&#41;](define-logical-relationships-in-a-data-source-view-analysis-services.md) e [Definire chiavi primarie logiche in una vista origine dati &#40;Analysis Services&#41;](define-logical-primary-keys-in-a-data-source-view-analysis-services.md).  
  
 In base alla risposta specificata, la Creazione guidata vista origine dati consente di definire la corrispondenza tra i nomi di colonna e di creare relazioni tra le diverse tabelle nella vista origine dati. È possibile specificare uno dei criteri elencati nella tabella seguente.  
  
|Criteri di corrispondenza nomi|Descrizione|  
|----------------------------|-----------------|  
|**Stesso nome della chiave primaria**|Il nome della colonna chiave esterna nella tabella di origine è uguale a quello della colonna chiave primaria nella tabella di destinazione. Ad esempio, il nome della colonna chiave esterna `Order.CustomerID` è uguale a quello della colonna chiave primaria `Customer.CustomerID`.|  
|**Stesso nome della tabella di destinazione**|Il nome della colonna chiave esterna nella tabella di origine è uguale a quello della tabella di destinazione. Ad esempio, il nome della colonna chiave esterna `Order.Customer` è uguale a quello della colonna chiave primaria `Customer.CustomerID`.|  
|**Nome tabella di destinazione + nome chiave primaria**|Il nome della colonna chiave esterna nella tabella di origine è uguale a quello della tabella di destinazione concatenato al nome della colonna chiave primaria. Per differenziarli, è consentito utilizzare uno spazio o un carattere di sottolineatura. Ad esempio, tutte le coppie di chiavi esterna-primaria seguenti sono corrispondenti:<br /><br /> `Order.CustomerID` e `Customer.ID`<br /><br /> `Order.Customer ID` e `Customer.ID`<br /><br /> `Order.Customer_ID` e `Customer.ID`|  
  
 I criteri selezionati consentono di modificare l'impostazione della proprietà **NameMatchingCriteria** della vista origine dati. Tale impostazione permette di determinare il modo in cui le tabelle correlate vengono aggiunte dalla procedura guidata. Quando si modifica la vista origine dati con Progettazione vista origine dati, l'impostazione consente di determinare la corrispondenza tra colonne utilizzata nella finestra di progettazione per creare le relazioni tra tabelle nella vista origine dati. È possibile modificare l'impostazione della proprietà **NameMatchingCriteria** in Progettazione vista origine dati. Per altre informazioni, vedere [Modificare le proprietà in una vista origine dati &#40;Analysis Services&#41;](change-properties-in-a-data-source-view-analysis-services.md).  
  
> [!NOTE]  
>  Al termine della Creazione guidata vista origine dati, è possibile aggiungere o rimuovere le relazioni nel riquadro degli schemi di Progettazione vista origine dati. Per altre informazioni, vedere [Definire relazioni logiche in una vista origine dati &#40;Analysis Services&#41;](define-logical-relationships-in-a-data-source-view-analysis-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiunta o rimozione di tabelle o viste in una vista origine dati &#40;Analysis Services&#41;](adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)   
 [Definire chiavi primarie logiche in una vista origine dati &#40;Analysis Services&#41;](define-logical-primary-keys-in-a-data-source-view-analysis-services.md)   
 [Definire calcoli denominati in una vista origine dati &#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [Definire query denominate in una vista origine dati &#40;Analysis Services&#41;](define-named-queries-in-a-data-source-view-analysis-services.md)   
 [Sostituire una tabella o una query denominata in una vista origine dati &#40;Analysis Services&#41;](replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services.md)   
 [Utilizzare diagrammi in Progettazione vista origine dati &#40;Analysis Services&#41;](work-with-diagrams-in-data-source-view-designer-analysis-services.md)   
 [Esplorazione dei dati in una vista origine dati &#40;Analysis Services&#41;](explore-data-in-a-data-source-view-analysis-services.md)   
 [Eliminare una vista origine dati &#40;Analysis Services&#41;](delete-a-data-source-view-analysis-services.md)   
 [Aggiornare lo schema in una vista origine dati &#40;Analysis Services&#41;](refresh-the-schema-in-a-data-source-view-analysis-services.md)  
  
  
