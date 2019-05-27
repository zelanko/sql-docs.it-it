---
title: Finestra di dialogo Proprietà assembly (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.assemblyproperties.f1
ms.assetid: da1174d6-d82b-4337-ac19-7368dbd95a84
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b21230ddff5a3db043b533a4f921a30b02da739b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062302"
---
# <a name="assembly-properties-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Proprietà assembly (Analysis Services - Dati multidimensionali)
  Utilizzare la finestra di dialogo **Proprietà assembly** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per impostare le proprietà di un riferimento ad assembly in un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . È possibile visualizzare la finestra di dialogo **Proprietà assembly** facendo clic con il pulsante destro del mouse su un assembly in **Esplora oggetti** e scegliendo **Proprietà**.  
  
## <a name="options"></a>Opzioni  
  
|Nome|Definizione|  
|----------|----------------|  
|**Name**|Consente di modificare il nome del riferimento a un assembly.<br /><br /> Nota: Se si modifica questo valore non modifica il nome dell'assembly a cui fa riferimento all'assembly, ma la modifica del nome utilizzato il di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] istanza o dal database quando si fa riferimento il riferimento all'assembly.|  
|**ID**|Consente di visualizzare l'ID dell'assembly a cui si riferisce il riferimento a un assembly.|  
|**Descrizione**|Consente di modificare la descrizione del riferimento a un assembly.|  
|**Timestamp creazione**|Consente di visualizzare la data e l'ora di creazione del riferimento a un assembly.|  
|**Ultimo aggiornamento schema**|Consente di visualizzare la data e l'ora dell'ultimo aggiornamento ai metadati per il riferimento a un assembly.|  
|**Tipo**|Consente di visualizzare il tipo del riferimento a un assembly. Vengono visualizzati i valori seguenti:<br /><br /> **Assembly .NET**: Il riferimento a un assembly si riferisce a un assembly di [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework.<br /><br /> **DLL COM**: Il riferimento a un assembly si riferisce a una libreria COM.|  
|**Origine**|Consente di visualizzare l'origine del riferimento a un assembly. Questa proprietà in genere contiene il percorso completo e il nome file di assembly a cui si riferisce il riferimento a un assembly.|  
|**Set di autorizzazioni**|Consente di selezionare il set di autorizzazioni utilizzato per determinare l'accesso al riferimento a un assembly. Per ulteriori informazioni sui valori disponibili per questa proprietà, vedere <xref:Microsoft.AnalysisServices.ClrAssembly.PermissionSet%2A>.|  
|**Impostazioni di rappresentazione**|Consente di selezionare le impostazioni di rappresentazione da utilizzare per l'accesso al riferimento a un assembly. Per altre informazioni sui valori disponibili per questa proprietà, vedere [Elemento ImpersonationInfo &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl)|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Gestione di assembly di modelli multidimensionali](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
