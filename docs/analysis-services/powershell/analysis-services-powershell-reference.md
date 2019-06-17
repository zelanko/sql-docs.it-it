---
title: Analysis Services PowerShell Reference | Microsoft Docs
ms.date: 06/25/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13ea15a23bbf6de6c50b494f709f65cae2f7c48b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509839"
---
# <a name="analysis-services-powershell-reference"></a>Guida di riferimento a PowerShell per Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] I cmdlet di PowerShell sono inclusi nel [modulo SqlServer](https://www.powershellgallery.com/packages/SqlServer/21.0.17099). 
  
>[!NOTE] 
> Operazioni di database Azure Analysis Services usano lo stesso modulo SqlServer di SQL Server Analysis Services. Tuttavia, non tutti i cmdlet sono supportati per Azure Analysis Services. Per altre informazioni, vedere [gestire Azure Analysis Services con PowerShell](https://docs.microsoft.com/azure/analysis-services/analysis-services-powershell).
  
##  <a name="bkmk_cmdlets"></a> Cmdlet di Analysis Services  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornisce cmdlet che corrispondono ai metodi nello spazio dei nomi **Microsoft.AnalysisServices** . Nella tabella seguente viene descritto ogni cmdlet e viene fornito un collegamento al metodo AMO (Analysis Management Objects) corrispondente.  
  
 Se si vuole usare PowerShell per eseguire un'attività non inclusa nell'elenco seguente (ad esempio creare o sincronizzare un database), è possibile scrivere uno script TMSL o XMLA per tale azione, quindi eseguire lo script usando il cmdlet **Invoke-ASCmd** .  
  
|Cmdlet|Descrizione|Metodi AMO equivalenti|  
|------------|-----------------|----------------------------|  
|[Cmdlet Add-RoleMember](https://docs.microsoft.com/powershell/module/sqlserver/Add-RoleMember)|Aggiungere un membro a un ruolo del database.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Cmdlet Backup-ASDatabase](https://docs.microsoft.com/powershell/module/sqlserver/backup-asdatabase)|Eseguire il backup di un database di Analysis Services.|[Database.Backup](https://msdn.microsoft.com/library/microsoft.analysisservices.database.backup.aspx)|  
|[Cmdlet Invoke-ASCmd](https://docs.microsoft.com/powershell/module/sqlserver/invoke-ascmd)|Eseguire una query o uno script in formato XMLA o TSML (JSON).|<xref:Microsoft.AnalysisServices.Core.Server.Execute%2A>|  
|[Cmdlet Invoke-ProcessASDatabase](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processasdatabase)|Elaborare un database.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessCube](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processcube)|Elaborare un cubo.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessDimension](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processdimension)|Elaborare una dimensione.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessPartition](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processpartition)|Elaborare una partizione.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessTable](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processtable)|Elaborare una tabella in un modello tabulare, il modello di compatibilità 1200 o superiore.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Merge-Partition](https://docs.microsoft.com/powershell/module/sqlserver/merge-partition)|Unire una partizione.|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[Cmdlet New-RestoreFolder](https://docs.microsoft.com/powershell/module/sqlserver/new-restorefolder)|Creare una cartella per contenere il backup di un database.|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[Cmdlet New-RestoreLocation](https://docs.microsoft.com/powershell/module/sqlserver/new-restorelocation)|Specificare uno o più server remoti in cui ripristinare il database.|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Cmdlet Remove-RoleMember](https://docs.microsoft.com/powershell/module/sqlserver/remove-rolemember)|Rimuovere un membro da un ruolo del database.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Cmdlet Restore-ASDatabase](https://docs.microsoft.com/powershell/module/sqlserver/restore-asdatabase)|Ripristinare un database in un'istanza del server.|<xref:Microsoft.AnalysisServices.Core.Server.Restore%2A>|  
  

  
  
