---
title: Lavorare con i progetti e i database nell'ambiente di produzione di Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f90af41c397da20fb26c73bebc6723b9a3cf6270
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62743237"
---
# <a name="work-with-analysis-services-projects-and-databases-in-production"></a>Lavorare con i progetti e i database nell'ambiente di produzione di Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Dopo aver sviluppato e distribuito il database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dal progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è necessario decidere come si desidera apportare modifiche agli oggetti del database distribuito. Alcune modifiche, ad esempio quelle relative ai ruoli di sicurezza, al partizionamento e alle impostazioni di archiviazione, possono essere apportate mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Altre modifiche, ad esempio l'aggiunta di attributi o gerarchie definite dall'utente, possono essere apportate soltanto usando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]in modalità progetto o in modalità online.  
  
 Non appena si apporta una modifica a un database distribuito di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] in modalità online, il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usato per la distribuzione risulta obsoleto. Se uno sviluppatore apporta qualsiasi modifica all'interno del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e tenta di distribuire il progetto modificato, verrà richiesto di sovrascrivere l'intero database. In caso di sovrascrittura dell'intero database, è inoltre necessario eseguirne l'elaborazione. Il problema risulta ancora più complesso se le modifiche apportate direttamente al database distribuito dal personale di produzione non sono state comunicate al team di sviluppo, poiché non sarà in grado di comprendere il motivo per cui le relative modifiche non vengono più riportate nel database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Per evitare i problemi intrinseci di questa situazione, è possibile utilizzare gli strumenti di SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in diversi modi.  
  
-   Metodo 1: Ogni volta che viene apportata una modifica a una versione di produzione di un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del database, utilizzare [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per creare un nuovo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto basato sulla versione modificata del [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database. Questo nuovo progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] può essere archiviato nel sistema di controllo del codice sorgente come copia master del progetto. Questo metodo è applicabile indipendentemente dal fatto che la modifica venga apportata al database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] in modalità online.  
  
-   Metodo 2: Apportare solo modifiche alla versione di produzione di un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del database utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] in modalità progetto. Questo metodo consente di utilizzare le opzioni disponibili nella Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per mantenere le modifiche apportate da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ad esempio per i ruoli di sicurezza e le impostazioni di archiviazione. È così possibile garantire che vengano mantenute le impostazioni relative alla progettazione nel file di progetto (ignorando impostazioni di archiviazione e ruoli di sicurezza) e che per le impostazioni di archiviazione e i ruoli di sicurezza venga utilizzato il server online.  
  
-   Metodo 3: Apportare solo modifiche alla versione di produzione di un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del database utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] in modalità online. Poiché entrambi gli strumenti utilizzano solo lo stesso server online, non è possibile ottenere una diversa versione non sincronizzata.  
  
  
