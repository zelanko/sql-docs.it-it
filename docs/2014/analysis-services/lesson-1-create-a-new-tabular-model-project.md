---
title: 'Lezione 1: creare un nuovo progetto di modello tabulare | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fb9ca011cdbbe32ebd6c71cb9ca64967cfbccb9e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079312"
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>Lezione 1: Creare un nuovo modello di progetto tabulare
  In questa lezione verrà creato un nuovo progetto di modello tabulare in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Una volta creato il nuovo progetto, è possibile iniziare ad aggiungere dati tramite l'Importazione guidata tabella. Oltre alla creazione di un nuovo progetto, questa lezione include anche una breve introduzione all'ambiente di creazione di modelli tabulari in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
 Per altre informazioni sui diversi tipi di progetti di modelli tabulari, vedere [Progetti di modello tabulare &#40;SSAS tabulare&#41;](tabular-models/tabular-model-projects-ssas-tabular.md). Per ulteriori informazioni sull'ambiente di creazione di modelli tabulari, vedere [progettazione di modelli tabulari &#40;SSAS tabulare&#41;](tabular-model-designer-ssas-tabular.md).  
  
 Tempo previsto per il completamento della lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisites  
 Questo argomento è la prima lezione dell'esercitazione per la creazione di un modello tabulare. Per completare questa lezione, è necessario avere installato il database AdventureWorksDW in un'istanza di SQL Server. Per altre informazioni, vedere [Modellazione tabulare &#40;esercitazione di AdventureWorks&#41;](tabular-modeling-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Creare un nuovo modello di progetto tabulare  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Per creare un nuovo progetto di modello tabulare  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
2.  Nella finestra di dialogo **nuovo progetto** , in **modelli installati**, fare clic su **Business Intelligence**, quindi fare clic su **Analysis Services**, quindi su **Analysis Services progetto tabulare**.  
  
3.  In **nome**Digitare `AW Internet Sales Tabular Model`, quindi specificare un percorso per i file di progetto.  
  
     Per impostazione predefinita, in **Nome soluzione** sarà indicato lo stesso nome del progetto, ma è possibile digitare un nome diverso per la soluzione.  
  
4.  Fare clic su **OK**.  
  
## <a name="understanding-the-sql-server-data-tools-tabular-model-authoring-environment"></a>Informazioni sull'ambiente di creazione di modelli tabulari per SQL Server Data Tools  
 Ora che è stato creato un nuovo progetto di modello tabulare, è necessario esaminare l'ambiente di creazione di modelli tabulari in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] (Visual Studio 2010 o versione successiva).  
  
 Dopo essere stato creato, il progetto verrà visualizzato in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. In Progettazione modelli verrà visualizzato un modello vuoto e il file **Model.bim** verrà selezionato nella finestra **Esplora soluzioni** . Quando si aggiungono dati, nella finestra di progettazione vengono visualizzate tabelle e colonne. Se la finestra di progettazione, ovvero la finestra vuota con la scheda Model. BIM, non viene **** visualizzata, in `AW Internet Sales Tabular Model`Esplora soluzioni in fare doppio clic sul file **Model. BIM** .  
  
 Nella finestra **Proprietà** è possibile visualizzare le proprietà di base del progetto. In **Esplora soluzioni**fare clic `AW Internet Sales Tabular Model`su. Si noti che nella finestra **Proprietà** , in **File di progetto**, viene visualizzato **AW Internet Sales Tabular Model.smproj**. Si tratta del nome del file di progetto, mentre in **Cartella di progetto**viene visualizzato il percorso specifico del file di progetto.  
  
 In **Esplora soluzioni**fare clic con il pulsante `AW Internet Sales Tabular Model` destro del mouse sul progetto, quindi scegliere **proprietà**. Verrà visualizzata la finestra di dialogo **Pagine delle proprietà di AW Internet Sales Tabular Model** (Pagine delle proprietà di AW Internet Sales Tabular Model). Queste sono le proprietà avanzate del progetto. Più avanti, prima di distribuire il modello, verranno impostate alcune di queste proprietà.  
  
 Verranno ora esaminate le proprietà del modello. In **Esplora soluzioni**fare clic su **Model.bim**. Nella finestra **Proprietà** verranno visualizzate le proprietà del modello, la più importante delle quali è la proprietà **Modalità DirectQuery** . Questa proprietà specifica se il modello viene distribuito in modalità In-Memory (Disattivata) o in modalità DirectQuery (Attivata). Per questa esercitazione, il modello verrà creato e distribuito in modalità In-Memory.  
  
 Quando si crea un nuovo modello, determinate proprietà del modello vengono impostate automaticamente in base alle impostazioni di Modellazione dati che è possibile specificare nella finestra di dialogo Strumenti\Opzioni. Le proprietà Backup dei dati, Memorizzazione area di lavoro e Server dell'area di lavoro specificano come e dove viene eseguito il backup, viene mantenuto in memoria e viene creato il database dell'area di lavoro, ovvero il database per la creazione del modello. È possibile modificare queste impostazioni in un secondo momento, se necessario, ma per ora, lasciarle come sono.  
  
 Con l'installazione di [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]vengono aggiunte nuove voci di menu all'ambiente di Visual Studio. Verranno ora esaminate le nuove voci di menu specifiche per la creazione di modelli tabulari. Fare clic sul menu **Modello**. Da questa posizione è possibile avviare l'Importazione guidata tabella, visualizzare e modificare le connessioni esistenti, aggiornare i dati dell'area di lavoro, esplorare il modello in [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel utilizzando la funzionalità Analizza in Excel, creare prospettive e ruoli, selezionare la vista del modello e impostare opzioni di calcolo.  
  
 Fare clic sul menu **Tabella**. Da questa posizione è possibile creare e gestire relazioni tra tabelle, creare, gestire e specificare impostazioni della tabella data, creare partizioni e modificare proprietà della tabella.  
  
 Fare clic sul menu **Colonna** . Da questa posizione è possibile aggiungere ed eliminare colonne in una tabella, bloccare colonne e specificare un ordinamento. È inoltre possibile utilizzare la funzionalità Somma automatica per creare una misura di aggregazione standard per una colonna selezionata. Con gli altri pulsanti della barra degli strumenti è possibile accedere rapidamente ai comandi e alle funzioni usati di frequente.  
  
 Esplorare alcune delle finestre di dialogo e individuare le posizioni delle varie funzionalità specifiche per la creazione di modelli tabulari. Anche se alcune voci di menu o opzioni non sono ancora attive, è così possibile acquisire familiarità con l'ambiente per la creazione di modelli tabulari.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 2: Aggiungere dati](lesson-2-add-data.md).  
  
  
