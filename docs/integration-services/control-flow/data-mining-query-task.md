---
title: Attività Query di data mining | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquerytask.f1
- sql13.dts.designer.dmquerytask.miningmodel.f1
- sql13.dts.designer.dmquerytask.query.f1
- sql13.dts.designer.dmquerytask.output.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e678774a8da38b8ff2e8c64adc7309828d6dffb6
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919837"
---
# <a name="data-mining-query-task"></a>Attività Query di data mining

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  L'attività Query di data mining consente di eseguire query di stima basate sui modelli di data mining compilati in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Una query di stima genera una stima per nuovi dati utilizzando modelli di data mining. È ad esempio possibile utilizzare una query di stima per stimare il numero di barche a vela che si prevede di vendere durante i mesi estivi o per generare un elenco dei potenziali clienti che probabilmente acquisteranno una barca a vela.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornisce attività che consentono di eseguire altre operazioni di Business Intelligence, quali l'esecuzione di istruzioni DDL (Data Definition Language) e l'elaborazione di oggetti di analisi.  
  
 Per ulteriori informazioni su altre attività di Business Intelligence, fare clic su uno degli argomenti seguenti:  
  
-   [Attività Esegui DDL Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Attività Elaborazione Analysis Services](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>Query di stima  
 La query è un'istruzione DMX (Data Mining Extensions). Il linguaggio DMX è un'estensione del linguaggio SQL che consente di supportare l'utilizzo dei modelli di data mining. Per altre informazioni su come usare il linguaggio DMX, vedere [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../../dmx/data-mining-extensions-dmx-reference.md).  
  
 L'attività consente di eseguire query su più modelli di data mining compilati in base alla stessa struttura di data mining. Per compilare un modello di data mining è necessario usare uno degli algoritmi di data mining disponibili in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La struttura di data mining a cui fa riferimento l'attività Query di data mining può includere più modelli di data mining, compilati utilizzando algoritmi diversi. Per altre informazioni, vedere [Strutture di data mining &#40;Analysis Services – Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-structures-analysis-services-data-mining) e [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining).  
  
 La query di stima eseguita dall'attività Query di data mining restituisce un risultato costituito da una singola riga o da un set di dati. Una query che restituisce una singola riga è detta query singleton. La query per la stima del numero di barche a vela che si prevede di vendere nei mesi estivi, ad esempio, restituisce un numero. Per altre informazioni sulle query di stima che restituiscono una singola riga, vedere [Data Mining Query Tools](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools)(Strumenti query di data mining).  
  
 I risultati delle query vengono salvati in tabelle. Se esiste già una tabella con il nome specificato dall'attività Query di data mining, l'attività può creare una nuova tabella con lo stesso nome, a cui viene aggiunto un numero, oppure sovrascrivere il contenuto della tabella.  
  
 Se il set di risultati è nidificato, verrà convertito in formato flat prima del salvataggio. La conversione in formato flat trasforma un set di risultati nidificato in una tabella. Se ad esempio si converte in formato flat un set di risultati annidato che include una colonna di nome **Customer** e una colonna annidata di nome **Product** , alla colonna **Customer** verranno aggiunte le righe necessarie per ottenere una tabella che include dati sui prodotti per ogni cliente. Per un cliente con tre prodotti diversi, ad esempio, si ottiene una tabella con tre righe, ognuna delle quali contiene il nome del cliente ripetuto e un nome di prodotto diverso. Se la parola chiave FLATTENED viene omessa, la tabella conterrà solo la colonna **Customer** e una sola riga per cliente. Per altre informazioni, vedere [SELECT &#40;DMX&#41;](../../dmx/select-dmx.md).  
  
## <a name="configuration-of-the-data-mining-query-task"></a>Configurazione dell'attività Query di data mining  
 Per l'attività Query di data mining sono necessarie due connessioni. La prima è una gestione connessione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che stabilisce la connessione a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contenente la struttura e il modello di data mining. La seconda è una gestione connessione OLE DB che stabilisce la connessione al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente la tabella in cui l'attività scrive i dati. Per altre informazioni, vedere [Gestione connessione Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md) e [Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
> [!NOTE]  
>  L'Editor attività Query di data mining non include la pagina Espressioni. È tuttavia possibile usare la finestra **Proprietà** per accedere agli strumenti per la creazione e la gestione di espressioni di proprietà per le proprietà dell'attività Query di data mining.  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>Configurazione a livello di codice dell'attività Query di data mining  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
## <a name="data-mining-query-task-editor-mining-model-tab"></a>Editor attività Query di data mining (scheda Modello di data mining)
  Utilizzare la scheda **Modello di data mining** della finestra di dialogo **Editor attività Query di data mining** per specificare la struttura e il modello di data mining da utilizzare.  
  
 Per informazioni sull'implementazione di data mining nei pacchetti, vedere [Attività Query di data mining](../../integration-services/control-flow/data-mining-query-task.md) e [Soluzioni di data mining](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions).  
  
### <a name="general-options"></a>Opzioni generali  
 **Nome**  
 Consente di specificare un nome univoco per l'attività Query di data mining. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Query di data mining.  
  
### <a name="mining-model-tab-options"></a>Opzioni della scheda Modello di data mining  
 **Connection**  
 Consente di selezionare una gestione connessione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nell'elenco o di creare una nuova gestione connessione facendo clic sul pulsante **Nuova** .  
  
 **Argomenti correlati:**  [Gestione connessione Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **Nuovo**  
 Consente di creare una nuova gestione connessione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 **Argomenti correlati:** [Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Struttura di data mining**  
 Consente di selezionare una struttura di data mining nell'elenco.  
  
 **Modelli di data mining**  
 Consente di selezionare un modello di data mining compilato in base alla struttura di data mining selezionata.  

## <a name="data-mining-query-task-editor-query-tab"></a>Editor attività Query di data mining (scheda Query)
  Usare la scheda **Query** della finestra di dialogo **Attività Query di data mining** per creare query di stima basate su un modello di data mining. In questa finestra di dialogo è inoltre possibile associare parametri e set di risultati a variabili.  
  
 Per informazioni sull'implementazione di data mining nei pacchetti, vedere [Attività Query di data mining](../../integration-services/control-flow/data-mining-query-task.md) e [Soluzioni di data mining](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions).  
  
### <a name="general-options"></a>Opzioni generali  
 **Nome**  
 Consente di specificare un nome univoco per l'attività Query di data mining. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Query di data mining.  
  
### <a name="build-query-tab-options"></a>Opzioni della scheda Compila query  
 **Query di data mining**  
 Consente di digitare una query di data mining.  
  
 **Argomenti correlati:**  [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../../dmx/data-mining-extensions-dmx-reference.md)  
  
 **Compila nuova query**  
 Consente di creare una query di data mining utilizzando uno strumento grafico.  
  
 **Argomenti correlati:** [Query di data mining](../../integration-services/control-flow/data-mining-query.md)  
  
### <a name="parameter-mapping-tab-options"></a>Opzioni della scheda Mapping parametri  
 **Nome parametro**  
 Se lo si desidera, consente di aggiornare il nome del parametro. Eseguire il mapping del parametro a una variabile selezionando una variabile nell'elenco **Nome variabile** .  
  
 **Nome variabile**  
 Consente di selezionare una variabile nell'elenco per mapparla al parametro.  
  
 **Aggiungere**  
 Consente di aggiungere un parametro all'elenco.  
  
 **Rimuovi**  
 Selezionare un parametro e quindi fare clic su **Rimuovi**.  
  
### <a name="result-set-tab-options"></a>Opzioni della scheda Set dei risultati  
 **Nome risultato**  
 Se lo si desidera, consente di aggiornare il nome del set di risultati. Eseguire il mapping del risultato a una variabile selezionando una variabile nell'elenco **Nome variabile** .  
  
 Dopo aver aggiunto un risultato facendo clic su **Aggiungi**, specificare un nome univoco per il risultato.  
  
 **Nome variabile**  
 Consente di selezionare una variabile nell'elenco per mapparla al set dei risultati.  
  
 **Tipo di risultato**  
 Consente di indicare se restituire un singola riga o un set di risultati completo.  
  
 **Aggiungere**  
 Consente di aggiungere il set di risultati all'elenco.  
  
 **Rimuovi**  
 Selezionare un risultato e quindi fare clic su **Rimuovi**.  
## <a name="data-mining-query-task-editor-output-tab"></a>Editor attività Query di data mining (Scheda Output)
  Utilizzare la scheda **Output** della finestra di dialogo **Editor attività Query di data mining** per specificare la destinazione della query di stima.  
  
 Per informazioni sull'implementazione di data mining nei pacchetti, vedere [Attività Query di data mining](../../integration-services/control-flow/data-mining-query-task.md) e [Soluzioni di data mining](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions).  
  
### <a name="general-options"></a>Opzioni generali  
 **Nome**  
 Consente di specificare un nome univoco per l'attività Query di data mining. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Query di data mining.  
  
### <a name="output-tab-options"></a>Opzioni della scheda Output  
 **Connection**  
 Selezionare una gestione connessione nell'elenco oppure fare clic su **Nuova** per creare una nuova gestione connessione.  
  
 **Nuovo**  
 Consente di creare una nuova gestione connessione. È possibile utilizzare solo i tipi di gestione connessione ADO.NET e OLE DB.  
  
 **Tabella di output**  
 Consente di specificare la tabella in cui la query di stima scrive i risultati.  
  
 **Elimina e ricrea tabella di output**  
 Consente di indicare se la query di stima deve sovrascrivere il contenuto nella tabella di destinazione, eliminando e quindi creando di nuovo la tabella.  
  
