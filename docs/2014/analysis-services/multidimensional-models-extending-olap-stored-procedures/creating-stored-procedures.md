---
title: Creazione di stored procedure | Microsoft Docs
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
ms.openlocfilehash: 9a997244a2d54cca8732196107dd21927b5f9e2f
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545449"
---
# <a name="creating-stored-procedures"></a>Creazione di stored procedure
  Tutte le stored procedure devono essere associate a una classe CLR (Common Language Runtime) o COM (Component Object Model) per poter essere utilizzate. La classe deve essere installata nel server, in genere sotto forma di libreria di [!INCLUDE[msCoName](../../includes/msconame-md.md)] collegamento dinamico (dll) ActiveX® e registrata come assembly nel server o in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database.  
  
 Le stored procedure vengono registrate in un server o in un database. Le stored procedure del server possono essere chiamate da qualsiasi contesto di query, mentre le stored procedure di database sono accessibili solo se il contesto del database è il database nel quale è stata definita la stored procedure. Se in un assembly sono presenti funzioni che chiamano funzioni di un assembly diverso, è necessario registrare entrambi gli assembly nello stesso contesto (server o database). Per un server o un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database distribuito in un server, è possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per registrare un assembly. Per un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile utilizzare Progettazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per registrare un assembly nel progetto.  
  
> [!IMPORTANT]  
>  Gli assembly COM potrebbero comportare un rischio per la sicurezza. A causa di tale rischio e di altre considerazioni, gli assembly COM sono stati deprecati in [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)] e potrebbero non essere supportati nelle versioni future.  
  
## <a name="registering-a-server-assembly"></a>Registrazione di un assembly server  
 In Esplora oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gli assembly server vengono elencati nella cartella Assembly in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Gli assembly server possono contenere sia assembly .NET (CLR) sia librerie COM.  
  
### <a name="to-create-a-server-assembly"></a>Per creare un assembly server  
  
1.  Espandere l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in Esplora oggetti, fare clic con il pulsante destro del mouse sulla cartella **assembly** , quindi scegliere **nuovo assembly**. Verrà visualizzata la finestra di dialogo **Registra assembly server** .  
  
2.  Per **tipo** specificare il tipo di assembly:  
  
    -   Per una DLL (CLR) con codice gestito, specificare Assembly .NET.  
  
    -   Per una DLL (COM) con codice nativo, specificare DLL COM.  
  
3.  Per **nome file**specificare la DLL contenente le stored procedure.  
  
4.  Per **nome assembly**specificare un nome per l'assembly.  
  
5.  Se si tratta di una build di debug della libreria da utilizzare per eseguire il debug delle stored procedure, selezionare la casella di controllo **Includi informazioni di debug** . Per ulteriori informazioni sul debug di stored procedure, vedere [debug di stored procedure](debugging-stored-procedures.md).  
  
6.  È possibile fare clic su **OK** per registrare l'assembly immediatamente oppure, sulla barra degli strumenti della finestra di dialogo, è possibile fare clic su un comando nel menu **script** per creare uno script per l'azione di registrazione in una finestra di query, in un file o negli Appunti.  
  
 Dopo aver registrato un assembly server, è possibile configurarlo facendo clic con il pulsante destro del mouse sull'assembly in Esplora oggetti e quindi scegliendo **Proprietà**.  
  
## <a name="registering-a-database-assembly-on-the-server"></a>Registrazione di un assembly database nel server  
 In Esplora oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gli assembly database vengono elencati nella cartella Assembly in un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Gli assembly database possono contenere sia assembly .NET (CLR) sia librerie COM.  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>Per creare un assembly database in un server  
  
1.  Espandere l'istanza del [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database in Esplora oggetti, fare clic con il pulsante destro del mouse sulla cartella **assembly** e quindi scegliere **nuovo assembly**. Verrà visualizzata la finestra di dialogo **Registra assembly database** .  
  
2.  Per **tipo** specificare il tipo di assembly:  
  
    -   Per una DLL (CLR) con codice gestito, specificare Assembly .NET.  
  
    -   Per una DLL (COM) con codice nativo, specificare DLL COM.  
  
3.  Per **nome file**specificare la DLL contenente le stored procedure.  
  
4.  Per **nome assembly**specificare un nome per l'assembly.  
  
5.  Se si tratta di una build di debug della libreria da utilizzare per eseguire il debug delle stored procedure, selezionare la casella di controllo **Includi informazioni di debug** . Per ulteriori informazioni sul debug di stored procedure, vedere [debug di stored procedure](debugging-stored-procedures.md).  
  
6.  È possibile fare clic su **OK** per registrare l'assembly immediatamente oppure, sulla barra degli strumenti della finestra di dialogo, è possibile fare clic su un comando nel menu **script** per creare uno script per l'azione di registrazione in una finestra di query, in un file o negli Appunti.  
  
 Dopo aver registrato un assembly del database, è possibile configurarlo facendo clic con il pulsante destro del mouse sull'assembly in Esplora oggetti e quindi scegliendo **Proprietà**.  
  
## <a name="registering-a-database-assembly-in-a-project"></a>Registrazione di un assembly database in un progetto  
 In Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] gli assembly database vengono elencati nella cartella Assembly in un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Gli assembly database possono contenere sia assembly .NET (CLR) sia librerie COM.  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>Per creare un assembly database in un progetto di Analysis Services  
  
1.  Espandere l'istanza del [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database in Esplora oggetti, fare clic con il pulsante destro del mouse sulla cartella **assembly** e quindi scegliere **nuovo riferimento ad assembly**. Verrà visualizzata la finestra di dialogo **Aggiungi riferimento** . Nella scheda **.NET** della finestra di dialogo **Aggiungi riferimento** sono elencati gli assembly .NET (CLR) esistenti, mentre nella scheda **progetti** sono elencati i progetti.  
  
2.  È possibile fare clic su un componente o un progetto esistente e quindi fare clic su **Aggiungi** per aggiungerlo al [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto. Per aggiungere un riferimento a una DLL COM, fare clic sulla scheda **Sfoglia** per individuare il file. Nell'elenco **progetti e componenti selezionati** vengono visualizzati il nome, il tipo, la versione e il percorso di ogni componente aggiunto al progetto.  
  
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
  
  
