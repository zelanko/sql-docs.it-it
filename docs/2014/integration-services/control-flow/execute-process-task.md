---
title: Attività Esegui processo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executeprocesstask.f1
helpviewer_keywords:
- Execute Process task [Integration Services]
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b21aa5d2834143ab012b90e0fa6f8a1e22a8314
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831865"
---
# <a name="execute-process-task"></a>Attività Esegui processo
  L'attività Esegui processo consente di eseguire un'applicazione o un file batch nell'ambito del flusso di lavoro di un pacchetto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Sebbene sia possibile usarla per aprire qualsiasi applicazione standard, ad esempio [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] o [!INCLUDE[ofprword](../../includes/ofprword-md.md)], l'attività Esegui processo viene in genere usata per eseguire applicazioni aziendali o file batch che usano un'origine dei dati. È ad esempio possibile utilizzare l'attività Esegui processo per espandere un file di testo compresso. Il pacchetto può quindi utilizzare il file di testo come origine dei dati per il proprio flusso di dati. Sempre a titolo di esempio, è anche possibile utilizzare tale attività per eseguire un'applicazione [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] personalizzata che genera un report giornaliero sulle vendite, che può essere allegato a un'attività Invia messaggi e inoltrato a una lista di distribuzione.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include altre attività che consentono l'esecuzione di operazioni di flusso di lavoro, quale l'esecuzione di pacchetti. Per altre informazioni, vedere [Attività Esegui pacchetto](execute-package-task.md)  
  
## <a name="custom-log-entries-available-on-the-execute-process-task"></a>Voci di log personalizzate disponibili nell'attività Esegui processo  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Esegui processo. Per altre informazioni, vedere [Registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) e [Messaggi personalizzati per la registrazione](../custom-messages-for-logging.md).  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|Fornisce informazioni sui processi che l'attività dovrà eseguire.<br /><br /> Vengono scritte due voci di log. Una contiene informazioni sul nome e sulla posizione del file eseguibile eseguito dall'attività, l'altra registra l'uscita dal file eseguibile.|  
|`ExecuteProcessVariableRouting`|Fornisce informazioni sulle variabili indirizzate all'input e agli output del file eseguibile. Vengono scritte voci di log per stdin (l'input), stdout (l'output) e stderr (l'output degli errori).|  
  
## <a name="configuration-of-the-execute-process-task"></a>Configurazione dell'attività Esegui processo  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Esegui processo &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor attività Esegui processo &#40;pagina Processo&#41;](../execute-process-task-editor-process-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="property-settings"></a>Impostazioni delle proprietà  
 Quando l'attività Esegui processo esegue un'applicazione personalizzata, fornisce dati di input all'applicazione tramite uno o entrambi i metodi seguenti:  
  
-   Una variabile specificata nell'impostazione della proprietà **StandardInputVariable**. Per altre informazioni sulle variabili, vedere [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](../use-variables-in-packages.md).  
  
-   Un argomento specificato nell'impostazione della proprietà **Arguments**. Se, ad esempio, l'attività apre un documento in Word, l'argomento può assegnare un nome al file con estensione doc.  
  
 Per passare più argomenti a un'applicazione personalizzata in un'attività Esegui processo, utilizzare gli spazi per delimitarli. Un argomento non può includere uno spazio. In caso contrario, l'attività non verrà eseguita. È possibile utilizzare un'espressione per passare il valore di una variabile come argomento. Nell'esempio seguente l'espressione passa due valori di variabili come argomenti e utilizza uno spazio per delimitare gli argomenti:  
  
 `@variable1 + " " + @variable2`  
  
 È possibile utilizzare un'espressione per impostare varie proprietà dell'attività Esegui processo.  
  
 Quando si usa la **StandardInputVariable** proprietà per configurare l'attività Esegui processo per un input, chiamare il `Console.ReadLine` metodo dall'applicazione per leggere l'input. Per altre informazioni, vedere l'argomento [Console.ReadLine Method](https://go.microsoft.com/fwlink/?LinkId=129201)nella libreria di classi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
 Quando si usa la proprietà **Arguments** per configurare l'attività Esegui processo in modo che fornisca dati di input, effettuare uno dei passaggi seguenti per ottenere gli argomenti:  
  
-   Se si usa Microsoft Visual Basic per scrivere l'applicazione, impostare la proprietà `My.Application.CommandLineArgs`. Nell'esempio seguente viene impostata la proprietà `My.Application.CommandLineArgs` per recuperare due argomenti:  
  
    ```  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     Per altre informazioni, vedere l'argomento [Proprietà My.Application.CommandLineArgs](https://go.microsoft.com/fwlink/?LinkId=129200)nei riferimenti di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .  
  
-   Se si utilizza Microsoft Visual C# per scrivere l'applicazione, utilizzare il metodo `Main`.  
  
     Per altre informazioni, vedere l'argomento [Argomenti della riga di comando (Guida per programmatori C#)](https://go.microsoft.com/fwlink/?LinkId=129406)nella Guida per programmatori C#.  
  
 L'attività Esegui processo include inoltre le proprietà **StandardOutputVariable** e **StandardErrorVariable** che consentono di specificare le variabili che usano rispettivamente l'output standard e l'output degli errori dell'applicazione.  
  
 È inoltre possibile configurare l'attività Esegui processo specificando una directory di lavoro, un periodo di timeout o un valore che indica se l'esecuzione del file eseguibile è stata completata. L'attività può essere configurata anche in modo da non riuscire se il codice restituito dal file eseguibile non corrisponde al valore che indica il completamento dell'esecuzione oppure se il file eseguibile non viene trovato nel percorso specificato.  
  
## <a name="programmatic-configuration-of-the-execute-process-task"></a>Configurazione a livello di codice dell'attività Esegui processo  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di Integration Services](integration-services-tasks.md)   
 [Flusso di controllo](control-flow.md)  
  
  
