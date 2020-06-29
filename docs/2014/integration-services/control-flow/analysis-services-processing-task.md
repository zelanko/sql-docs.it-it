---
title: Attività Elaborazione Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asprocessingtask.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3e0b4cb1d3602b29f29e0de6d2beea07bc21831d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85434158"
---
# <a name="analysis-services-processing-task"></a>Elaborazione Analysis Services - attività
  Con l'attività Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile elaborare gli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quali modelli tabulari, cubi, dimensioni e modelli di data mining.  
  
 Quando si elaborano modelli tabulari, tenere presente quanto segue:  
  
-   Non è possibile effettuare analisi di impatto sui modelli tabulari.  
  
-   Alcune opzioni di elaborazione per la modalità tabulare non sono esposte, ad esempio Elaborazione deframmentazione e Elabora ricalcolo. È possibile eseguire queste funzioni tramite l'attività Esegui DDL.  
  
-   Le opzioni Elaborazione indice e Elaborazione di aggiornamento non sono appropriate per i modelli tabulari, pertanto non devono essere utilizzate.  
  
-   Le impostazioni batch vengono ignorate per i modelli tabulari.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono incluse diverse attività tramite cui è possibile effettuare operazioni di Business Intelligence, quali l'esecuzione di istruzioni DDL (Data Definition Language) e di query di stima basate su modelli di data mining. Per ulteriori informazioni sulle attività di Business Intelligence correlate, fare clic su uno degli argomenti seguenti:  
  
-   [Attività Esegui DDL Analysis Services](analysis-services-execute-ddl-task.md)  
  
-   [Attività Query di data mining](data-mining-query-task.md)  
  
## <a name="object-processing"></a>Elaborazione di oggetti  
 È possibile elaborare più oggetti contemporaneamente. Per l'elaborazione di più oggetti è necessario definire impostazioni applicabili all'elaborazione di tutti gli oggetti nel batch.  
  
 Gli oggetti in un batch possono essere elaborati sequenzialmente o in parallelo. Se il batch non contiene oggetti per i quali la sequenza di elaborazione è importante, l'elaborazione parallela può accelerare l'operazione. Se gli oggetti nel batch vengono elaborati in parallelo, sarà possibile configurare l'attività in modo da determinare automaticamente il numero degli oggetti da elaborare in parallelo oppure specificare tale numero manualmente. Se gli oggetti vengono elaborati sequenzialmente, sarà possibile impostare un attributo di transazione sul batch integrando tutti gli oggetti in un'unica transazione oppure utilizzando una transazione distinta per ogni oggetto del batch.  
  
 Quando si elaborano oggetti di analisi può essere necessario elaborare anche gli oggetti che dipendono da questi ultimi. L'attività Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include un'opzione che, oltre agli oggetti selezionati, consente di elaborare anche tutti gli oggetti dipendenti.  
  
 In genere, si elaborano tabelle delle dimensioni prima di elaborare tabelle dei fatti. È possibile rilevare errori se si tenta di elaborare le tabelle dei fatti prima di elaborare le tabelle delle dimensioni.  
  
 Questa attività consente inoltre di configurare la gestione degli errori nelle chiavi delle dimensioni. È ad esempio possibile ignorare gli errori oppure arrestare l'attività dopo un numero di errori specificato. È possibile utilizzare la configurazione di gestione degli errori predefinita oppure creare una configurazione di gestione degli errori personalizzata, in cui sono specificate le condizioni di errore e la modalità con cui l'attività gestisce gli errori. È ad esempio possibile specificare che l'esecuzione dell'attività deve essere arrestata dopo il quarto errore oppure come devono essere gestiti i valori di chiave **Null** . La configurazione di gestione degli errori personalizzata può inoltre includere il percorso di un log degli errori.  
  
> [!NOTE]  
>  L'attività Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è in grado di elaborare solo oggetti di analisi creati utilizzando gli strumenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Questa attività viene spesso usata insieme a un'attività Inserimento bulk che carica dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure a un'attività Flusso di dati che implementa un flusso di dati per il caricamento di dati in una tabella. L'attività Flusso di dati può ad esempio includere un flusso di dati che estrae dati da un database OLTP (Online Transaction Processing) e li carica in una tabella dei fatti in un data warehouse, quindi chiama l'attività Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per elaborare il cubo compilato in base al data warehouse.  
  
 L'attività Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa una gestione connessione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per connettersi a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni, vedere [Gestione connessione Analysis Services](../connection-manager/analysis-services-connection-manager.md).  
  
## <a name="error-handling"></a>Gestione degli errori  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Configurazione dell'attività Elaborazione Analysis Services  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Elaborazione Analysis Services &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor attività Elaborazione Analysis Services &#40;pagina Analysis Services&#41;](../analysis-services-processing-task-editor-analysis-services-page.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>Configurazione a livello di codice dell'attività Elaborazione Analysis Services  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
  
