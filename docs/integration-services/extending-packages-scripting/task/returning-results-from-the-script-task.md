---
title: Restituzione di risultati dall'attività Script | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], status information
- ExecutionValue property
- status information [Integration Services]
- TaskResult property
- SSIS Script task, status information
ms.assetid: ac06805b-c2db-44bd-af5c-5a0debe36dd7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9a291a51aee2160d3b6680a2c5baac415e66bdf5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102859"
---
# <a name="returning-results-from-the-script-task"></a>Risultati restituiti dall'attività Script

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  L'attività Script utilizza la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> e la proprietà facoltativa <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> per restituire informazioni sullo stato al runtime di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] che è possibile utilizzare per determinare il percorso del flusso di lavoro al termine dell'attività Script.  
  
## <a name="taskresult"></a>TaskResult  
 La proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> indica l'esito positivo o negativo dell'attività. Esempio:  
  
 `Dts.TaskResult = ScriptResults.Success`  
  
## <a name="executionvalue"></a>ExecutionValue  
 La proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> restituisce facoltativamente un oggetto definito dall'utente che quantifica o fornisce ulteriori informazioni sull'esito positivo o negativo dell'attività Script. Ad esempio, l'attività FTP utilizza la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> per restituire il numero di file trasferiti. L'attività Esegui SQL restituisce il numero di righe interessate dall'attività. La proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> può anche essere utilizzata per determinare il percorso del flusso di lavoro. Esempio:  
  
 `Dim rowsAffected as Integer`  
  
 `...`  
  
 `rowsAffected = 1000`  
  
 `Dts.ExecutionValue = rowsAffected`  
