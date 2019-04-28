---
title: Attività e procedure relative alle Query di Data Mining | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], how-to topics
ms.assetid: 1bc2a775-6e62-4c66-a53c-201f2ea66295
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cfa2d33d949aad49701e5294329349dc231965db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722853"
---
# <a name="data-mining-query-tasks-and-how-tos"></a>Attività e procedure relative alle query di data mining
  La possibilità di creare query è fondamentale se si utilizzeranno i modelli di data mining. Questa sezione include collegamenti a esempi relativi alla creazione di query rispetto a un modello di data mining mediante gli strumenti disponibili in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per altre informazioni sulle query di data mining o sui diversi tipi di query che è possibile creare, vedere [Query di data mining](data-mining-queries.md).  
  
## <a name="creating-queries-with-prediction-query-builder"></a>Creazione di query con il generatore delle query di stima  
 Il generatore delle query di stima è disponibile sia in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] sia in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] come strumento grafico per la creazione di query rispetto ai modelli di data mining. Negli argomenti seguenti viene illustrato come selezionare un modello, specificare un'origine dati, personalizzare le stime e salvare l'output.  
  
-   [Creare una query di stima usando Generatore di query di stima](create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [Creare una query singleton in Progettazione modelli di data mining](create-a-singleton-query-in-the-data-mining-designer.md)  
  
-   [Creare una query di stima usando Generatore di query di stima](create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [Visualizzare e salvare i risultati di una query di stima](view-and-save-the-results-of-a-prediction-query.md)  
  
-   [Modificare manualmente un query di stima](manually-edit-a-prediction-query.md)  
  
-   [Applicare le funzioni di stima a un modello](apply-prediction-functions-to-a-model.md)  
  
-   [Scegliere ed eseguire il mapping di dati di input per una query di stima](choose-and-map-input-data-for-a-prediction-query.md)  
  
## <a name="using-other-data-mining-query-tools"></a>Utilizzo di altri strumenti di query di data mining  
 Oltre a usare il generatore delle query di stima, è possibile digitare una query direttamente in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tramite DMX o XMLA. È inoltre possibile creare le query di stima a livello di codice e inviarle a un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Negli argomenti seguenti vengono fornite informazioni sulla creazione e utilizzo delle query di stima all'esterno del generatore delle query di stima.  
  
 [Creare una Query di stima Singleton da un modello](create-a-singleton-prediction-query-from-a-template.md)  
 Viene illustrato come usare gli strumenti disponibili in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per creare ed eseguire una query di stima.  
  
 [Creare una query di stima singleton da un modello](create-a-singleton-prediction-query-from-a-template.md)  
 Viene illustrato come usare i modelli disponibili in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per aggiungere parametri a una query di stima.  
  
 [Modificare il valore di timeout per le query di data mining](change-the-time-out-value-for-data-mining-queries.md)  
 Viene illustrato come impostare proprietà nel server per controllare il comportamento correlato alle query di data mining.  
  
 [Creare una query sul contenuto di un modello di data mining](create-a-content-query-on-a-mining-model.md)  
 Viene illustrato come creare query che restituiscono informazioni dettagliate archiviate nel modello di data mining utilizzando i set di righe dello schema di data mining.  
  
 [Creare una query di data mining usando XMLA](create-a-data-mining-query-by-using-xmla.md)  
 Viene illustrato come creare una query sul contenuto del modello di data mining utilizzando i modelli XMLA in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento al linguaggio di query ed espressioni &#40;Analysis Services&#41;](https://msdn.microsoft.com/library/gg492188(SQL.130).aspx)   
 [Stored procedure di data mining &#40;Analysis Services - Data mining&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  
