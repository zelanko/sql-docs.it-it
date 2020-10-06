---
description: Elaborazione Analysis Services - attività
title: Attività Elaborazione Analysis Services | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.asprocessingtask.f1
- sql13.dts.designer.asprocessingtask.general.f1
- sql13.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2db38d2ad6c102b47b2a9f3349a3877a9d55a4c4
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727588"
---
# <a name="analysis-services-processing-task"></a>Elaborazione Analysis Services - attività

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Con l'attività Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile elaborare gli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quali modelli tabulari, cubi, dimensioni e modelli di data mining.  
  
 Quando si elaborano modelli tabulari, tenere presente quanto segue:  
  
-   Non è possibile effettuare analisi di impatto sui modelli tabulari.  
  
-   Alcune opzioni di elaborazione per la modalità tabulare non sono esposte, ad esempio Elaborazione deframmentazione e Elabora ricalcolo. È possibile eseguire queste funzioni tramite l'attività Esegui DDL.  
  
-   Le opzioni Elaborazione indice e Elaborazione di aggiornamento non sono appropriate per i modelli tabulari, pertanto non devono essere utilizzate.  
  
-   Le impostazioni batch vengono ignorate per i modelli tabulari.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono incluse diverse attività tramite cui è possibile effettuare operazioni di Business Intelligence, quali l'esecuzione di istruzioni DDL (Data Definition Language) e di query di stima basate su modelli di data mining. Per ulteriori informazioni sulle attività di Business Intelligence correlate, fare clic su uno degli argomenti seguenti:  
  
-   [Attività Esegui DDL Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Attività Query di data mining](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="object-processing"></a>Elaborazione di oggetti  
 È possibile elaborare più oggetti contemporaneamente. Per l'elaborazione di più oggetti è necessario definire impostazioni applicabili all'elaborazione di tutti gli oggetti nel batch.  
  
 Gli oggetti in un batch possono essere elaborati sequenzialmente o in parallelo. Se il batch non contiene oggetti per i quali la sequenza di elaborazione è importante, l'elaborazione parallela può accelerare l'operazione. Se gli oggetti nel batch vengono elaborati in parallelo, sarà possibile configurare l'attività in modo da determinare automaticamente il numero degli oggetti da elaborare in parallelo oppure specificare tale numero manualmente. Se gli oggetti vengono elaborati sequenzialmente, sarà possibile impostare un attributo di transazione sul batch integrando tutti gli oggetti in un'unica transazione oppure utilizzando una transazione distinta per ogni oggetto del batch.  
  
 Quando si elaborano oggetti di analisi può essere necessario elaborare anche gli oggetti che dipendono da questi ultimi. L'attività Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include un'opzione che, oltre agli oggetti selezionati, consente di elaborare anche tutti gli oggetti dipendenti.  
  
 In genere, si elaborano tabelle delle dimensioni prima di elaborare tabelle dei fatti. È possibile rilevare errori se si tenta di elaborare le tabelle dei fatti prima di elaborare le tabelle delle dimensioni.  
  
 Questa attività consente inoltre di configurare la gestione degli errori nelle chiavi delle dimensioni. È ad esempio possibile ignorare gli errori oppure arrestare l'attività dopo un numero di errori specificato. È possibile utilizzare la configurazione di gestione degli errori predefinita oppure creare una configurazione di gestione degli errori personalizzata, in cui sono specificate le condizioni di errore e la modalità con cui l'attività gestisce gli errori. È ad esempio possibile specificare che l'esecuzione dell'attività deve essere arrestata dopo il quarto errore oppure come devono essere gestiti i valori di chiave **Null** . La configurazione di gestione degli errori personalizzata può inoltre includere il percorso di un log degli errori.  
  
> [!NOTE]  
>  L'attività Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è in grado di elaborare solo oggetti di analisi creati utilizzando gli strumenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Questa attività viene spesso usata insieme a un'attività Inserimento bulk che carica dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure a un'attività Flusso di dati che implementa un flusso di dati per il caricamento di dati in una tabella. L'attività Flusso di dati può ad esempio includere un flusso di dati che estrae dati da un database OLTP (Online Transaction Processing) e li carica in una tabella dei fatti in un data warehouse, quindi chiama l'attività Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per elaborare il cubo compilato in base al data warehouse.  
  
 L'attività Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa una gestione connessione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per connettersi a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni, vedere [Gestione connessione Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
## <a name="error-handling"></a>Gestione degli errori  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Configurazione dell'attività Elaborazione Analysis Services  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Pagina Espressioni](../../integration-services/expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>Configurazione a livello di codice dell'attività Elaborazione Analysis Services  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
## <a name="analysis-services-processing-task-editor-general-page"></a>Editor attività Elaborazione Analysis Services (pagina Generale)
  La pagina **Generale** della finestra di dialogo **Editor attività Elaborazione Analysis Services** consente di denominare e descrivere l'attività Elaborazione Analysis Services.  
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Consente di specificare un nome univoco per l'attività Elaborazione Analysis Services. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di immettere una descrizione dell'attività Elaborazione Analysis Services.  
  
## <a name="analysis-services-processing-task-editor-analysis-services-page"></a>Editor attività Elaborazione Analysis Services (pagina Analysis Services)
  Usare la pagina **Analysis Services** della finestra di dialogo **Editor attività Elaborazione Analysis Services** per specificare una gestione connessione Analysis Services, selezionare gli oggetti analitici da elaborare e impostare le opzioni di elaborazione e di gestione degli errori.  
  
 Quando si elaborano modelli tabulari, tenere presente quanto segue:  
  
1.  Non è possibile effettuare analisi di impatto sui modelli tabulari.  
  
2.  Alcune opzioni di elaborazione per la modalità tabulare non sono esposte, ad esempio Elaborazione deframmentazione e Elabora ricalcolo. È possibile eseguire queste funzioni tramite l'attività Esegui DDL.  
  
3.  Alcune opzioni di elaborazione fornite, ad esempio l'elaborazione di indici, non sono appropriate per i modelli tabulari, pertanto non devono essere utilizzate.  
  
4.  Le impostazioni batch vengono ignorate per i modelli tabulari.  
  
### <a name="options"></a>Opzioni  
 **Analysis Services - gestione connessione**  
 Consente di selezionare una gestione connessione Analysis Services esistente nell'elenco o di crearne una nuova usando il pulsante **Nuova** .  
  
 **Nuovo**  
 Consente di creare una nuova gestione connessione Analysis Services.  
  
 **Argomenti correlati:** [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md), [Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Elenco oggetti**  
 
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**nome oggetto**|Consente di visualizzare i nomi degli oggetti specificati.|  
|**Tipo**|Consente di visualizzare i tipi degli oggetti specificati.|  
|**Opzioni elaborazione**|Consente di selezionare un'opzione di elaborazione nell'elenco.<br /><br /> **Argomenti correlati**: [Elaborazione di un modello multidimensionale &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services)|  
|**Impostazioni**|Consente di visualizzare le impostazioni di elaborazione per gli oggetti specificati.|  
  
 **Aggiungere**  
 Consente di aggiungere un oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] all'elenco.  
  
 **Rimuovi**  
 Selezionare un oggetto, quindi fare clic su **Elimina**.  
  
 **Analisi di impatto**  
 Consente di eseguire un'analisi di impatto sull'oggetto selezionato.  
  
 **Argomenti correlati:** [Finestra di dialogo Analisi di impatto &#40;Analysis Services - Dati multidimensionali&#41;](/analysis-services/analysis-services-overview?viewFallbackFrom=sql-server-ver15)  
  
 **Riepilogo impostazioni batch**  
 
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**Ordine di elaborazione**|Consente di specificare se gli oggetti devono essere elaborati sequenzialmente o in un batch. Se si utilizza l'elaborazione parallela, consente di specificare il numero di oggetti da elaborare simultaneamente.|  
|**Modalità transazione**|Consente di specificare la modalità di transazione per l'elaborazione sequenziale.|  
|**Errori dimensione**|Consente di specificare il funzionamento dell'attività quando si verificano errori.|  
|**Percorso log degli errori di chiave della dimensione**|Consente di specificare il percorso del file nel quale vengono registrati gli errori.|  
|**Elabora oggetti interessati**|Indica se vengono elaborati anche gli oggetti dipendenti o interessati.|  
  
 **Cambia impostazioni**  
 Consente di modificare le opzioni di elaborazione e la gestione degli errori nelle chiavi della dimensione.  
  
 **Argomenti correlati:** [Finestra di dialogo Cambia impostazioni &#40;Analysis Services - Dati multidimensionali&#41;](/analysis-services/analysis-services-overview?viewFallbackFrom=sql-server-ver15)