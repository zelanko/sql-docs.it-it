---
title: Tabelle e colonne del modello tabulare di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7a9844032ad24de1c81144ca742bfb185aecc36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207487"
---
# <a name="tables-and-columns"></a>Tabelle e colonne 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Dopo aver aggiunto tabelle e dati in un modello tramite l'Importazione guidata tabella, è possibile iniziare a utilizzare le tabella aggiungendo nuove colonne di dati, creando relazioni tra tabelle, definendo calcoli che consentono di estendere i dati, nonché filtrando e ordinando i dati nelle tabelle per una visualizzazione più semplice.  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#bkmk_benefits)  
  
-   [Utilizzo di tabelle e colonne](#bkmk_working)  
  
-   [Attività correlate](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> Vantaggi  
 Nei modelli tabulari, le tabelle garantiscono il framework con cui vengono definiti le colonne e altri metadati. Nelle tabelle sono inclusi gli elementi seguenti:  
  
 **Definizione della tabella**  
 Nella definizione della tabella è incluso il set di colonne. Le colonne possono essere importate da un'origine dati o aggiunte manualmente, ad esempio con le colonne calcolate.  
  
 **Metadati della tabella**  
 Relazioni, misure, ruoli, prospettive e dati incollati sono tutti metadati che consentono di definire gli oggetti all'interno del contesto di una tabella.  
  
 **Dati**  
 I dati vengono popolati nelle colonne delle tabelle alla prima importazione delle tabelle tramite l'Importazione guidata tabella o la creazione di nuovi dati nelle colonne calcolate. Quando i dati vengono modificati all'origine oppure quando un modello viene rimosso dalla memoria, è necessario eseguire un'operazione di elaborazione per popolare nuovamente i dati nelle tabelle.  
  
##  <a name="bkmk_working"></a> Utilizzo di tabelle e colonne  
 In Progettazione modelli non vengono create direttamente nuove tabelle del modello. Viene creata automaticamente una nuova scheda ogni volta che si importano o copiano dati da un'altra origine. In ciascuna scheda di Progettazione modelli è contenuta una tabella di dati in cui possono essere inclusi gli elementi seguenti:  
  
-   Una singola tabella o vista di un database relazionale o di altre origini non relazionali, ad esempio un cubo di Analysis Services.  
  
-   Un set di dati tabulare importato da un feed o da un file di testo.  
  
-   Una combinazione di dati relazionali e tabulari (HTML) copiati e incollati nella tabella.  
  
 Quando si importano dati, ogni tabella o vista, foglio o file di dati viene aggiunto come tabella in Progettazione modelli. Di solito, vengono aggiunti dati di varie origini in schede separate, tuttavia è possibile unire dati in un'unica tabella usando le opzioni **Incolla** e **Accoda il contenuto degli Appunti**. Per altre informazioni, vedere [copiare e incollare dati](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md).  
  
 Dopo aver aggiunto i dati necessari, è possibile creare ulteriori relazioni tra le tabelle, ricercare o fare riferimento a valori correlati in altre tabelle oppure creare valori derivati aggiungendo nuove colonne calcolate.  
  
 Se si utilizzano set di dati molto grandi, potrebbe essere necessario filtrare alcuni dati affinché non siano visibili. Potrebbe anche essere necessario ordinare i dati in modo diverso. Tramite Progettazione modelli, è possibile utilizzare le funzionalità che consentono di filtrare, ordinare e nascondere al fine di visualizzare o meno colonne intere o determinati dati.  
  
##  <a name="bkmk_related_tasks"></a> Attività correlate  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Aggiungere colonne a una tabella](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)|Viene descritto come aggiungere una colonna di origine a una definizione della tabella.|  
|[Eliminare una colonna](../../analysis-services/tabular-models/delete-a-column-ssas-tabular.md)|Viene descritto come eliminare una colonna di tabella di un modello utilizzando Progettazione modelli o la finestra di dialogo Proprietà tabella.|  
|[Modificare i mapping di filtri tabella, colonna o riga](../../analysis-services/tabular-models/change-table-column-or-row-filter-mappings-ssas-tabular.md)|Viene descritto come modificare i mapping di filtri tabella, colonna o riga tramite l'anteprima della tabella o l'editor di query SQL nella finestra di dialogo Modifica proprietà tabella.|  
|[Specificare Contrassegna come tabella data per l'uso con funzionalità di Business Intelligence per le gerarchie temporali](../../analysis-services/tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md)|Viene descritto come utilizzare la finestra di dialogo Contrassegna come tabella data per specificare una tabella relativa alla data e una colonna dell'identificatore univoco. La specifica di una tabella relativa alla data e l'identificatore univoco è necessaria quando si utilizzano le funzioni di Business Intelligence per la gerarchia temporale nelle formule DAX.|  
|[Aggiungere una tabella](../../analysis-services/tabular-models/add-a-table-ssas-tabular.md)|Viene descritto come aggiungere una tabella da un'origine dati tramite una connessione all'origine dati esistente.|  
|[Eliminare una tabella](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)|Viene descritto come eliminare le tabelle non più necessarie nel database dell'area di lavoro modello.|  
|[Rinominare una tabella o una colonna](../../analysis-services/tabular-models/rename-a-table-or-column-ssas-tabular.md)|Viene descritto come rinominare una tabella o una colonna per renderla più identificabile nel modello.|  
|[Impostare il tipo di dati di una colonna](../../analysis-services/tabular-models/set-the-data-type-of-a-column-ssas-tabular.md)|Viene descritto come modificare il tipo di dati di una colonna. Il tipo di dati consente di definire la modalità di archiviazione e presentazione dei dati della colonna.|  
|[Nascondere o bloccare colonne](../../analysis-services/tabular-models/hide-or-freeze-columns-ssas-tabular.md)|Viene descritto come nascondere le colonne che non si desidera visualizzare e come mantenere visibile un'area di un modello durante lo scorrimento a un'altra area del modello bloccando colonne specifiche (blocco) in un'area.|  
|[Colonne calcolate](../../analysis-services/tabular-models/ssas-calculated-columns.md)|Negli argomenti di questa sezione viene descritto come utilizzare le colonne calcolate per aggiungere dati aggregati al modello.|  
|[Filtrare e ordinare dati](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)|Negli argomenti di questa sezione viene descritto come filtrare oppure ordinare i dati utilizzando i controlli disponibili in Progettazione modelli.|  
  
  
