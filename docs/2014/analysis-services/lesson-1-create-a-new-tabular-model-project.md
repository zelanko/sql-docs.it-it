---
title: 'Lezione 1: Creare un nuovo progetto di modello tabulare | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d7ab0a864d99e3cade96b7715adf7d307ca355c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729467"
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>Lezione 1: Creare un nuovo modello di progetto tabulare
  In questa lezione verrà creato un nuovo progetto di modello tabulare in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Una volta creato il nuovo progetto, è possibile iniziare ad aggiungere dati tramite l'Importazione guidata tabella. Oltre alla creazione di un nuovo progetto, questa lezione include anche una breve introduzione all'ambiente di creazione di modelli tabulari in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
 Per altre informazioni sui diversi tipi di progetti di modelli tabulari, vedere [Progetti di modello tabulare &#40;SSAS tabulare&#41;](tabular-models/tabular-model-projects-ssas-tabular.md). Per altre informazioni sull'ambiente di creazione di modelli tabulari, vedere [progettazione di modelli tabulari &#40;modello tabulare di SSAS&#41;](tabular-model-designer-ssas-tabular.md).  
  
 Tempo stimato per il completamento della lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento è la prima lezione di un'esercitazione sulla creazione di modelli tabulari. Per completare questa lezione, è necessario avere installato il database AdventureWorksDW in un'istanza di SQL Server. Per altre informazioni, vedere [Modellazione tabulare &#40;esercitazione di AdventureWorks&#41;](tabular-modeling-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Creare un nuovo modello di progetto tabulare  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Per creare un nuovo modello di progetto tabulare  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
2.  Nel **nuovo progetto** nella finestra di dialogo **modelli installati**, fare clic su **Business Intelligence**, quindi fare clic su **Analysis Services**, e quindi fare clic su **progetto tabulare di Analysis Services**.  
  
3.  Nelle **Name**, tipo `AW Internet Sales Tabular Model`, quindi specificare un percorso per i file di progetto.  
  
     Per impostazione predefinita, **Nome soluzione** corrisponde al nome del progetto. È tuttavia possibile digitare un nome diverso per la soluzione.  
  
4.  Fare clic su **OK**.  
  
## <a name="understanding-the-sql-server-data-tools-tabular-model-authoring-environment"></a>Informazioni sull'ambiente di creazione di modelli tabulari per SQL Server Data Tools  
 Ora che è stato creato un nuovo progetto di modello tabulare, verrà analizzato l'ambiente di creazione di modelli tabulari [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] (Visual Studio 2010 o versione successiva).  
  
 Dopo essere stato creato, il progetto verrà visualizzato in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. In Progettazione modelli verrà visualizzato un modello vuoto e il file **Model.bim** verrà selezionato nella finestra **Esplora soluzioni** . Quando si aggiungono dati, nella finestra di progettazione vengono visualizzate tabelle e colonne. Se non viene visualizzata la finestra di progettazione (la finestra vuota con la scheda Model. bim), in **Esplora soluzioni**, in `AW Internet Sales Tabular Model`, fare doppio clic il **Model. bim** file.  
  
 Nella finestra **Proprietà** è possibile visualizzare le proprietà di base del progetto. Nelle **Esplora soluzioni**, fare clic su `AW Internet Sales Tabular Model`. Si noti che nella finestra **Proprietà** , in **File di progetto**, viene visualizzato **AW Internet Sales Tabular Model.smproj**. Si tratta del nome del file di progetto, mentre in **Cartella di progetto**viene visualizzato il percorso specifico del file di progetto.  
  
 Nella **Esplora soluzioni**, fare doppio clic il `AW Internet Sales Tabular Model` del progetto e quindi fare clic su **proprietà**. Verrà visualizzata la finestra di dialogo **Pagine delle proprietà di AW Internet Sales Tabular Model** (Pagine delle proprietà di AW Internet Sales Tabular Model). Si tratta delle proprietà avanzate del progetto. Più avanti, prima di distribuire il modello, verranno impostate alcune di queste proprietà.  
  
 A questo punto, esaminiamo le proprietà del modello. In **Esplora soluzioni**fare clic su **Model.bim**. Nella finestra **Proprietà** verranno visualizzate le proprietà del modello, la più importante delle quali è la proprietà **Modalità DirectQuery** . Questa proprietà specifica se il modello verrà distribuito o meno nella modalità In-Memory (disattivata) o nella modalità DirectQuery (attivata). Per questa esercitazione il modello verrà creato e distribuito nella modalità In-Memory.  
  
 Quando si crea un nuovo modello, determinate proprietà del modello vengono impostate automaticamente in base alle impostazioni di Modellazione dati che è possibile specificare nella finestra di dialogo Strumenti\Opzioni. Le proprietà Backup dei dati, Memorizzazione area di lavoro e Server dell'area di lavoro consentono di specificare la modalità e la posizione per il backup, la conservazione in memoria e la compilazione del database dell'area di lavoro, ovvero il database di creazione di modelli. Queste impostazioni possono essere modificate successivamente, ma per il momento è possibile lasciarle invariate.  
  
 Con l'installazione di [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]vengono aggiunte nuove voci di menu all'ambiente di Visual Studio. Esaminiamo le nuove voci di menu che sono specifiche per la creazione di modelli tabulari. Fare clic sul menu **Modello** . Da questa posizione è possibile avviare l'Importazione guidata tabella, visualizzare e modificare le connessioni esistenti, aggiornare i dati dell'area di lavoro, esplorare il modello in [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel utilizzando la funzionalità Analizza in Excel, creare prospettive e ruoli, selezionare la vista del modello e impostare opzioni di calcolo.  
  
 Fare clic sul menu **Tabella**. Da questa posizione è possibile creare e gestire relazioni tra tabelle, creare, gestire e specificare impostazioni della tabella data, creare partizioni e modificare proprietà della tabella.  
  
 Fare clic sul menu **Colonna** . Da questa posizione è possibile aggiungere ed eliminare colonne in una tabella, bloccare colonne e specificare un ordinamento. È inoltre possibile utilizzare la funzionalità Somma automatica per creare una misura di aggregazione standard per una colonna selezionata. Gli altri pulsanti della barra degli strumenti forniscono accesso rapido a funzionalità e comandi utilizzati di frequente.  
  
 Esplorare alcune delle finestre di dialogo e posizioni per diverse funzionalità specifiche della creazione di modelli tabulari. Sebbene alcuni elementi non saranno ancora attivi, è possibile farsi una buona idea dell'ambiente di creazione di modelli tabulari.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 2: Aggiungere dati](lesson-2-add-data.md).  
  
  
