---
title: Query di definizione dei dati (data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 49e02de1-4ffa-401c-8eee-471a9c25b86a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a67cadab4ee67bb3f81776ccb658c66fe6a67d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085154"
---
# <a name="data-definition-queries-data-mining"></a>Query di definizione dei dati (Data mining)
  Per il data mining, la *query di definizione dei dati* della categoria indica le istruzioni DMX o i comandi XMLA usati per eseguire le operazioni seguenti:  
  
-   Creare o modificare oggetti di data mining, ad esempio un modello.  
  
-   Definire l'origine dei dati da utilizzare per il training o per la stima.  
  
-   Esportare o importare modelli e strutture di data mining  
  
 [Creazione di query di definizione dei dati](#bkmk_Create)  
  
-   [Query di definizione dei dati in SQL Server Data Tools](#bkmk_ssdt)  
  
-   [Query di definizione dei dati in SQL Server Management Studio](#bkmk_SSMS)  
  
 [Scripting di istruzioni di definizione dei dati](#bkmk_Scripts)  
  
 [Scripting di istruzioni di definizione dei dati](#bkmk_Export)  
  
##  <a name="bkmk_Create"></a>Creazione di query di definizione dei dati  
 È possibile creare query di definizione dei dati (istruzioni) usando il generatore delle query di stima in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]o tramite la finestra Query DMX in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Le istruzioni DMX per la definizione dei dati fanno parte del linguaggio DDL (Data Definition Language) di Analysis Services.  
  
 Per informazioni sulla sintassi di istruzioni per la definizione dei dati specifiche, vedere [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-reference).  
  
###  <a name="bkmk_ssdt"></a>Query di definizione dei dati in SQL Server Data Tools  
 Creazione guidata modello di data mining è lo strumento preferito in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per la creazione e la modifica di modelli e strutture di data mining, nonché per la definizione delle origini dati utilizzate nelle query di stima e per il training.  
  
 Tuttavia, se si desidera conoscere quali istruzioni vengono inviate al server dalla procedura guidata per creare strutture di dati o modelli di data mining, è possibile utilizzare SQL Server Profiler per acquisire le istruzioni per la definizione dei dati. Per altre informazioni, vedere [Utilizzare SQL Server Profiler per il monitoraggio di Analysis Services](../instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 Per visualizzare le istruzioni usate per la definizione delle origini dati per il training o la stima, è possibile usare la **Visualizzazione SQL** nel generatore delle query di stima. Talvolta, può essere utile per compilare query di base per il training e il testing di modelli utilizzando il generatore delle query di stima, per stabilire la sintassi corretta. È possibile passare quindi alla **Visualizzazione SQL** e modificare manualmente la query. Per altre informazioni, vedere [Modificare manualmente un query di stima](manually-edit-a-prediction-query.md).  
  
###  <a name="bkmk_SSMS"></a>Query di definizione dei dati in SQL Server Management Studio  
 Per oggetti di data mining, è possibile utilizzare le query di definizione dei dati per effettuare le azioni seguenti:  
  
-   Creare tipi di modelli specifici, ad esempio un modello di clustering o di albero delle decisioni, tramite [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx).  
  
-   Modificare una struttura di data mining esistente aggiungendo un modello o modificando le colonne tramite [ALTER MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx). Si noti che non è possibile modificare un modello di data mining tramite DMX. Vengono aggiunti solo nuovi modelli a una struttura esistente.  
  
-   Effettuare una copia di un modello di data mining e quindi modificarla tramite [SELECT INTO &#40;DMX&#41;](/sql/dmx/select-into-dmx).  
  
-   Definire il set di dati usato per il training di un modello tramite [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx), insieme a una query di origine dati quale OPENROWSET.  
  
 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] offre modelli di query utili per la creazione di query di definizione dei dati. Per altre informazioni, vedere [Utilizzare i modelli di Analysis Services in SQL Server Management Studio](../instances/use-analysis-services-templates-in-sql-server-management-studio.md).  
  
 In generale, nei modelli forniti per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è contenuta solo la definizione della sintassi generale, che è necessario personalizzare digitando nella finestra **Query** o tramite la finestra di dialogo fornita per l'immissione di parametri.  
  
 Per un esempio di come immettere i parametri tramite l'interfaccia, vedere [Creare una query di stima singleton da un modello](create-a-singleton-prediction-query-from-a-template.md).  
  
###  <a name="bkmk_Scripts"></a>Scripting di istruzioni di definizione dei dati  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornisce più linguaggi di script e di programmazione che è possibile usare per creare o modificare oggetti di data mining o per definire le origini dati.  Anche se DMX è progettato per facilitare le attività di data mining, è possibile utilizzare inoltre sia XMLA sia AMO per modificare oggetti negli script o in codice personalizzato.  
  
 Nel componente aggiuntivo Data mining per Excel sono inclusi anche molti modelli di query, oltre all' **Editor avanzato query**che consente di comporre istruzioni DMX complesse. È possibile compilare una query in modo interattivo e passare a Visualizzazione SQL per acquisire l'istruzione DMX.  
  
##  <a name="bkmk_Export"></a>Esportazione e importazione di modelli  
 È possibile utilizzare le istruzioni per la definizione dei dati in DMX per esportare la definizione di un modello e le relative origini dati e struttura necessarie, e importare quindi tale definizione in un server diverso. L'utilizzo dell'esportazione e dell'importazione è il modo più veloce per spostare modelli e strutture di data mining tra istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per ulteriori informazioni, vedere [gestione di soluzioni e oggetti di data mining](management-of-data-mining-solutions-and-objects.md).  
  
> [!WARNING]  
>  Se il modello è basato sui dati provenienti dall'origine dati di un cubo, non è possibile utilizzare DMX per esportare il modello, è necessario utilizzare invece la funzionalità di backup e ripristino.  
  
##  <a name="bkmk_Tasks"></a> Attività correlate  
 Nella tabella seguente vengono forniti i collegamenti alle attività correlate alle query di definizione dei dati.  
  
|||  
|-|-|  
|Utilizzo di modelli per query DMX.|[Usare i modelli di Analysis Services in SQL Server Management Studio](../instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|Progettazione di query di tutti i tipi tramite il generatore delle query di stima.|[Creare una query di stima utilizzando Generatore query di stima](create-a-prediction-query-using-the-prediction-query-builder.md)|  
|Acquisizione delle definizioni di query tramite SQL Server Profiler e utilizzo delle tracce per monitorare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|[Usare SQL Server Profiler per il monitoraggio di Analysis Services](../instances/use-sql-server-profiler-to-monitor-analysis-services.md)|  
|Informazioni sui linguaggi di scripting e di programmazione forniti per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|[XML for Analysis &#40;riferimento&#41; XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)<br /><br /> [Sviluppo con Analysis Management Objects &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)|  
|Informazioni sulla gestione di modelli in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|[Esportare e importare gli oggetti di data mining](export-and-import-data-mining-objects.md)<br /><br /> [ESPORTA &#40;DMX&#41;](/sql/dmx/export-dmx)<br /><br /> [IMPORTA &#40;DMX&#41;](/sql/dmx/import-dmx)|  
|Informazioni su OPENROWSET e su altre modalità per eseguire una query sui dati esterni.|[&#60;&#62;di query sui dati di origine ](/sql/dmx/source-data-query).|  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione guidata modello di data mining &#40;Analysis Services-&#41;di data mining](data-mining-wizard-analysis-services-data-mining.md)  
  
  
