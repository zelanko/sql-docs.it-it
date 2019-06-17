---
title: Creazione di Stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- registering assemblies
- database assemblies [Analysis Services]
- server assemblies [Analysis Services]
- stored procedures [Analysis Services], creating
- assemblies [Analysis Services]
ms.assetid: a12ff02f-6d0b-4488-9846-3609fc0d0554
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7beb77adf595b055a6c1e4a7543b428a06ce7640
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62703083"
---
# <a name="creating-stored-procedures"></a>Creazione di stored procedure
  Tutte le stored procedure devono essere associate a una classe CLR (Common Language Runtime) o COM (Component Object Model) per poter essere utilizzate. La classe deve essere installata nel server, in genere sotto forma di una [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® dynamic link library (DLL) - e registrato come un assembly nel server o in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database.  
  
 Le stored procedure vengono registrate in un server o in un database. Le stored procedure del server possono essere chiamate da qualsiasi contesto di query, mentre le stored procedure di database sono accessibili solo se il contesto del database è il database nel quale è stata definita la stored procedure. Se in un assembly sono presenti funzioni che chiamano funzioni di un assembly diverso, è necessario registrare entrambi gli assembly nello stesso contesto (server o database). Per un server o un distribuito [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database in un server, è possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per registrare un assembly. Per un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile utilizzare Progettazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per registrare un assembly nel progetto.  
  
> [!IMPORTANT]  
>  Gli assembly COM potrebbero comportare un rischio per la sicurezza. A causa di tale rischio e di altre considerazioni, gli assembly COM sono stati deprecati in [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)] e potrebbero non essere supportati nelle versioni future.  
  
## <a name="registering-a-server-assembly"></a>Registrazione di un assembly server  
 In Esplora oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gli assembly server vengono elencati nella cartella Assembly in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Gli assembly server possono contenere sia assembly .NET (CLR) sia librerie COM.  
  
### <a name="to-create-a-server-assembly"></a>Per creare un assembly server  
  
1.  Espandere l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in Esplora oggetti fare doppio clic il **assembly** cartella e quindi fare clic su **nuovo Assembly**. Ciò consente di visualizzare il **registra Assembly Server** nella finestra di dialogo.  
  
2.  Per la **tipo** specificare il tipo dell'assembly:  
  
    -   Per una DLL (CLR) con codice gestito, specificare Assembly .NET.  
  
    -   Per una DLL (COM) con codice nativo, specificare DLL COM.  
  
3.  Per la **nome del File**, specificare la DLL che contiene le stored procedure.  
  
4.  Per la **nome dell'Assembly**, specificare un nome per l'assembly.  
  
5.  Se si tratta di una build di debug della libreria che si intende usare per il debug di stored procedure, selezionare la **Includi informazioni di debug** casella di controllo. Per altre informazioni sul debug delle stored procedure, vedere [debug di Stored procedure](debugging-stored-procedures.md).  
  
6.  È possibile fare clic su **OK** per registrare l'assembly immediatamente oppure sulla barra degli strumenti finestra di dialogo, è possibile fare clic su un comando sulle **Script** menu per creare uno script di azione di registrazione in una finestra di query, un file o negli Appunti.  
  
 Dopo aver registrato un assembly di server, è possibile configurarlo facendo l'assembly in Esplora oggetti e scegliendo **proprietà**.  
  
## <a name="registering-a-database-assembly-on-the-server"></a>Registrazione di un assembly database nel server  
 In Esplora oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gli assembly database vengono elencati nella cartella Assembly in un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Gli assembly database possono contenere sia assembly .NET (CLR) sia librerie COM.  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>Per creare un assembly database in un server  
  
1.  Espandere l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in Esplora oggetti di database, fare doppio clic sui **assembly** cartella e quindi fare clic su **nuovo Assembly**. Ciò consente di visualizzare il **registra Assembly Database** nella finestra di dialogo.  
  
2.  Per la **tipo** specificare il tipo dell'assembly:  
  
    -   Per una DLL (CLR) con codice gestito, specificare Assembly .NET.  
  
    -   Per una DLL (COM) con codice nativo, specificare DLL COM.  
  
3.  Per la **nome del File**, specificare la DLL che contiene le stored procedure.  
  
4.  Per la **nome dell'Assembly**, specificare un nome per l'assembly.  
  
5.  Se si tratta di una build di debug della libreria che si intende usare per il debug di stored procedure, selezionare la **Includi informazioni di debug** casella di controllo. Per altre informazioni sul debug delle stored procedure, vedere [debug di Stored procedure](debugging-stored-procedures.md).  
  
6.  È possibile fare clic su **OK** per registrare l'assembly immediatamente oppure sulla barra degli strumenti finestra di dialogo, è possibile fare clic su un comando sulle **Script** menu per creare uno script di azione di registrazione in una finestra di query, un file o negli Appunti.  
  
 Dopo aver registrato un assembly database, è possibile configurarlo facendo l'assembly in Esplora oggetti e scegliendo **proprietà**.  
  
## <a name="registering-a-database-assembly-in-a-project"></a>Registrazione di un assembly database in un progetto  
 In Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] gli assembly database vengono elencati nella cartella Assembly in un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Gli assembly database possono contenere sia assembly .NET (CLR) sia librerie COM.  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>Per creare un assembly database in un progetto di Analysis Services  
  
1.  Espandere l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in Esplora oggetti di database, fare doppio clic sui **assembly** cartella e quindi fare clic su **nuovo riferimento ad Assembly**. Ciò consente di visualizzare il **Aggiungi riferimento** nella finestra di dialogo. Il **.NET** scheda della finestra di **Aggiungi riferimento** nella finestra di dialogo vengono elencati gli assembly .NET (CLR) esistenti, mentre il **progetti** scheda vengono elencati i progetti.  
  
2.  È possibile fare clic su un componente esistente o un progetto e quindi fare clic su **Add** deve essere aggiunto il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto. Per aggiungere un riferimento a una DLL COM, scegliere il **Sfoglia** pressione di tab per trovare il file. Il **progetti e componenti selezionati** elenco Mostra il nome, tipo, versione e percorso di ogni componente che si sta aggiungendo al progetto.  
  
3.  Al termine della selezione dei componenti da aggiungere, fare clic su **OK** per aggiungerli al [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto.  
  
## <a name="script-format-for-an-assembly"></a>Formatto dello script di un assembly  
 Registrare un assembly .NET è un'operazione piuttosto semplice. Per aggiungere un assembly .NET a un database in formato binario è possibile utilizzare il formato seguente:  
  
```  
<Create>  
   <ObjectDefinition>  
      <Assembly>  
         <Files>  
            <File>  
               <Name>filename</Name>  
               <Type>filetype</Type>  
               <Data>  
                  <Block>binarydatablock</Block>  
                  <Block>binarydatablock</Block>  
                  ...  
               </Data>  
            </File>  
         </Files>  
         <PermissionSet>PermissionSet</PermissionSet>  
      </Assembly>  
   <ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di assembly di modelli multidimensionali](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definizione delle stored procedure](defining-stored-procedures.md)  
  
  
