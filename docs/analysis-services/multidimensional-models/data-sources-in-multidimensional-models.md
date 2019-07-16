---
title: Origini dati nei modelli multidimensionali | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 149ac1e36eb07d40223ffc97fba1646932ab0093
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178947"
---
# <a name="data-sources-in-multidimensional-models"></a>Origini dati nei modelli multidimensionali
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Tutti i dati importati o caricati in un modello multidimensionale provengono da un'origine dati esterna. In genere i dati di origine provengono da un data warehouse progettato per la creazione di report, ma potrebbero provenire da qualsiasi database relazionale a cui è stato effettuato l'accesso in modo diretto o indiretto tramite un intermediario, ad esempio un pacchetto [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Un oggetto **origine dati** in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente di specificare una connessione diretta a un'origine dati esterna. Oltre alla posizione fisica, un oggetto origine dati consente di specificare la stringa di connessione, il provider di dati, le credenziali e altre proprietà utilizzate per controllare il comportamento di connessione.  
  
 Le informazioni fornite dall'oggetto origine dati vengono utilizzate durante le operazioni seguenti:  
  
-   Ottenere informazioni sullo schema e altri metadati utilizzati per generare viste origine dati in un modello.  
  
-   Eseguire una query e caricare i dati in un modello durante l'elaborazione.  
  
-   Eseguire query su modelli multidimensionali o di data mining in cui si utilizza la modalità di archiviazione ROLAP.  
  
-   Leggere o scrivere in partizioni remote.  
  
-   Connettersi a oggetti collegati ed eseguire la sincronizzazione da una destinazione a un'origine.  
  
-   Eseguire operazioni di writeback per l'aggiornamento di dati della tabella dei fatti archiviati in un database relazionale.  
  
 Quando si compila un modello multidimensionale a partire dal basso, si inizia creando l'oggetto origine dati che viene quindi usato per generare l'oggetto successivo, una **vista origine dati**. Una vista origine dati rappresenta il livello di astrazione dati nel modello. Viene in genere creata dopo l'oggetto origine dati, utilizzando come base quello del database di origine. Tuttavia, si possono scegliere altri modi per compilare un modello, tra cui iniziare con cubi e dimensioni per poi generare lo schema che meglio supporta la progettazione.  
  
 Indipendentemente dalla modalità di compilazione, ogni modello richiede almeno un oggetto origine dati con cui è possibile specificare una connessione all'origine dati. È possibile creare più oggetti origine dati in un solo modello per utilizzare dati provenienti da origini diverse o diverse proprietà di connessione per oggetti specifici.  
  
 Gli oggetti origine dati possono essere gestiti in modo indipendente da altri oggetti nel modello. Dopo aver creato un'origine dati, è possibile modificarne le proprietà in seguito, quindi pre-elaborare il modello per assicurarsi che i dati vengano correttamente recuperati.  
  
## <a name="related-topics-and-tasks"></a>Attività e argomenti correlati  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Origini dati supportate &#40;SSAS - multidimensionale&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)|Vengono descritti i tipi di origini dati che possono essere utilizzati in un modello multidimensionale.|  
|[Creare un'origine dati &#40;SSAS multidimensionale&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)|Viene illustrato come aggiungere un oggetto origine dati a un modello multidimensionale.|  
|[Eliminare un'origine dati in Esplora soluzioni &#40;SSAS multidimensionale&#41;](../../analysis-services/multidimensional-models/delete-a-data-source-in-solution-explorer-ssas-multidimensional.md)|Utilizzare questa procedura per eliminare un oggetto origine dati da un modello multidimensionale.|  
|[Impostare le proprietà dell'origine dati &#40;SSAS multidimensionale&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)|Viene descritta ogni proprietà e fornite informazioni su come impostarle.|  
|[Impostare opzioni di rappresentazione &#40;SSAS multidimensionale&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)|Viene descritto come configurare le opzioni nella finestra di dialogo Impostazioni di rappresentazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetti di database &#40;Analysis Services - Dati multidimensionali&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Architettura logica &#40;Analysis Services - Dati multidimensionali&#41;](../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Viste origine dati in modelli multidimensionali](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Origini dati e associazioni &#40;SSAS multidimensionale&#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
