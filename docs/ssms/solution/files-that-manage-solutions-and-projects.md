---
title: File per la gestione di soluzioni e progetti | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], files
- .ssmssln files
- .ssmsmobileproj files
- .ssmsasproj files
- .ssmssqlproj files
- .sqlsuo files
- files [SQL Server Management Studio], projects
ms.assetid: e19d2859-0b97-4727-ac27-c4c226d86b2f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4b7be4d0cc64a72198525f059469f65b0c518a36
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65104968"
---
# <a name="files-that-manage-solutions-and-projects"></a>File per la gestione di soluzioni e progetti
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 In questo argomento vengono descritti i tipi di file specifici per [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per impostazione predefinita, tutte le soluzioni e i relativi progetti vengono creati in \Documenti\SQL Server Management Studio Projects.  


## <a name="management-studio-solution-files"></a>File della soluzione di Management Studio  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa tipi di file diversi di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] o [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Studio. Ciò vuol dire che non è possibile aprire una soluzione [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] o in Visual Studio. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] I file della soluzione consentono a Esplora soluzioni di visualizzare un'interfaccia grafica per la gestione dei file.  
   
|Estensione|Tipo di file|Descrizione|Creato da|  
|-------------|-------------|---------------|--------------|  
|ssmssln|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Oggetto della soluzione|Offre l'ambiente con riferimenti alla posizione sul disco di progetti, elementi di progetto e soluzione di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
  
## <a name="management-studio-project-files"></a>File del progetto di Management Studio  
Mentre le soluzioni contengono i file della soluzione per la gestione degli oggetti presenti in una soluzione, i progetti contengono i file del progetto. Il tipo di file del progetto creato da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per un progetto dipende dal modello utilizzato per la creazione del progetto stesso. Nella tabella seguente viene descritto il tipo di file creato per ogni progetto.  
   
|Estensione|Modelli di progetto|  
|-------------|--------------------|  
|ssmssqlproj|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Progetto di script|  
|ssmsasproj|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] Progetto di script|  
   
## <a name="location-of-solution-level-files"></a>Posizione dei file a livello di soluzione  
Per impostazione predefinita, i file a livello di soluzione vengono creati nella directory fisica del primo progetto creato con la soluzione. È possibile specificare una directory per la soluzione creando una soluzione oppure specificare la directory quando si crea un nuovo progetto.  
 
Se la struttura della directory è simile alla struttura logica visualizzata in Esplora soluzioni, è più facile individuare i file del progetto e della soluzione e condividerli con altri sviluppatori di un team.  
   
## <a name="see-also"></a>Vedere anche  
[Gestione di file con codifica](../../ssms/solution/manage-files-with-encoding.md)  
[File esterni](../../ssms/solution/miscellaneous-files.md)  
[Esplora soluzioni](../../ssms/solution/solution-explorer.md)  
[Soluzioni &#40;SQL Server Management Studio&#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[Progetti &#40;SQL Server Management Studio&#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
[Controllo del codice sorgente di Esplora soluzioni](https://msdn.microsoft.com/library/ms173879.aspx)  
  
