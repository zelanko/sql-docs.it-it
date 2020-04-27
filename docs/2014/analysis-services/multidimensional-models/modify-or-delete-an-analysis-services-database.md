---
title: Modificare o eliminare un database di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], modifying
- removing databases
- deleting databases
- dropping databases
- databases [Analysis Services], deleting
- modifying databases
ms.assetid: e48e3988-c091-4379-aabc-4da62f709a7e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f806501ffbb52f3839fa343a05a8db57917533ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073688"
---
# <a name="modify-or-delete-an-analysis-services-database"></a>Modificare o eliminare un database di Analysis Services
  È possibile modificare il nome e la descrizione di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] prima della distribuzione in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e dopo la distribuzione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. A seconda dell'ambiente di lavoro, è inoltre possibile modificare altre impostazioni di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
> [!NOTE]  
>  Le proprietà del database tuttavia non possono essere modificate quando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] è nella modalità online.  
  
## <a name="modifying-databases-using-sql-server-management-studio"></a>Modifica di databases tramite SQL Server Management Studio  
 Dopo la distribuzione di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è possibile modificare la modalità di rappresentazione utilizzata da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durante la connessione alle origini dei dati contenute nel database. Nella modalità di rappresentazione è possibile specificare il contesto di sicurezza utilizzato da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nei tentativi di connessione a un'origine dati a scopo di elaborazione, esplorazione e drill-through.  
  
## <a name="modifying-databases-using-sql-server-data-tools"></a>Modifica di database tramite SQL Server Data Tools  
 È possibile usare [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nella modalità progetto per modificare le traduzioni della didascalia e della descrizione di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usato per definire un database. Per ulteriori informazioni sull'utilizzo delle traduzioni in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] un database, vedere [scenari di globalizzazione per Analysis Services multidimensionale](../globalization-scenarios-for-analysis-services-multiidimensional.md).  
  
 È inoltre possibile impostare gli alias e le funzioni di aggregazione associate ai tipi di conto utilizzati dagli attributi Conto nelle dimensioni incluse in un database. Gli alias consentono di selezionare la terminologia aziendale specifica utilizzata all'interno di un'organizzazione per i tipi di conto in un grafico dei conti. I tipi di conto vengono utilizzati dai membri di un attributo Conto per indicare la modalità di aggregazione delle misure per ogni membro tramite le funzioni di aggregazione specificate per ogni tipo di conto incluso nel database. Per altre informazioni sugli attributi dell'account, vedere [Attributi e gerarchie di attributi](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
## <a name="deleting-databases"></a>eliminazione di database  
 Quando si elimina un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente vengono eliminati anche tutti i cubi, le dimensioni e i modelli di data mining del database. È possibile eliminare solo un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-delete-an-analysis-services-database"></a>Per eliminare un database di Analysis Services  
  
1.  Connettersi a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  In **Esplora oggetti**espandere il nodo dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] connessa e verificare che l'oggetto da eliminare sia visibile.  
  
3.  Fare clic con il pulsante destro del mouse sull'oggetto da eliminare e scegliere **Elimina**.  
  
4.  Nella finestra di dialogo **Elimina oggetto** fare clic su **OK**.  
  
## <a name="see-also"></a>Vedi anche  
 [Documentazione e script per un database di Analysis Services](document-and-script-an-analysis-services-database.md)  
  
  
