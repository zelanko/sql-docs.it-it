---
title: Trasferimento di oggetti di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], models
- data mining editor [Analysis Services]
- mining models [Analysis Services], managing
- Data Mining Designer
- mining models [Analysis Services], modifying
ms.assetid: bc108407-2603-4387-b930-b5bb9df78069
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2b10be3a79487376b173eab87059404b7f7a618e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84521047"
---
# <a name="moving-data-mining-objects"></a>Spostamento di oggetti di data mining
  Gli scenari più comuni per lo spostamento di oggetti di data mining sono la distribuzione di un modello da un ambiente di test o analisi a un ambiente di produzione o la condivisione di modelli con altri utenti.  
  
 Questo argomento descrive come usare gli strumenti e i linguaggi di scripting forniti da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], per lo spostamento di oggetti di data mining.  
  
## <a name="moving-data-mining-objects-between-databases-or-servers"></a>Spostamento di oggetti di data mining tra database o server  
 È possibile spostare oggetti di data mining tra database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o tra istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nei modi seguenti:  
  
-   Ridistribuzione della soluzione in un altro database.  
  
-   Generazione di script di oggetti singoli.  
  
-   Backup e ripristino di una copia del database.  
  
-   Esportazione e importazione di strutture e modelli.  
  
 Nella sezione seguente queste opzioni vengono descritte in modo più dettagliato.  
  
### <a name="deploying"></a>Distribuzione  
 La distribuzione della soluzione in un server o un database diverso richiede che sia disponibile il file della soluzione creato tramite [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Per altre informazioni sulla distribuzione di Analysis Services, vedere [Distribuire progetti di Analysis Services &#40;SSDT&#41;](../multidimensional-models/deploy-analysis-services-projects-ssdt.md).  
  
### <a name="scripting"></a>Scripting  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono disponibili diversi linguaggi che è possibile usare per generare script di oggetti.  
  
-   **XMLA**: è possibile generare script di oggetti usando XMLA facendo clic con il pulsante destro del mouse sugli oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per eseguire lo script, aprirlo in una finestra **Query XMLA** nel server di destinazione.  
  
-   **DMX**: è possibile creare script tramite modelli o uno dei generatori di query forniti in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Si noti, tuttavia, che sono presenti differenze nelle attività che è possibile eseguire con ogni linguaggio di scripting:  
  
-   Alcune proprietà, quali la descrizione dell'oggetto e le associazioni dati, possono essere create o modificate solo tramite i linguaggi DDL di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , non tramite DMX.  
  
-   Solo DMX supporta l'importazione e l'esportazione di oggetti di data mining.  
  
-   Solo DMX supporta la generazione di PMML o l'importazione di definizioni di modello da PMML.  
  
-   Solo DMX supporta il training di un modello con i dati dell'applicazione. Inoltre, l'istruzione DMX INSERT INTO supporta il training di un modello senza fornire valori per una colonna chiave.  
  
 Per ulteriori informazioni, vedere [Sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
### <a name="backup-and-restore"></a>Backup e ripristino  
 Le operazioni di backup e ripristino di un intero database di Analysis Services sono il metodo ottimale se la soluzione di data mining si basa su oggetti OLAP. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] offre nuove funzionalità di backup e ripristino che rendono più veloci e facili le operazioni di backup del database.  
  
 Per altre informazioni, vedere [Backup e ripristino di database di Analysis Services](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
### <a name="exporting-and-importing"></a>Esportazione e importazione  
 Le operazioni di esportazione e reimportazione di modelli e strutture di data mining mediante le istruzioni DMX costituiscono il modo più semplice per spostare o eseguire il backup di singoli oggetti di data mining relazionali. Per ulteriori informazioni sulla sintassi DMX per queste operazioni, vedere i seguenti argomenti:  
  
-   [EXPORT &#40;DMX&#41;](/sql/dmx/export-dmx)  
  
-   [IMPORT &#40;DMX&#41;](/sql/dmx/import-dmx)  
  
 Se si specifica l'opzione INCLUDE DEPENDENCIES, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esporterà anche la definizione di eventuali viste origine dati obbligatorie e, durante l'importazione del modello o della struttura, verrà ricreata la vista origine dati nel server di destinazione. Al termine dell'importazione del modello, assicurarsi di impostare le autorizzazioni di data mining necessarie per l'oggetto.  
  
> [!NOTE]  
>  Non è possibile esportare né importare modelli OLAP tramite DMX. Se il modello di data mining è basato su un cubo OLAP, è necessario usare le funzionalità di backup e ripristino di un intero database o di ridistribuzione del cubo e dei relativi modelli di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione degli oggetti e delle soluzioni di data mining](management-of-data-mining-solutions-and-objects.md)  
  
  
