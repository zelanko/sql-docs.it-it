---
title: Annotazioni CSDL per Business Intelligence (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: bf6f372a-bc67-45ea-a771-b2dc5b0527e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 22ca1fe2ace8ef3b04adaf8323e0edaac2a07af6
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246780"
---
# <a name="csdl-annotations-for-business-intelligence-csdlbi"></a>Annotazioni CSDL per Business Intelligence (CSDLBI)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta la presentazione della definizione di un modello tabulare in un formato XML denominato Conceptual Schema Definition Language con annotazioni Business Intelligence (CSDLBI).  
  
 In questo argomento viene fornita una panoramica di CSDLBI e viene descritto come utilizzarlo con i modelli di dati [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="understanding-the-role-of-csdl"></a>Informazioni sul ruolo del linguaggio CSDL  
 Conceptual Schema Data Language (CSDL) è un linguaggio basato su XML tramite cui vengono descritte entità, relazioni e funzioni. CSDL è definito come parte di Entity Data Framework. Le annotazioni di Business Intelligence sono un'estensione progettata per supportare la modellazione dati utilizzando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Anche se CSDL è conforme a Entity Data Framework, non è necessario conoscere il modello entità-relazione o disporre di strumenti speciali per compilare un modello tabulare o un report basato su un modello. I modelli vengono compilati tramite strumenti client quali [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o un'API, ad esempio AMO, quindi vengono distribuiti a un server. I client si connettono al modello tramite un file di definizione del modello, di solito pubblicato in una raccolta di SharePoint dove può essere utilizzato da progettisti e utenti di report. Per ulteriori informazioni, vedere i collegamenti seguenti:  
  
-   [Soluzioni di modelli tabulari &#40;SSAS tabulare&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
-   [Distribuzione di una soluzione del modello tabulare &#40;SSAS tabulare&#41;](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
-   [Connessione BI Semantic Model di PowerPivot &#40;con estensione bism&#41;](../power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)  
  
 Lo schema CSDLBI è generato dal server Analysis Services in risposta a una richiesta di una definizione del modello da un client, ad esempio [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. L'applicazione client invia una query XML al server Analysis Services che ospita i dati del modello. In risposta, il server invia un messaggio XML che contiene una definizione delle entità nel modello,utilizzando le annotazioni CSDLBI. Il client di creazione report quindi utilizza le informazioni per presentare i campi, le aggregazioni e le misure disponibili nel modello. Le annotazioni CSDLBI forniscono inoltre informazioni sul raggruppamento, l'ordinamento e la formattazione dei dati.  
  
 Per informazioni generali su CSDLBI, vedere [concetti di CSDLBI](https://docs.microsoft.com/bi-reference/csdl/csdlbi-concepts).  
  
### <a name="working-with-csdl"></a>Utilizzo di CSDL  
 Il set di annotazioni CSDLBI che rappresenta un qualsiasi modello tabulare particolare è un documento XML contenente una raccolta di entità semplici e complesse. Le entità definiscono tabelle (o dimensioni), colonne (attributi), associazioni (relazioni) e formule incluse in colonne calcolate, misure o indicatori KPI.  
  
 Non è possibile modificare questi oggetti direttamente, ma è necessario utilizzare gli strumenti client e le API disponibili per l'utilizzo dei modelli tabulari.  
  
 È possibile ottenere il linguaggio CSDL per un modello inviando una richiesta DISCOVER al server in cui è ospitato il modello. La richiesta deve essere qualificata specificando il server e il modello e, facoltativamente, una vista o una prospettiva. Il messaggio restituito è una stringa XML. Determinati elementi dipendono dal linguaggio e possono restituire valori diversi a seconda del linguaggio della connessione corrente. Per altre informazioni, vedere [set di righe DISCOVER_CSDL_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset).  
  
### <a name="csdlbi-versions"></a>Versioni di CSDLBI  
 La specifica CSDL originale di Entity Data Framework fornisce la maggior parte delle entità e proprietà necessarie per supportare la modellazione. Le annotazioni Business Intelligence supportano i requisiti speciali dei modelli tabulari, le proprietà della creazione report necessarie per i client quali [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] e metadati aggiuntivi richiesti per i modelli multidimensionali. In questa sezione vengono descritti gli aggiornamenti di ogni versione.  
  
 **CSDLBI 1.0**  
  
 Il set iniziale di aggiunte allo schema CSDL che consente di utilizzare i modelli tabulari di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contiene le annotazioni a supporto della modellazione dati, dei calcoli personalizzati e della presentazione avanzata:  
  
-   Nuovi elementi e proprietà per supportare i modelli tabulari. Ad esempio, è stata aggiunta una proprietà per specificare il tipo di query database utilizzato per popolare il modello.  
  
-   Nuove proprietà e nuove estensioni alle entità esistenti.  Ad esempio, l'elemento Association è stato esteso per supportare le relazioni.  
  
-   Proprietà di visualizzazione e navigazione. Ad esempio, sono state aggiunte le proprietà per supportare l'ordinamento personalizzato dei campi, delle immagini predefinite e  
  
 **CSDLBI 1.1**  
  
 Questa versione dello schema CSDLBI include le aggiunte a supporto dei database multidimensionali, ad esempio i cubi OLAP. Di seguito sono riportati i nuovi elementi e le nuove proprietà:  
  
-   Supporto per le dimensioni come entità.  
  
-   Supporto per le gerarchie.  
  
-   Esposizione delle partizioni ROLAP.  
  
-   Supporto per le traduzioni.  
  
-   Supporto per le prospettive.  
  
 Per informazioni dettagliate sui singoli elementi delle annotazioni CSDLBI, vedere [Technical Reference for annotazioni Business Intelligence per CSDL](https://docs.microsoft.com/bi-reference/csdl/technical-reference-for-bi-annotations-to-csdl). Per informazioni sulla specifica CSDL di base, vedere la [specifica CSDL v3](https://docs.microsoft.com/ef/ef6/modeling/designer/advanced/edmx/csdl-spec).  
  
  
## <a name="see-also"></a>Vedere anche  
 [Comprendere il modello a oggetti tabulare](representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Concetti di CSDLBI](https://docs.microsoft.com/bi-reference/csdl/csdlbi-concepts)   
 [Informazioni sul modello a oggetti tabulare](representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
