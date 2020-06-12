---
title: Importazione di un progetto di data mining utilizzando l'importazione guidata Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 62bc9fc5-c6ff-4517-b598-d92df76743a2
author: minewiskan
ms.author: owend
ms.openlocfilehash: 63034ac9d8ba601070f716830b3b9173575a8775
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522333"
---
# <a name="import-a-data-mining-project-using-the-analysis-services-import-wizard"></a>Importare un progetto di data mining utilizzando l'Importazione guidata di Analysis Services
  In questo argomento viene descritto come creare un nuovo progetto di data mining importando i metadati da un progetto di data mining esistente in un altro server, usando il modello **Importa da server (multidimensionale e data mining)** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="import-data-sources-mining-structures-and-mining-models-from-an-existing-data-mining-project"></a>Importare origini dati, strutture e modelli di data mining da un progetto di data mining esistente  
 Quando si utilizza il modello, **Importa da server (multidimensionale e data mining)**, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Crea un nuovo progetto di data mining, quindi copia i metadati dal progetto data mining specificato. Il nuovo progetto contiene le stesse origini dati, viste origine dati, strutture e modelli di data mining del database di ssASnoversion da cui è stata effettuata l'importazione. Tuttavia, non è possibile utilizzare il progetto finché non sono state aggiornate alcune proprietà e non sono stati elaborati gli oggetti come descritto:  
  
-   I dati non vengono copiati dal server di origine al nuovo progetto data mining. vengono importate solo le definizioni delle origini dati e le viste origine dati. Pertanto, al completamento del processo di importazione e dopo la creazione degli oggetti, è necessario popolare gli oggetti con i dati eseguendo il training delle strutture di data mining e dei modelli dipendenti. Per eseguire il training dei modelli e delle strutture, è possibile utilizzare il comando **Elabora tutto** di Progettazione modelli di data mining.  
  
-   Se si importa un progetto creato in una versione precedente di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], l'origine dati potrebbe utilizzare provider che non sono installati nel server nel quale si importa il progetto. Se si riscontrano errori durante l'elaborazione delle strutture di data mining importate, fare clic con il pulsante destro del mouse su ogni origine dati e selezionare **Apri finestra di progettazione** per modificare la stringa di connessione e rivedere le proprietà del provider.  
  
     Potrebbe inoltre essere necessario verificare che l'account utilizzato per elaborare gli oggetti di data mining o i modelli di data mining di query disponga delle autorizzazioni necessarie sull'origine dati.  
  
-   Per impostazione predefinita, quando si importa un progetto, il database dell'area di lavoro viene impostato su localhost o qualsiasi istanza predefinita configurata come **Server di destinazione predefinito** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per impostare questa proprietà, scegliere **Finestre di progettazione Business Intelligence** dal menu **Opzioni**, selezionare **Analysis Services**, quindi **Generale**.  
  
     Si noti che in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]è disponibile un'altra opzione separata che è possibile impostare per configurare il server di distribuzione predefinito per i progetti di modello tabulare di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . L'impostazione **Server di distribuzione predefinito**determina il database dell'area di lavoro predefinito per i progetti di modello tabulare. Non è possibile utilizzare istanze che supportano i modelli tabulari per i progetti di data mining  
  
     Se non è possibile modificare il database di distribuzione predefinito per utilizzare un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione in modalità multidimensionale o di data mining, è sempre possibile specificare il database di distribuzione tramite la finestra di dialogo **Proprietà progetto** .  
  
#### <a name="to-create-a-new-data-mining-project-by-importing-an-existing-data-mining-project"></a>Per creare un nuovo progetto di data mining importando un progetto di data mining esistente  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
2.  In **Modelli installati** nella finestra di dialogo **Nuovo progetto**fare clic su **Business Intelligence**, fare clic su **Analysis Services**e quindi su **Importa da server (multidimensionale e data mining)**.  
  
3.  In **Nome**digitare un nome per il progetto, quindi specificare un percorso e un nome per la soluzione e scegliere **OK**.  
  
     Verrà avviata l' **Importazione guidata database di Analysis Services** . Fare clic su OK nella pagina introduttiva per continuare.  
  
4.  Nella pagina **Seleziona database di origine**per **Server**specificare l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che contiene la soluzione da importare.  
  
     Per **Database**scegliere il database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contenente i dati e gli oggetti di data mining da importare.  
  
    > [!WARNING]  
    >  Non è possibile specificare gli oggetti da importare; quando si sceglie un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente, vengono importati tutti gli oggetti multidimensionali e di data mining.  
  
     Fare clic su **Avanti**.  
  
5.  Nella pagina **Completamento procedura guidata**viene visualizzato lo stato di avanzamento dell'operazione di importazione. Non è possibile annullare l'operazione o modificare gli oggetti importati. Fare clic su **Fine** al termine.  
  
     Il nuovo progetto viene aperto automaticamente tramite [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà del progetto &#40;SSAS tabulare&#41;](../tabular-models/properties-ssas-tabular.md)  
  
  
