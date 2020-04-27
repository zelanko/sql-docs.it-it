---
title: Debug di stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- debugging stored procedures [Analysis Services]
- stored procedures [Analysis Services], debugging
ms.assetid: 34f51b85-02b3-40dd-bf93-375a9e522385
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90b72b0e60550b0b6bdf89e0ba39e6089c5d8de2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727747"
---
# <a name="debugging-stored-procedures"></a>Debug di stored procedure
  Le stored procedure di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in realtà sono librerie CLR o COM, in genere DLL, scritte in C# o qualsiasi altro linguaggio CLR o COM. Pertanto, il debug di una stored procedure è molto simile al debug di qualsiasi altra applicazione nell'ambiente di debug di Visual Studio. Per eseguire il debug di una stored procedure nell'ambiente di sviluppo di Visual Studio vengono utilizzate le funzioni di debug integrate, che consentono di arrestare l'esecuzione in corrispondenza delle posizioni delle procedure, controllare la memoria e registrare valori, modificare variabili, osservare i messaggi visualizzati e analizzare in dettaglio il funzionamento del codice.  
  
### <a name="to-debug-a-stored-procedure"></a>Per eseguire il debug di una stored procedure  
  
1.  Aprire il progetto utilizzato per creare la DLL in Visual Studio.  
  
2.  Impostare punti di interruzione nel metodo o nella funzione corrispondente alla procedura di cui si desidera eseguire il debug.  
  
3.  Utilizzare Visual Studio per creare una build di debug di una DLL di stored procedure.  
  
4.  Distribuire la DLL nel server. Per ulteriori informazioni sulla distribuzione della DLL nel server, vedere [creazione di stored procedure](creating-stored-procedures.md).  
  
5.  La stored procedure di cui si desidera eseguire il debug deve essere chiamata da un'applicazione. Se non esiste un'applicazione utilizzabile a tale scopo, è possibile utilizzare l'Editor di query MDX in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per creare una query MDX che chiami la stored procedure desiderata.  
  
6.  In Visual Studio connettersi al processo di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (Msmdsrv.exe).  
  
    1.  Scegliere **Connetti toProcess**dal menu **debug** .  
  
    2.  Nella finestra di dialogo **Connetti toProcess** selezionare **Mostra i processi di tutti gli utenti**.  
  
    3.  Nell'elenco **processi disponibili** , nella colonna **processo** , fare clic su **msmdsrv. exe**. Se le istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione nel server sono più di una, è necessario identificare il processo specificando l'ID dell'istanza che si desidera utilizzare.  
  
    4.  Nella casella **di testo Connetti a** verificare che sia selezionato il tipo di programma appropriato. Per una DLL CLR, fare clic su **Seleziona**, quindi su **Esegui il debug di questi tipi di codice**, quindi su **gestito**e infine su **OK**. Per una DLL COM, fare clic su **Seleziona**, quindi su **Esegui il debug di questi tipi di codice**, quindi su **nativo**e infine su **OK**.  
  
    5.  Scegliere **Connetti**.  
  
7.  In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] richiamare il programma o lo script MDX che chiama la stored procedure. Il debugger interrompe l'esecuzione quando raggiunge una riga contenente un punto di interruzione. È possibile valutare variabili nella finestra Espressione di controllo, visualizzare variabili locali ed eseguire il codice un'istruzione alla volta.  
  
 In caso di problemi durante il debug di una libreria, verificare che il file del database di programma (PDB) corrispondente sia stato copiato nel percorso di distribuzione nel server. Se questo file non è stato copiato durante la registrazione o la distribuzione, è necessario copiarlo manualmente nello stesso percorso della DLL. Per il codice nativo (DLL COM), il file PDB si trova nella sottodirectory \debug. Per il codice gestito (DLL CLR), si trova nella sottodirectory \WINDEBUG.  
  
## <a name="see-also"></a>Vedi anche  
 [Gestione di assembly di modelli multidimensionali](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definizione delle stored procedure](defining-stored-procedures.md)  
  
  
