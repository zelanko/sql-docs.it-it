---
title: Attività Query di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingquerytask.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 93021fb7000bd7adccd467e04fb7cf3430db5efe
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84919472"
---
# <a name="data-mining-query-task"></a>Attività Query di data mining
  L'attività Query di data mining consente di eseguire query di stima basate sui modelli di data mining compilati in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Una query di stima genera una stima per nuovi dati utilizzando modelli di data mining. È ad esempio possibile utilizzare una query di stima per stimare il numero di barche a vela che si prevede di vendere durante i mesi estivi o per generare un elenco dei potenziali clienti che probabilmente acquisteranno una barca a vela.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornisce attività che consentono di eseguire altre operazioni di Business Intelligence, quali l'esecuzione di istruzioni DDL (Data Definition Language) e l'elaborazione di oggetti di analisi.  
  
 Per ulteriori informazioni su altre attività di Business Intelligence, fare clic su uno degli argomenti seguenti:  
  
-   [Attività Esegui DDL Analysis Services](analysis-services-execute-ddl-task.md)  
  
-   [Attività Elaborazione Analysis Services](analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>Query di stima  
 La query è un'istruzione DMX (Data Mining Extensions). Il linguaggio DMX è un'estensione del linguaggio SQL che consente di supportare l'utilizzo dei modelli di data mining. Per altre informazioni su come usare il linguaggio DMX, vedere [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-reference).  
  
 L'attività consente di eseguire query su più modelli di data mining compilati in base alla stessa struttura di data mining. Per compilare un modello di data mining è necessario usare uno degli algoritmi di data mining disponibili in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La struttura di data mining a cui fa riferimento l'attività Query di data mining può includere più modelli di data mining, compilati utilizzando algoritmi diversi. Per altre informazioni, vedere [Strutture di data mining &#40;Analysis Services – Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-structures-analysis-services-data-mining) e [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining).  
  
 La query di stima eseguita dall'attività Query di data mining restituisce un risultato costituito da una singola riga o da un set di dati. Una query che restituisce una singola riga è detta query singleton. La query per la stima del numero di barche a vela che si prevede di vendere nei mesi estivi, ad esempio, restituisce un numero. Per ulteriori informazioni sulle query di stima che restituiscono una singola riga, vedere [interfacce di query di data mining](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools).  
  
 I risultati delle query vengono salvati in tabelle. Se esiste già una tabella con il nome specificato dall'attività Query di data mining, l'attività può creare una nuova tabella con lo stesso nome, a cui viene aggiunto un numero, oppure sovrascrivere il contenuto della tabella.  
  
 Se il set di risultati è nidificato, verrà convertito in formato flat prima del salvataggio. La conversione in formato flat trasforma un set di risultati nidificato in una tabella. Se ad esempio si converte in formato flat un set di risultati annidato che include una colonna di nome **Customer** e una colonna annidata di nome **Product** , alla colonna **Customer** verranno aggiunte le righe necessarie per ottenere una tabella che include dati sui prodotti per ogni cliente. Per un cliente con tre prodotti diversi, ad esempio, si ottiene una tabella con tre righe, ognuna delle quali contiene il nome del cliente ripetuto e un nome di prodotto diverso. Se la parola chiave FLATTENED viene omessa, la tabella conterrà solo la colonna **Customer** e una sola riga per cliente. Per altre informazioni, vedere [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
## <a name="configuration-of-the-data-mining-query-task"></a>Configurazione dell'attività Query di data mining  
 Per l'attività Query di data mining sono necessarie due connessioni. La prima è una gestione connessione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che stabilisce la connessione a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contenente la struttura e il modello di data mining. La seconda è una gestione connessione OLE DB che stabilisce la connessione al database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contenente la tabella in cui l'attività scrive i dati. Per altre informazioni, vedere [Gestione connessione Analysis Services](../connection-manager/analysis-services-connection-manager.md) e [Gestione connessione OLE DB](../connection-manager/ole-db-connection-manager.md).  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Query di data mining &#40;scheda Modello di data mining&#41;](../data-mining-query-task-editor-mining-model-tab.md)  
  
-   [Editor attività Query di data mining &#40;scheda Query&#41;](../data-mining-query-task-editor-query-tab.md)  
  
-   [Editor attività Query di data mining &#40;scheda Output&#41;](../data-mining-query-task-editor-output-tab.md)  
  
> [!NOTE]  
>  L'Editor attività Query di data mining non include la pagina Espressioni. È tuttavia possibile usare la finestra **Proprietà** per accedere agli strumenti per la creazione e la gestione di espressioni di proprietà per le proprietà dell'attività Query di data mining.  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>Configurazione a livello di codice dell'attività Query di data mining  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
  
