---
title: 'Analysis Services tutorial-lezione 1: Creare un nuovo progetto di modello tabulare | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 52e0b3f317044e25b2004512083fdcaff7a77ecf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148987"
---
# <a name="create-a-tabular-model-project"></a>Creare un progetto di modello tabulare

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione si usa Visual Studio con SQL Server Data Tools (SSDT) o Visual Studio 2017 con Microsoft Analysis Services progetti VSIX per creare un nuovo progetto di modello tabulare al livello di compatibilità 1400. Dopo aver creato il nuovo progetto, è possibile iniziare l'aggiunta di dati e creazione del modello. Questa lezione offre anche una breve introduzione all'ambiente di Visual Studio di creazione di modelli tabulari.  
  
Tempo stimato per il completamento della lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti

Questo articolo è la prima lezione di un'esercitazione sulla creazione di modelli tabulari. Per completare questa lezione, esistono diversi prerequisiti, che dovrai avere sul posto. Per altre informazioni, vedere [Analysis Services - esercitazione su Adventure Works](../tutorial-tabular-1400/as-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Creare un nuovo modello di progetto tabulare  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Per creare un nuovo modello di progetto tabulare  
  
1.  In Visual Studio sul **File** menu, fare clic su **New** > **progetto**.  
  
2.  Nel **nuovo progetto** finestra di dialogo espandere **installati** > **Business Intelligence** > **Analysis Services**, quindi fare clic su **progetto tabulare di Analysis Services**.  
  
3.  Nelle **Name**, digitare **AW Internet Sales**e quindi specificare un percorso per i file di progetto.  
  
    Per impostazione predefinita **nome della soluzione** corrisponde al nome del progetto; tuttavia, è possibile digitare un nome diverso per la soluzione.  
  
4.  Fare clic su **OK**.  
  
5.  Nel **progettazione di modelli tabulari** finestra di dialogo **dell'area di lavoro integrata**.  
  
    L'area di lavoro ospita un database modello tabulare con lo stesso nome del progetto durante la creazione di modelli. Area di lavoro integrata significa che Visual Studio Usa un'istanza predefinita, eliminando la necessità di installare un'istanza del server Analysis Services separata solo per la creazione del modello.
      
6.  Nelle **livello di compatibilità**, selezionare **SQL Server 2017 / Azure Analysis Services (1400)**.   
 
    ![as-lesson1-tmd](../tutorial-tabular-1400/media/as-lesson1-tmd.png)
      
    Se SQL Server 2017 / Azure Analysis Services (1400) nella casella di riepilogo livello compatibilità non è visibile, non si usa la versione più recente di SQL Server Data Tools. Per ottenere l'ultima versione, vedere [Installare SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>Informazioni sul modello tabulare di SSDT ambiente di creazione  

Ora che è stato creato un nuovo progetto di modello tabulare, verrà analizzato l'ambiente di Visual Studio di creazione di modelli tabulari.  
  
Dopo aver creato il progetto, viene aperto in Visual Studio. Sul lato destro, in **Esplora modelli tabulari**, è disponibile una visualizzazione struttura ad albero degli oggetti nel modello. Poiché sono stati ancora importati i dati, le cartelle sono vuote. È possibile fare doppio clic su una cartella di oggetti per eseguire azioni, simile alla barra dei menu. Durante l'esecuzione di questa esercitazione, si usa Esplora modelli tabulari per spostarsi tra i diversi oggetti nel progetto del modello.

![as-lesson1-tme](../tutorial-tabular-1400/media/as-lesson1-tme.png)

Scegliere il **Esplora soluzioni** scheda. In questo caso, viene visualizzato il **Model. bim** file. Se non è visibile la finestra di progettazione verso sinistra (la finestra vuota con la scheda Model. bim), in **Esplora soluzioni**, in **progetto AW Internet Sales**, fare doppio clic il **Model. bim** file. Il file Model. bim contiene i metadati per il progetto di modello. 

![as-lesson1-se](../tutorial-tabular-1400/media/as-lesson1-se.png)
  
Scegliere **Model.bim**. Nel **delle proprietà** finestra vengono visualizzate le proprietà di modello, più importante delle quali è la **la modalità DirectQuery** proprietà. Questa proprietà specifica se il modello viene distribuito nella modalità In-Memory (disattivata) o la modalità DirectQuery (attivata). Per questa esercitazione, creare e distribuire il modello in modalità In memoria.

![as-lesson1-properties](../tutorial-tabular-1400/media/as-lesson1-properties.png)
  
Quando si crea un progetto di modello, determinate proprietà del modello vengono impostate automaticamente in base alle impostazioni di modellazione dati che possono essere specificate nel **degli strumenti** menu > **opzioni** nella finestra di dialogo. Le proprietà Backup dei dati, Memorizzazione area di lavoro e Server dell'area di lavoro consentono di specificare la modalità e la posizione per il backup, la conservazione in memoria e la compilazione del database dell'area di lavoro, ovvero il database di creazione di modelli. È possibile modificare queste impostazioni in un secondo momento se necessario, ma per ora, lasciarle come sono.  

Nelle **Esplora soluzioni**, fare doppio clic su **AW Internet Sales** (progetto), quindi fare clic su **proprietà**. Il **pagine delle proprietà di AW Internet Sales** verrà visualizzata la finestra di dialogo. Impostare alcune di queste proprietà in un secondo momento quando si distribuisce il modello.  
  
Durante l'installazione di SSDT, nuove voci di menu sono stati aggiunti all'ambiente di Visual Studio. Scegliere il **modello** menu. A questo punto, si può importare i dati, aggiornare i dati dell'area di lavoro, esplorare il modello in Excel, creare prospettive e ruoli, selezionare la vista modelli e impostare le opzioni di calcolo. Scegliere il **tabella** menu. A questo punto, è possibile creare e gestire relazioni, specificare impostazioni tabella data, creare partizioni e modificare le proprietà della tabella. Se si sceglie la **colonna** menu, è possibile aggiungere ed eliminare colonne in una tabella, bloccare le colonne e specificare l'ordinamento. SSDT aggiunge anche alcuni pulsanti alla barra. Più utile è la funzionalità Somma automatica per creare una misura di aggregazione standard per una colonna selezionata. Gli altri pulsanti della barra degli strumenti forniscono accesso rapido a funzionalità e comandi utilizzati di frequente.  
  
Esplorare alcune delle finestre di dialogo e posizioni per diverse funzionalità specifiche della creazione di modelli tabulari. Mentre alcuni elementi non sono ancora attivi, è possibile ottenere una buona idea dell'ambiente di creazione di modelli tabulari.  
  

## <a name="whats-next"></a>Quali sono le operazioni successive?

[Lezione 2: Ottenere dati](../tutorial-tabular-1400/as-lesson-2-get-data.md).

  
  
  
