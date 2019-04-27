---
title: Restituzione di risultati dall'attività Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 77839c8b9e937e180ad188bd8aadb9792a35dfa2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768367"
---
# <a name="returning-results-from-the-script-task"></a>Risultati restituiti dall'attività Script
  L'attività Script utilizza la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> e la proprietà facoltativa <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> per restituire informazioni sullo stato al runtime di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] che è possibile utilizzare per determinare il percorso del flusso di lavoro al termine dell'attività Script.  
  
## <a name="taskresult"></a>TaskResult  
 La proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> indica l'esito positivo o negativo dell'attività. Ad esempio:  
  
 `Dts.TaskResult = ScriptResults.Success`  
  
## <a name="executionvalue"></a>ExecutionValue  
 La proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> restituisce facoltativamente un oggetto definito dall'utente che quantifica o fornisce ulteriori informazioni sull'esito positivo o negativo dell'attività Script. Ad esempio, l'attività FTP utilizza la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> per restituire il numero di file trasferiti. L'attività Esegui SQL restituisce il numero di righe interessate dall'attività. La proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> può anche essere utilizzata per determinare il percorso del flusso di lavoro. Ad esempio:   
  
 `Dim rowsAffected as Integer`  
  
 `...`  
  
 `rowsAffected = 1000`  
  
 `Dts.ExecutionValue = rowsAffected`  
  
![Icona di Integration Services (piccola)](../../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
  
