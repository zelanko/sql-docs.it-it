---
title: Debug di Stored procedure | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d37eebfad3f8a3e89dc65ad9602f4b5d61b5072e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68181144"
---
# <a name="debugging-stored-procedures"></a>Debug di stored procedure
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Le stored procedure di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in realtà sono librerie CLR o COM, in genere DLL, scritte in C# o qualsiasi altro linguaggio CLR o COM. Pertanto, il debug di una stored procedure è molto simile al debug di qualsiasi altra applicazione nell'ambiente di debug di Visual Studio. Per eseguire il debug di una stored procedure nell'ambiente di sviluppo di Visual Studio vengono utilizzate le funzioni di debug integrate, che consentono di arrestare l'esecuzione in corrispondenza delle posizioni delle procedure, controllare la memoria e registrare valori, modificare variabili, osservare i messaggi visualizzati e analizzare in dettaglio il funzionamento del codice.  
  
### <a name="to-debug-a-stored-procedure"></a>Per eseguire il debug di una stored procedure  
  
1.  Aprire il progetto utilizzato per creare la DLL in Visual Studio.  
  
2.  Impostare punti di interruzione nel metodo o nella funzione corrispondente alla procedura di cui si desidera eseguire il debug.  
  
3.  Utilizzare Visual Studio per creare una build di debug di una DLL di stored procedure.  
  
4.  Distribuire la DLL nel server. Per altre informazioni sulla distribuzione della DLL per il server, vedere [creazione di Stored procedure](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md).  
  
5.  La stored procedure di cui si desidera eseguire il debug deve essere chiamata da un'applicazione. Se non esiste un'applicazione utilizzabile a tale scopo, è possibile utilizzare l'Editor di query MDX in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per creare una query MDX che chiami la stored procedure desiderata.  
  
6.  In Visual Studio connettersi al processo di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (Msmdsrv.exe).  
  
    1.  Dal **Debug** menu, scegliere **toProcess Connetti**.  
  
    2.  Nel **Connetti toProcess** finestra di dialogo **Mostra i processi di tutti gli utenti**.  
  
    3.  Nel **processi disponibili** elenco le **processo** colonna, fare clic su **Msmdsrv.exe**. Se le istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione nel server sono più di una, è necessario identificare il processo specificando l'ID dell'istanza che si desidera utilizzare.  
  
    4.  Nel **Collega a** testo, assicurarsi che sia selezionato il tipo di programma appropriato. Per una DLL CLR, fare clic su **selezionate**, quindi fare clic su **eseguire il Debug di questi tipi di codice**, quindi fare clic su **gestito**, quindi fare clic su **OK**. Per una DLL COM, fare clic su **selezionate**, quindi fare clic su **eseguire il Debug di questi tipi di codice**, quindi fare clic su **Native**, quindi fare clic su **OK**.  
  
    5.  Fare clic su **collegare**.  
  
7.  In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] richiamare il programma o lo script MDX che chiama la stored procedure. Il debugger interrompe l'esecuzione quando raggiunge una riga contenente un punto di interruzione. È possibile valutare variabili nella finestra Espressione di controllo, visualizzare variabili locali ed eseguire il codice un'istruzione alla volta.  
  
 In caso di problemi durante il debug di una libreria, verificare che il file del database di programma (PDB) corrispondente sia stato copiato nel percorso di distribuzione nel server. Se questo file non è stato copiato durante la registrazione o la distribuzione, è necessario copiarlo manualmente nello stesso percorso della DLL. Per il codice nativo (DLL COM), il file PDB si trova nella sottodirectory \debug. Per il codice gestito (DLL CLR), si trova nella sottodirectory \WINDEBUG.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di assembly di modelli multidimensionali](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definizione delle stored procedure](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
