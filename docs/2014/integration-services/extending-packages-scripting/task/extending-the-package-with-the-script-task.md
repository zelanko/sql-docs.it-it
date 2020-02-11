---
title: Estensione del pacchetto con l'attività Script | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- scripts [Integration Services]
- SSIS Script task
- tasks [Integration Services], scripts
- Script task [Integration Services], about Script task
- scripts [Integration Services], about Script task with packages
- SSIS Script task, about Script task
ms.assetid: 911e6d26-a6fd-4fc3-a111-bf5f048e9bff
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 10cfa4d5d9deeeeb6bc664fc6480e31bc5dc483e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62894775"
---
# <a name="extending-the-package-with-the-script-task"></a>Estensione del pacchetto con l'attività Script
  L'attività script estende le funzionalità di runtime dei pacchetti [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] di con codice personalizzato scritto in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# che viene compilato ed eseguito in fase di esecuzione del pacchetto. L'attività Script semplifica lo sviluppo di un'attività di runtime personalizzata quando le attività incluse in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] non soddisfano pienamente tutti i requisiti. L'attività Script scrive automaticamente tutto il codice dell'infrastruttura richiesto, consentendo agli sviluppatori di concentrarsi esclusivamente sul codice necessario per l'elaborazione personalizzata.  
  
 Un'attività Script interagisce con il pacchetto che la contiene tramite l'oggetto `Dts` globale, un'istanza della classe <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> esposta nell'ambiente di scripting. È possibile scrivere codice in un'attività Script che modifica i valori archiviati nelle variabili [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]; in seguito, il pacchetto può utilizzare questi valori aggiornati per determinare il percorso del proprio flusso di lavoro. L'attività Script può inoltre utilizzare lo spazio dei nomi [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] e la libreria di classi [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], nonché assembly personalizzati, per implementare la funzionalità personalizzata.  
  
 L'attività Script e il codice dell'infrastruttura che genera semplificano in modo significativo il processo di sviluppo di un'attività personalizzata. Tuttavia, per comprendere il funzionamento dell'attività Script, può risultare utile leggere la sezione [Sviluppo di un'attività personalizzata](../../extending-packages-custom-objects/task/developing-a-custom-task.md) per informazioni sui passaggi necessari per lo sviluppo di un'attività personalizzata.  
  
 Se si crea un'attività che si prevede di riutilizzare in più pacchetti, è preferibile sviluppare un'attività personalizzata anziché utilizzare l'attività Script. Per altre informazioni, vedere [Confronto tra soluzioni di scripting e oggetti personalizzati](../comparing-scripting-solutions-and-custom-objects.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 Negli argomenti seguenti vengono fornite ulteriori informazioni sull'attività Script.  
  
 [Configurazione dell'attività Script nell'editor attività Script](configuring-the-script-task-in-the-script-task-editor.md)  
 Illustra gli effetti delle proprietà configurate in **Editor trasformazione Script** sulle funzionalità e sulle prestazioni del codice dell'attività Script.  
  
 [Scrittura di codice e debug dell'attività Script](../../control-flow/script-task.md)  
 Viene illustrato come utilizzare [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) per sviluppare gli script contenuti nell'attività script.  
  
 [Uso delle variabili nell'attività Script](using-variables-in-the-script-task.md)  
 Viene descritto come utilizzare le variabili tramite la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>.  
  
 [Connessione a origini dati nell'attività Script](connecting-to-data-sources-in-the-script-task.md)  
 Viene descritto come utilizzare le connessioni tramite la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>.  
  
 [Generazione di eventi nell'attività Script](raising-events-in-the-script-task.md)  
 Viene descritto come generare eventi tramite la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>.  
  
 [Registrazione nell'attività Script](logging-in-the-script-task.md)  
 Viene descritto come registrare informazioni tramite il metodo <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>.  
  
 [Risultati restituiti dall'attività Script](returning-results-from-the-script-task.md)  
 Viene descritto come restituire risultati tramite le proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> e <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>.  
  
 [Esempi di attività Script](../../extending-packages-scripting-task-examples/script-task-examples.md)  
 Vengono forniti esempi che dimostrano diversi utilizzi possibili di un'attività Script.  
  
![Integration Services icona (piccola)](../../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video [!INCLUDE[msCoName](../../../includes/msconame-md.md)] più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] su MSDN:<br /><br /> [Visita la pagina Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività script](../../control-flow/script-task.md)   
 [Confronto tra l'attività Script e il componente script](../../extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
