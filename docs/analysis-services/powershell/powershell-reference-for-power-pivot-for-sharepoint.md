---
title: Informazioni di riferimento di PowerShell per Analysis Services Power Pivot per SharePoint | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9228eb879ed1417b31c95d53783d32acf53bcdb4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62509809"
---
# <a name="powershell-reference-for-power-pivot-for-sharepoint"></a>Informazioni di riferimento su PowerShell per Power Pivot per SharePoint
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In questa sezione vengono elencati i cmdlet di PowerShell utilizzati per configurare o amministrare un'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Per altre informazioni sull'abilitazione dei cmdlet e la visualizzazione della Guida integrata, vedere [Configurazione di Power Pivot con Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).  

>[!NOTE] 
>Questo articolo può contenere esempi e informazioni obsolete. Usare il cmdlet Get-Help per la versione più recente.
  
## <a name="cmdlet-list"></a>Elenco di cmdlet  
 Per visualizzare un elenco di cmdlet dal prompt di PowerShell:  
  
1.  Aprire una shell di gestione di SharePoint usando l'opzione **Esegui come amministratore** .  
  
2.  Immettere il comando seguente: `Get-help *powerpivot*`  
  
|Cmdlet|Versioni supportate|  
|------------|------------------------|  
|[Cmdlet Get-PowerPivotServiceApplication](../../analysis-services/powershell/get-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Get-PowerPivotSystemService](../../analysis-services/powershell/get-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Get-PowerPivotSystemServiceInstance](../../analysis-services/powershell/get-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet New-PowerPivotServiceApplication](../../analysis-services/powershell/new-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet New-PowerPivotSystemServiceInstance](../../analysis-services/powershell/new-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Remove-PowerPivotServiceApplication](../../analysis-services/powershell/remove-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Remove-PowerPivotSystemServiceInstance](../../analysis-services/powershell/remove-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Set-PowerPivotServiceApplication](../../analysis-services/powershell/set-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Set-PowerPivotSystemService](../../analysis-services/powershell/set-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Update-PowerPivotSystemService](../../analysis-services/powershell/update-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
  
 Nota: I seguenti cmdlet funzionano solo con SharePoint 2010, quali [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] non supporta.  
  
-   Get-PowerPivotEngineService  
  
-   Get-PowerPivotEngineServiceInstance  
  
-   New-PowerPivotEngineServiceInstance  
  
-   Remove-PowerPivotEngineServiceInstance  
  
-   Set-PowerPivotEngineService  
  
-   Set-PowerPivotEngineServiceInstance  
  
-   Update-PowerPivotEngineService  
  
  
