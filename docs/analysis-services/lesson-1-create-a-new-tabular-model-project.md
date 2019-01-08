---
title: 'Lezione 1: Creare un nuovo progetto di modello tabulare | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b0c376c6ab8625d2f31e6ad6ea132842315b1e1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52410777"
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>Lezione 1: Creare un nuovo modello di progetto tabulare
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In questa lezione verrà creato un nuovo progetto di modello tabulare in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Una volta creato il nuovo progetto, è possibile iniziare ad aggiungere dati tramite l'Importazione guidata tabella. Questa lezione offre anche una breve introduzione all'ambiente di SSDT di creazione di modelli tabulari.  
  
Tempo stimato per il completamento della lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento è la prima lezione di un'esercitazione sulla creazione di modelli tabulari. Per completare questa lezione, è necessario disporre di database di esempio AdventureWorksDW installato in un'istanza di SQL Server. Per altre informazioni, vedere [modellazione tabulare &#40;esercitazione su Adventure Works&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Creare un nuovo modello di progetto tabulare  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Per creare un nuovo modello di progetto tabulare  
  
1.  In SSDT nel **File** menu, fare clic su **New** > **progetto**.  
  
2.  Nel **nuovo progetto** finestra di dialogo espandere **installati** > **Business Intelligence** > **Analysis Services**, quindi fare clic su **progetto tabulare di Analysis Services**.  
  
3.  Nelle **Name**, digitare **AW Internet Sales**e quindi specificare un percorso per i file di progetto.  
  
    Per impostazione predefinita, **Nome soluzione** corrisponde al nome del progetto. È tuttavia possibile digitare un nome diverso per la soluzione.  
  
4.  Fare clic su **OK**.  
  
5.  Nel **progettazione di modelli tabulari** finestra di dialogo **dell'area di lavoro integrata**.  
  
    L'area di lavoro ospiterà un database modello tabulare con lo stesso nome del progetto durante la creazione di modelli. Area di lavoro integrata significa che SSDT userà un'istanza predefinita, eliminando la necessità di installare un'istanza del server Analysis Services separata solo per la creazione del modello. Per altre informazioni, vedere [dell'area di lavoro Database](../analysis-services/tabular-models/workspace-database-ssas-tabular.md).
      
6.  In **Livello di compatibilità**verificare che **SQL Server 2016 (1200)** sia selezionato e fare clic su **OK**.   
 
    ![as-tabular-lesson1-tmd](../analysis-services/media/as-tabular-lesson1-tmd.png)
      
    Se non SQL Server 2016 RTM (1200) nella casella di riepilogo livello compatibilità, non si usa la versione più recente di SQL Server Data Tools. Per ottenere l'ultima versione, vedere [Installare SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

    Se si usa la versione più recente di SSDT, è anche possibile scegliere SQL Server 2017 (1400). Tuttavia, per completare la lezione 13: Distribuire, è necessario un SQL Server 2017 o a un server di Azure per distribuire in.
      
    Selezionare un livello di compatibilità precedenti è consigliabile solo se si vuole distribuire il modello tabulare in una diversa istanza di Analysis Services in esecuzione una versione precedente di SQL Server. Area di lavoro integrata non è supportata per i livelli di compatibilità precedenti. Per alte informazioni, vedere [Livello di compatibilità per i modelli tabulari in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).   
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>Informazioni sul modello tabulare di SSDT ambiente di creazione  
Ora che è stato creato un nuovo progetto di modello tabulare, verrà analizzato l'ambiente di SSDT di creazione di modelli tabulari.  
  
Dopo aver creato il progetto, viene aperto in SSDT. Sul lato destro, in **Esplora modelli tabulari**, si noterà una visualizzazione albero degli oggetti nel modello. Poiché sono stati ancora importati i dati, le cartelle sono vuote. È possibile fare doppio clic su una cartella di oggetti per eseguire azioni, simile alla barra dei menu. Durante l'esecuzione di questa esercitazione, si userà Esplora modelli tabulari per spostarsi tra i diversi oggetti nel progetto del modello.

![as-tabular-lesson1-tme](../analysis-services/media/as-tabular-lesson1-tme.png)

Scegliere il **Esplora soluzioni** scheda. In questo caso, si noterà il **Model. bim** file. Se non è visibile la finestra di progettazione verso sinistra (la finestra vuota con la scheda Model. bim), in **Esplora soluzioni**, in **progetto AW Internet Sales**, fare doppio clic il **Model. bim** file. Il file Model. bim contiene tutti i metadati per il progetto di modello. 

![as-tabular-lesson1-se](../analysis-services/media/as-tabular-lesson1-se.png)
  
Esaminiamo le proprietà del modello. Scegliere **Model.bim**. Nel **le proprietà** finestra, si noterà il [delle proprietà del modello](../analysis-services/tabular-models/model-properties-ssas-tabular.md)più importante delle quali è la **la modalità DirectQuery** proprietà. Questa proprietà specifica se il modello verrà distribuito o meno nella modalità In-Memory (disattivata) o nella modalità DirectQuery (attivata). Per questa esercitazione il modello verrà creato e distribuito nella modalità In-Memory.

![as-tabular-lesson1-properties](../analysis-services/media/as-tabular-lesson1-properties.png)
  
Quando si crea un nuovo modello, determinate proprietà del modello vengono impostate automaticamente in base alle impostazioni di modellazione dati che possono essere specificate nel **degli strumenti** > **opzioni** nella finestra di dialogo. Le proprietà Backup dei dati, Memorizzazione area di lavoro e Server dell'area di lavoro consentono di specificare la modalità e la posizione per il backup, la conservazione in memoria e la compilazione del database dell'area di lavoro, ovvero il database di creazione di modelli. Queste impostazioni possono essere modificate successivamente, ma per il momento è possibile lasciarle invariate.  

Nelle **Esplora soluzioni**, fare doppio clic su **AW Internet Sales** (progetto), quindi fare clic su **proprietà**. Il **pagine delle proprietà di AW Internet Sales** verrà visualizzata la finestra di dialogo. Questi sono gli avanzati [proprietà del progetto](../analysis-services/tabular-models/project-properties-ssas-tabular.md). Più avanti, prima di distribuire il modello, verranno impostate alcune di queste proprietà.  
  
Durante l'installazione di SSDT, nuove voci di menu sono stati aggiunti all'ambiente di Visual Studio. Diamo un'occhiata quelle specifiche per la creazione di modelli tabulari. Fare clic sul menu **Modello** . A questo punto, è possibile avviare l'importazione guidata tabella consente di visualizzare e modificare le connessioni esistenti, aggiornare i dati dell'area di lavoro, esplorare il modello in Excel con la funzionalità analizza in Excel, creare prospettive e ruoli, selezionare la vista modelli e impostare le opzioni di calcolo.  
  
Fare clic sul menu **Tabella** . Da questa posizione è possibile creare e gestire relazioni tra tabelle, creare, gestire e specificare impostazioni della tabella data, creare partizioni e modificare proprietà della tabella.  
  
Fare clic sul menu **Colonna** . Da questa posizione è possibile aggiungere ed eliminare colonne in una tabella, bloccare colonne e specificare un ordinamento. È inoltre possibile utilizzare la funzionalità Somma automatica per creare una misura di aggregazione standard per una colonna selezionata. Gli altri pulsanti della barra degli strumenti forniscono accesso rapido a funzionalità e comandi utilizzati di frequente.  
  
Esplorare alcune delle finestre di dialogo e posizioni per diverse funzionalità specifiche della creazione di modelli tabulari. Sebbene alcuni elementi non saranno ancora attivi, è possibile farsi una buona idea dell'ambiente di creazione di modelli tabulari.  


## <a name="additional-resources"></a>Risorse aggiuntive
Per altre informazioni sui diversi tipi di progetti di modelli tabulari, vedere [progetti di modello tabulare](../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md). Per altre informazioni sull'ambiente di creazione di modelli tabulari, vedere [progettazione di modelli tabulari ](../analysis-services/tabular-models/tabular-model-designer-ssas.md).  
  

## <a name="whats-next"></a>Quali sono le operazioni successive?
Passare alla lezione successiva: [Lezione 2: Aggiungere dati](../analysis-services/lesson-2-add-data.md).

  
  
  
