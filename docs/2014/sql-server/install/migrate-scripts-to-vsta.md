---
title: Eseguire la migrazione degli script a VSTA | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SSIS Script task, converting scripts
- Script component [Integration Services], converting scripts
- Script task [Integration Services], converting scripts
- SSIS Script component, converting scripts
ms.assetid: d685098b-86a1-46bf-939a-63d56951e009
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: cb44a7b635e24c0c2e3266c1cca98a9c4f6a347c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093993"
---
# <a name="migrate-scripts-to-vsta"></a>Migrare script a VSTA
  Quando si aggiornano [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] i [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a, esegue la migrazione degli script in qualsiasi attività script o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] componente di script a Tools for Applications (VSTA). VSTA è l'ambiente di scripting utilizzato da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]l'ambiente di scripting per [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] for Applications (VSA).  
  
 Se gli script nelle attività Script o nei componenti di script fanno riferimento a interfacce, potrebbe essere necessario modificare tali riferimenti prima di aggiornare il pacchetto. In caso contrario, il pacchetto non verrà aggiornato o gli script non verranno convalidati, a seconda del metodo di aggiornamento utilizzato. Per modificare questi riferimenti, sostituire i riferimenti alle interfacce IDTS*xxx*90 con riferimenti alle interfacce IDTS*xxx*100 corrispondenti.  
  
 Per ulteriori informazioni su come eseguire la migrazione degli script e aggiornare i pacchetti, vedere [upgrade Integration Services packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
## <a name="understanding-migration-failures"></a>Informazioni sugli errori di migrazione  
 Quando si esegue la migrazione degli script, la migrazione può non riuscire a causa di uno dei motivi seguenti:  
  
-   Il punto di ingresso per lo script VSA è stato rinominato.  
  
     Il punto di ingresso specifica il metodo nella classe `ScriptMain` nel progetto VSTA chiamato dal runtime di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come punto di ingresso nel codice dell'attività Script. La classe `ScriptMain` è la classe predefinita generata dai modelli di script.  
  
-   Nello script VSA non è presente alcun punto di ingresso o sono presenti più punti di ingresso.  
  
-   Non è stato possibile aggiungere riferimenti ad assembly.  
  
-   La classe `ScriptMain` è stata modificata per ereditare dalle altre classi oltre alla classe `ScriptObjectModelSSIS`. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] non supporta l'ereditarietà multipla.  
  
 Non è possibile convertire uno script VSA che [!INCLUDE[vbprvblong](../../includes/vbprvblong-md.md)] USA in uno script VSTA che [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]USA. Tuttavia, è possibile creare un nuovo script VSTA che utilizza [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]. Per altre informazioni, vedere [Scrittura di codice e debug dell'attività Script](../../integration-services/control-flow/script-task.md) e [Codifica e debug del componente Script](../../integration-services/data-flow/transformations/script-component.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Estensione di pacchetti tramite scripting](../../relational-databases/server-management-objects-smo/tasks/scripting.md)  
  
  
