---
title: Strumenti di Data Mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tools [Analysis Services]
- mining models [Analysis Services], tools
- data mining [Analysis Services], tools
- data mining [Analysis Services], development
ms.assetid: 003ada6a-0bcd-4f16-8c34-1a9ffc75cd2c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dd0e6b696e692a9e88edd234d22f41983acbe961
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084830"
---
# <a name="data-mining-tools"></a>Strumenti di data mining
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] offre gli strumenti seguenti che consentono di creare soluzioni di data mining:  
  
-   La **Creazione guidata modello di data mining** di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] consente di semplificare la creazione di strutture e modelli di data mining, usando origini dati relazionali o dati multidimensionali in cubi.  
  
     Nella procedura guidata è possibile scegliere i dati da utilizzare e applicare tecniche specifiche di data mining, ad esempio clustering, reti neurali o modellizzazione della serie temporale.  
  
-   I**visualizzatori dei modelli** sono disponibili sia in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] che in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]per l'esplorazione dei modelli di data mining al termine della relativa creazione.  È possibile esplorare modelli utilizzando visualizzatori personalizzati per ogni algoritmo o eseguire un'analisi più approfondita tramite il visualizzatore di contenuto del modello.  
  
-   Il **generatore delle query di stima** viene fornito sia in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] che in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per consentire la creazione di query di stima. È possibile testare inoltre l'accuratezza di modelli rispetto a un set di dati di controllo o dati esterni o utilizzare la convalida incrociata per valutare la qualità del set di dati.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è l'interfaccia in cui è possibile gestire soluzioni di data mining esistenti distribuite in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. È possibile rielaborare strutture e modelli per aggiornare i dati in essi contenuti.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contiene strumenti che è possibile usare per pulire dati, automatizzare attività quali la creazione di stime e l'aggiornamento di modelli, nonché per creare soluzioni di text mining.  
  
 Nelle sezioni seguenti sono disponibili ulteriori informazioni sugli strumenti di data mining inclusi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="data-mining-wizard"></a>Creazione guidata modello di data mining  
 Utilizzare la Creazione guidata modello di data mining per iniziare la creazione di soluzioni di data mining. Questa procedura guidata è rapida e facile, consente di eseguire in modo semplificato il processo di creazione di una struttura di data mining e di un modello iniziale correlato e dispone di attività quali la selezione di un tipo di algoritmo e di un'origine dati e la definizione dei dati del case utilizzati per l'analisi.  
  
 **Per altre informazioni:** [Creazione guidata modello di data mining &#40;Analysis Services - Data mining&#41;](data-mining-wizard-analysis-services-data-mining.md)  
  
## <a name="data-mining-designer"></a>Data Mining Designer  
 Dopo aver creato una struttura e un modello di data mining tramite la Creazione guidata modello di data mining, è possibile utilizzare Progettazione modelli di data mining da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per utilizzare modelli e strutture esistenti.  
  
 Nella finestra di progettazione sono inclusi strumenti per le attività seguenti:  
  
-   Modifica delle proprietà di strutture di data mining, aggiunta di colonne e creazione di alias di colonna, modifica del metodo binning o della distribuzione prevista di valori.  
  
-   Aggiunta di nuovi modelli a una struttura esistente, copia di modelli, modifica di metadati o di proprietà del modello o definizione dei filtri in un modello di data mining.  
  
-   Esplorazione degli schemi e delle regole all'interno del modello, nonché esplorazione di associazioni o di alberi delle decisioni. Acquisizione di statistiche dettagliate sui  
  
     visualizzatori personalizzati forniti per ogni tipo diverso di modello, per consentire l'analisi dei dati e l'esplorazione dei modelli rivelati dal data mining.  
  
-   Convalida dei modelli creando grafici di accuratezza o analizzando la curva dei profitti per i modelli. Confronto dei modelli utilizzando matrici di classificazione o convalida di un set di dati e dei relativi modelli tramite la convalida incrociata.  
  
-   Creazione di query sul contenuto e di stima sui modelli di data mining esistenti. Compilazione di query uniche o configurazione di query per generare stime per intere tabelle di dati esterni.  
  
 **Per altre informazioni:** [Progettazione modelli di data mining](data-mining-designer.md)  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Al termine della creazione e distribuzione di modelli di data mining in un server, è possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per gestire il database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui sono ospitati gli oggetti di data mining. È possibile continuare inoltre a eseguire attività in cui viene utilizzato il modello, ad esempio l'esplorazione dei modelli, l'elaborazione di nuovi dati e la creazione di stime.  
  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] contiene inoltre editor di query che è possibile usare per progettare ed eseguire query DMX (Data Mining Extensions) o per utilizzare oggetti di data mining tramite XMLA.  
  
## <a name="integration-services-data-mining-tasks-and-transformations"></a>Attività di data mining e trasformazioni in Integration Services  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dispone di numerosi componenti che supportano il data mining.  
  
 Alcuni strumenti in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono progettati per consentire di automatizzare attività di data mining comuni, tra cui stime, compilazioni di modelli ed elaborazioni. Ad esempio:   
  
-   Creare un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che consenta di aggiornare automaticamente il modello ogni volta che il set di dati viene aggiornato con nuovi clienti.  
  
-   Eseguire segmentazioni o campionamenti personalizzati di record del case.  
  
-   Generare automaticamente modelli passati sui parametri.  
  
 Tuttavia, è possibile utilizzare il data mining anche in un flusso di lavoro del pacchetto, come input ad altri processi. Ad esempio:   
  
-   Utilizzare i valori delle probabilità generati dal modello per ponderare i punteggi per il text mining o per altre attività di classificazione.  
  
-   Generare automaticamente stime in base ai dati precedenti e utilizzare tali valori per valutare la validità dei nuovi dati.  
  
-   Utilizzare la regressione logistica per segmentare potenziali clienti in base ai rischi.  
  
 **Per altre informazioni:** [Progetti correlati per soluzioni di data mining](data-mining-solutions.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Attività e procedure relative al modello di data mining](mining-model-tasks-and-how-tos.md)   
 [Attività e procedure relative al visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md)   
 [Soluzioni di data mining](data-mining-solutions.md)  
  
  
