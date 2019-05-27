---
title: Oggetto di associazione nella finestra di dialogo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.objectbinding.f1
helpviewer_keywords:
- Object Binding dialog box
ms.assetid: 2bb5ad7c-2962-4559-8c95-cf7148bd2e72
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9cc86a5712dae9c231fa6e03d86a82d7dc172a75
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072193"
---
# <a name="object-binding-dialog-box"></a>Finestra di dialogo Associazione oggetto
  Utilizzare la finestra di dialogo **Associazione oggetto** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per definire associazioni tra la proprietà di un oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e una tabella o una colonna di una vista origine dati. Per visualizzare la finestra di dialogo **Associazione oggetto** selezionare **(nuovo)** nell'elenco a discesa per il valore delle proprietà seguenti di un oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nella finestra **Proprietà** di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]:  
  
-   NameColumn  
  
-   ValueColumn  
  
-   CustomRollupColumn  
  
-   CustomRollupPropertiesColumn  
  
-   UnaryOperatorColumn  
  
## <a name="options"></a>Opzioni  
 **Tipo di associazione**  
 Consente di selezionare l'associazione da utilizzare per l'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . È possibile utilizzare i tipi di associazione seguenti:  
  
 Associazione colonna  
 Consente di associare l'oggetto a una tabella e a una colonna esistenti in una vista origine dati.  
  
 Genera colonna  
 Consente di indicare che è necessario definire una nuova colonna nella vista origine dati. Su tale colonna verrà quindi eseguita un'associazione colonna.  
  
> [!NOTE]  
>  Se questa opzione è selezionata è necessario eseguire la **Generazione guidata schema** prima di distribuire l'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 Associazione righe  
 Consente di associare l'oggetto a una riga in una tabella dei fatti, in modo da semplificare le misure Distinct Count in base al numero di righe elaborate nella tabella dei fatti.  
  
 **Tabella di origine**  
 Consente di visualizzare un elenco di tabelle nella vista origine dati associate all'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 **Colonna di origine**  
 Consente di visualizzare un elenco di colonne nella tabella selezionata in **Tabella di origine**.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
