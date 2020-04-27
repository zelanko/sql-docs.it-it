---
title: Accesso ai dati PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 83dc82da-91fb-4e47-91a8-0e0db67339b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97f5d2045601f72c3536fbf2d4e469eb5eb20fbe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071248"
---
# <a name="powerpivot-data-access"></a>Accesso ai dati PowerPivot
  In questo argomento viene illustrata la modalità in cui i dati vengono recuperati da una cartella di lavoro di PowerPivot pubblicata in una raccolta di SharePoint.  
  
 I dati PowerPivot vengono archiviati in una cartella di lavoro di Excel. La stringa di connessione è un URL di una cartella di lavoro in un sito di SharePoint.  
  
 I dati PowerPivot vengono spesso utilizzati dalla cartella di lavoro che li contiene, come i dati sottostanti le tabelle pivot e i grafici pivot. In alternativa, è inoltre possibile utilizzare i dati PowerPivot come origine dati esterna, in cui una cartella di lavoro, un dashboard o un report si connette a un file di Excel (con estensione xlsx) separato in SharePoint e recupera i dati per l'utilizzo successivo. Gli strumenti client che in genere utilizzano dati PowerPivot sono Excel, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], altri report Reporting Services e PerformancePoint.  
  
 Sul desktop il componente aggiuntivo di PowerPivot utilizza AMO e ADOMD.NET per creare, elaborare ed eseguire una query sui dati PowerPivot nell'area di lavoro client.  
  
 In una farm di SharePoint, in Excel Services viene utilizzato il provider OLE DB MSOLAP locale per connettersi ai dati PowerPivot. La richiesta di connessione viene inviata dal provider a un server PowerPivot per SharePoint nella farm. In tale server vengono caricati i dati, viene eseguita la query e viene restituito il set di risultati.  
  
##  <a name="querying-powerpivot-data-in-sharepoint"></a><a name="queryproc"></a>Esecuzione di query sui dati PowerPivot in SharePoint  
 Quando si visualizza una cartella di lavoro di PowerPivot da una raccolta di SharePoint, i dati PowerPivot all'interno della cartella di lavoro vengono rilevati, estratti ed elaborati separatamente nelle istanze del server Analysis Services all'interno della farm, mentre Excel Services esegue il rendering del livello presentazione. È possibile visualizzare la cartella di lavoro completamente elaborata in una finestra del browser o in un'applicazione desktop di Excel 2010 che dispone del componente aggiuntivo di PowerPivot.  
  
 Nel diagramma seguente viene illustrato come una richiesta di elaborazione query viene spostata all'interno della farm. Poiché i dati PowerPivot fanno parte di una cartella di lavoro di Excel 2010, si verifica una richiesta di elaborazione query quando un utente apre una cartella di lavoro di Excel da una raccolta di SharePoint e interagisce con una tabella o un grafico pivot che contiene dati PowerPivot.  
  
 ![GMNI_DataProcReq](../media/gmni-dataprocreq.gif "GMNI_DataProcReq")  
  
 I componenti di PowerPivot per SharePoint ed Excel Services elaborano parti diverse dello stesso file (con estensione xlsx) della cartella di lavoro. Tramite Excel Services viene rilevata l'elaborazione di richieste e dati PowerPivot da un server PowerPivot nella farm. La richiesta viene allocata a un'istanza di [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] che consente di estrarre i dati dalla cartella di lavoro nella raccolta contenuto e di caricare i dati. I dati archiviati in memoria vengono uniti nuovamente nella cartella di lavoro di cui è stato eseguito il rendering e passati nuovamente a Excel Web Access per la presentazione in una finestra del browser.  
  
 Non tutti i dati in una cartella di lavoro di PowerPivot vengono gestiti da PowerPivot per SharePoint. Tramite Excel Services vengono elaborati i dati di celle e tabelle in un foglio di lavoro. Solo le tabelle e i grafici pivot e i sezionamenti che non risultano allineati ai dati PowerPivot vengono gestiti da PowerPivot per SharePoint.  
  
## <a name="see-also"></a>Vedi anche  
 [Connetti a Analysis Services](../instances/connect-to-analysis-services.md)   
 [Accesso ai dati di modello tabulare](../tabular-models/tabular-model-data-access.md)  
  
  
