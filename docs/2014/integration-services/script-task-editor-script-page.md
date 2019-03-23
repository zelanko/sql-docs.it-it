---
title: Editor attività script (pagina Script) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scripttask.script.f1
helpviewer_keywords:
- Script Task Editor
ms.assetid: 93da0e0d-83f5-406d-b144-4cce216571cb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 18be600182e3ebef6a13e19fecd7af06be2c19ec
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390119"
---
# <a name="script-task-editor-script-page"></a>Editor attività Script (pagina Script)
  Utilizzare la pagina **Script** della finestra di dialogo **Editor attività Script** per impostare le proprietà dello script e specificare le variabili accessibili per lo script.  
  
> [!NOTE]  
>  In [!INCLUDE[ssISversion10](../includes/ssisversion10-md.md)] e versioni successive, tutti gli script sono precompilati. Nelle versioni precedenti, si imposta una proprietà **PrecompileScriptIntoBinaryCode** per specificare che lo script è stato precompilato.  
  
 Per ulteriori informazioni sull'attività Script, vedere [Script Task](control-flow/script-task.md) e [Configurazione dell'attività Script nell'editor attività Script](extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md). Per informazioni sulla programmazione dell'attività Script, vedere [Estensione del pacchetto con l'attività Script](extending-packages-scripting/task/extending-the-package-with-the-script-task.md).  
  
## <a name="options"></a>Opzioni  
 **ScriptLanguage**  
 Selezionare il linguaggio di scripting per l'attività, [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#.  
  
 Dopo avere creato uno script per l'attività, non è possibile modificare il valore della proprietà **ScriptLanguage** .  
  
 Per impostare il linguaggio di scripting predefinito per l'attività Script, utilizzare l'opzione **Linguaggio di scripting** nella pagina **Generale** della finestra di dialogo **Opzioni** . Per ulteriori informazioni, vedere [General Page](general-page-of-integration-services-designers-options.md).  
  
 **EntryPoint**  
 Specificare il metodo chiamato dal runtime [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] come punto di ingresso nel codice dell'attività Script. Il metodo specificato deve essere nella classe ScriptMain del progetto [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA). ScriptMain è la classe predefinita generata dai modelli di script.  
  
 Se si modifica il nome del metodo nel progetto VSTA, è necessario modificare il valore della proprietà **EntryPoint** .  
  
 **ReadOnlyVariables**  
 Digitare un elenco delimitato da virgole di variabili di sola lettura disponibili per lo script oppure fare clic sul pulsante con i puntini di sospensione (**...**) e selezionare le variabili nella finestra di dialogo **Seleziona variabili**.  
  
> [!NOTE]  
>  Per i nomi delle variabili viene fatta distinzione tra maiuscole e minuscole.  
  
 **ReadWriteVariables**  
 Digitare un elenco delimitato da virgole di variabili di lettura/scrittura disponibili per lo script oppure fare clic sul pulsante con i puntini di sospensione (**...**) e selezionare le variabili nella finestra di dialogo **Seleziona variabili**.  
  
> [!NOTE]  
>  Per i nomi delle variabili viene fatta distinzione tra maiuscole e minuscole.  
  
 **Modifica script**  
 Apre VSTA IDE, dove è possibile creare o modificare lo script.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [General Page](general-page-of-integration-services-designers-options.md)   
 [Editor attività Script &#40;pagina Generale&#41;](../../2014/integration-services/script-task-editor-general-page.md)   
 [Pagina Espressioni](expressions/expressions-page.md)   
 [Esempi di attività Script](extending-packages-scripting-task-examples/script-task-examples.md)   
 [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)   
 [Aggiungere, eliminare o modificare l'ambito di una variabile definita dall'utente in un pacchetto](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
  
