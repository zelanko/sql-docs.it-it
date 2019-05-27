---
title: Rinominare un Database multidimensionale (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- renaming databases
ms.assetid: 15fdaec7-f3e4-44d9-9b78-1a1d78c484e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 28ec21d4cb0cda01852316c1198bd68df3058ffc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66073147"
---
# <a name="rename-a-multidimensional-database-analysis-services"></a>Rinominare un database multidimensionale (Analysis Services)
  Il modo in cui il nome di un database di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene modificato dipende dalla modalità di connessione al database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Per modificare il nome di un database esistente, è necessario connettersi in modalità online. Per modificare il nome del database in cui verranno create istanze degli oggetti di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è necessario connettersi in modalità progetto.  
  
### <a name="to-change-the-database-name-in-online-mode"></a>Per modificare il nome del database in modalità online  
  
1.  Connettersi direttamente al database di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]utilizzando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul database e quindi scegliere **Modifica database**.  
  
3.  Nella casella di testo **Nome database** modificare il nome del database.  
  
4.  Fare clic su **Salva** o **Salva tutto** sulla barra degli strumenti, scegliere **Salva elementi selezionati** o **Salva tutto** dal menu **File** oppure chiudere **Progettazione database** e quindi fare clic su **Salva** quando richiesto.  
  
     Il nome del database verrà aggiornato nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e l'oggetto di database verrà aggiornato in Esplora soluzioni.  
  
### <a name="to-change-the-database-name-in-project-mode"></a>Per modificare il nome del database in modalità progetto  
  
1.  Aprire il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e quindi scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Pagine delle proprietà** fare clic su **Distribuzione** nella sezione **Proprietà di configurazione** .  
  
4.  Modificare la proprietà **Database** nel nuovo nome del database.  
  
     La successiva distribuzione del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verrà eseguita per questo nuovo nome di database. Se il database esiste già, verrà sovrascritto.  
  
### <a name="to-change-the-database-name-using-sql-server-management-studio"></a>Per modificare il nome del database tramite SQL Server Management Studio  
  
-   Fare clic con il pulsante destro del mouse sul database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e modificare la proprietà Name.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le proprietà del Server in Analysis Services](../server-properties/server-properties-in-analysis-services.md)   
 [Impostare le proprietà dei database multidimensionali &#40;Analysis Services&#41;](set-multidimensional-database-properties-analysis-services.md)   
 [Configurare proprietà di progetti di Analysis Services &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)   
 [Distribuire progetti di Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
