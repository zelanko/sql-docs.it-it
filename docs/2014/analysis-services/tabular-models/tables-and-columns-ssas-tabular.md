---
title: Tabelle e colonne (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c428d717-05de-436c-b9dc-e8c1925a60ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4dcab58a876881cc9ca76e9159d5bcc68ffd5fdb
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66066506"
---
# <a name="tables-and-columns-ssas-tabular"></a>Tabelle e colonne (SSAS tabulare)
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
  
 Quando si importano dati, ogni tabella o vista, foglio o file di dati viene aggiunto come tabella in Progettazione modelli. Di solito, vengono aggiunti dati di varie origini in schede separate, tuttavia è possibile unire dati in un'unica tabella usando le opzioni **Incolla** e **Accoda il contenuto degli Appunti**. Per altre informazioni, vedere [Copiare e incollare dati &#40;SSAS tabulare&#41;](../copy-and-paste-data-ssas-tabular.md).  
  
 Dopo aver aggiunto i dati necessari, è possibile creare ulteriori relazioni tra le tabelle, ricercare o fare riferimento a valori correlati in altre tabelle oppure creare valori derivati aggiungendo nuove colonne calcolate.  
  
 Se si utilizzano set di dati molto grandi, potrebbe essere necessario filtrare alcuni dati affinché non siano visibili. Potrebbe anche essere necessario ordinare i dati in modo diverso. Tramite Progettazione modelli, è possibile utilizzare le funzionalità che consentono di filtrare, ordinare e nascondere al fine di visualizzare o meno colonne intere o determinati dati.  
  
##  <a name="bkmk_related_tasks"></a> Attività correlate  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Aggiungere colonne a una tabella &#40;SSAS tabulare&#41;](add-columns-to-a-table-ssas-tabular.md)|Viene descritto come aggiungere una colonna di origine a una definizione della tabella.|  
|[Eliminare una colonna &#40;SSAS tabulare&#41;](delete-a-column-ssas-tabular.md)|Viene descritto come eliminare una colonna di tabella di un modello utilizzando Progettazione modelli o la finestra di dialogo Proprietà tabella.|  
|[Modificare i mapping di filtri tabella, colonna o riga &#40;SSAS tabulare&#41;](change-table-column-or-row-filter-mappings-ssas-tabular.md)|Viene descritto come modificare i mapping di filtri tabella, colonna o riga tramite l'anteprima della tabella o l'editor di query SQL nella finestra di dialogo Modifica proprietà tabella.|  
|[Specificare Contrassegna come tabella data per l'utilizzo con funzionalità di Business Intelligence per le gerarchie temporali &#40;SSAS tabulare&#41;](specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md)|Viene descritto come utilizzare la finestra di dialogo Contrassegna come tabella data per specificare una tabella relativa alla data e una colonna dell'identificatore univoco. La specifica di una tabella relativa alla data e l'identificatore univoco è necessaria quando si utilizzano le funzioni di Business Intelligence per la gerarchia temporale nelle formule DAX.|  
|[Aggiungere una tabella &#40;SSAS tabulare&#41;](add-a-table-ssas-tabular.md)|Viene descritto come aggiungere una tabella da un'origine dati tramite una connessione all'origine dati esistente.|  
|[Eliminare una tabella &#40;SSAS tabulare&#41;](delete-a-table-ssas-tabular.md)|Viene descritto come eliminare le tabelle non più necessarie nel database dell'area di lavoro modello.|  
|[Rinominare una tabella o una colonna &#40;SSAS tabulare&#41;](rename-a-table-or-column-ssas-tabular.md)|Viene descritto come rinominare una tabella o una colonna per renderla più identificabile nel modello.|  
|[Impostare il tipo di dati di una colonna &#40;SSAS tabulare&#41;](set-the-data-type-of-a-column-ssas-tabular.md)|Viene descritto come modificare il tipo di dati di una colonna. Il tipo di dati consente di definire la modalità di archiviazione e presentazione dei dati della colonna.|  
|[Nascondere o bloccare colonne &#40;SSAS tabulare&#41;](hide-or-freeze-columns-ssas-tabular.md)|Viene descritto come nascondere le colonne che non si desidera visualizzare e come mantenere visibile un'area di un modello durante lo scorrimento a un'altra area del modello bloccando colonne specifiche (blocco) in un'area.|  
|[Colonne calcolate &#40;SSAS tabulare&#41;](ssas-calculated-columns.md)|Negli argomenti di questa sezione viene descritto come utilizzare le colonne calcolate per aggiungere dati aggregati al modello.|  
|[Filtrare e ordinare dati &#40;SSAS tabulare&#41;](../filter-and-sort-data-ssas-tabular.md)|Negli argomenti di questa sezione viene descritto come filtrare oppure ordinare i dati utilizzando i controlli disponibili in Progettazione modelli.|  
  
  
