---
title: Connettersi in modalità Online a un Database di Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 612e538ef01040778497242606115a01c6ef6921
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68179010"
---
# <a name="connect-in-online-mode-to-an-analysis-services-database"></a>Connettersi in modalità online a un database di Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  È possibile connettersi direttamente a un database esistente di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e modificare gli oggetti al suo interno. In caso di connessione diretta a un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , le modifiche agli oggetti vengono implementate in modo immediato e non viene creato alcun progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="to-connect-directly-to-an-analysis-services-database-by-using-sql-server-data-tools"></a>Per connettersi direttamente a un database di Analysis Services mediante gli strumenti dati di SQL Server  
  
1.  Aprire [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Scegliere **Apri** dal menu **File** e quindi fare clic su **Database di Analysis Services**.  
  
3.  Selezionare **Connetti a database esistente**.  
  
4.  Specificare il nome del server e il nome del database.  
  
     È possibile digitare il nome del database oppure eseguire una query sul server per visualizzare i database esistenti in tale server.  
  
5.  Fare clic su **OK**.  
  
     È ora possibile modificare direttamente qualsiasi oggetto all'interno del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di progetti e database di Analysis Services durante la fase di sviluppo](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-development.md)   
 [Creazione di modelli multidimensionali tramite SQL Server Data Tools &#40;SSDT&#41;](../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
  
  
