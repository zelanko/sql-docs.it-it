---
title: Eseguire query di generatore (Creazione guidata Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.dataview.vdtquerydesigner.f1
- sql12.rtp.rptwizard.querybuilder.f1
helpviewer_keywords:
- Query Builder [Reporting Services]
ms.assetid: 1b0904ea-28c1-448e-b56c-c0fdfbc8b222
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6874f54f70e038cd7cafbb0c82a463513d9ed10d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657607"
---
# <a name="query-builder-report-wizard"></a>Generatore di query (Creazione guidata report)
  Utilizzare un generatore di query per specificare una query che recuperi un set di risultati da utilizzare in un report. È possibile scegliere tra due generatori di query:  
  
-   Il generatore di query generico predefinito offre un'area di lavoro estremamente semplice per l'impostazione di query e la visualizzazione dei risultati. È possibile specificare più istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] , la sintassi della query o dei comandi per estensioni per l'elaborazione dati personalizzata e query che vengono specificate come espressioni. Poiché il generatore di query generico non esegue la pre-elaborazione della query e può gestire qualsiasi tipo di sintassi della query, rappresenta lo strumento di compilazione delle query predefinito per Progettazione report.  
  
-   Il generatore di query grafico offre una rappresentazione visiva più efficace. Viene utilizzato in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e in altre parti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. È possibile utilizzare il generatore di query grafico se non si desidera creare espressioni o istruzioni SQL in più parti.  
  
     Per passare al generatore di query grafico, attivare o disattivare il pulsante **Modifica come testo** nell'angolo in alto a sinistra della finestra.  
  
 È inoltre possibile importare una query da un altro report.  
  
## <a name="query-builder-options"></a>Opzioni relative al generatore di query  
 **Modifica come testo**  
 Consente di passare tra una progettazione di query basata su testo e una grafica, se sono supportate entrambe dalla query.  
  
 **Importa**  
 Consente di aprire la finestra di dialogo **Importa query** e di visualizzare i file con estensione rdl e sql per qualsiasi report disponibile. È possibile utilizzare la query importata così com'è oppure modificarla nel generatore di query.  
  
 **\! (Run)**  
 Consente di eseguire la query e di restituire un set di risultati nel caso in cui la query sia valida. Si noti che non è possibile eseguire la query nel caso in cui questa sia un'espressione. Per verificare una query basata su un'espressione, è necessario visualizzare l'anteprima del report.  
  
 **Tipo di comando**  
 Consente di specificare direttamente testo, stored procedure o tabelle. La disponibilità di un determinato tipo di comando dipende dall'estensione per l'elaborazione dati specificata.  
  
 **Riquadro query**  
 Consente di digitare la query.  
  
 **Riquadro risultati**  
 Visualizza il set di risultati restituito da una query.  
  
## <a name="see-also"></a>Vedere anche  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Guida della Creazione guidata report](../../2014/reporting-services/report-wizard-help.md)  
  
  
