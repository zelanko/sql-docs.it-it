---
title: 'Passaggio 2: Aggiunta e configurazione di registrazione | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ef4f5d42ae3451d4199e84480a5672e437d7ca5f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892437"
---
# <a name="step-2-adding-and-configuring-logging"></a>Passaggio 2: Aggiunta e configurazione di funzionalità di registrazione
  In questa attività verrà abilitata la registrazione per il flusso di dati del pacchetto Lesson 3.dtsx. Successivamente un provider di log per file di testo verrà configurato in modo da registrare gli eventi PipelineExecutionPlan e PipelineExecuteTrees. Il provider di log per file di testo crea log facili da visualizzare e da spostare. La semplicità di questi file di log li rende particolarmente utili nella fase di test di base di un pacchetto. Le voci di log possono essere visualizzate anche nella finestra Registra eventi di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
### <a name="to-add-logging-to-the-package"></a>Per aggiungere le funzionalità di registrazione al pacchetto  
  
1.  Scegliere **Registrazione** dal menu **SSIS**.  
  
2.  Nel riquadro **Contenitori** della finestra di dialogo **Configura log SSIS** verificare che sia selezionato l'oggetto in prima posizione, che rappresenta il pacchetto della lezione 3.  
  
3.  Nella casella **Tipo provider** della scheda **Provider e log** selezionare **Provider di log SSIS per file di testo**e quindi fare clic su **Aggiungi**.  
  
     Integration Services consente di aggiungere un nuovo provider di log per file di testo al pacchetto con il nome predefinito **Provider di log SSIS per file di testo**. È ora possibile configurare il nuovo provider di log.  
  
4.  Nel **Name** colonna, tipo `Lesson 3 Log File`.  
  
5.  Facoltativamente, modificare la **Descrizione**.  
  
6.  Nel **Configuration** colonna, fare clic su  **\<nuova connessione >** per specificare la destinazione in cui viene scritto le informazioni del log.  
  
     Nella finestra di dialogo **Editor gestione connessione file** per **Tipo di utilizzo**selezionare **Crea file**e quindi fare clic su **Sfoglia**. Per impostazione predefinita, la finestra di dialogo **Seleziona file** apre la cartella di progetto; tuttavia è possibile salvare le informazioni sulla registrazione in qualsiasi posizione.  
  
7.  Nel **seleziona File** nella finestra di dialogo il **nome File** nella casella `TutorialLog.log`, fare clic su **Open**.  
  
8.  Fare clic su **OK** per chiudere la finestra di dialogo **Editor gestione connessione file** .  
  
9. Nel riquadro **Contenitori** espandere tutti i nodi della gerarchia del contenitore del pacchetto e quindi deselezionare tutte le caselle di controllo, compresa **Extract Sample Currency Data** . Selezionare quindi la casella di controllo **Extract Sample Currency Data** per ottenere solo gli eventi relativi a tale nodo.  
  
    > [!IMPORTANT]  
    >  Se la casella di controllo **Extract Sample Currency Data** risulta non disponibile anziché selezionata, l'attività usa le impostazioni log del contenitore padre e non è possibile attivare gli eventi specifici dell'attività.  
  
10. Nella colonna **Eventi** della scheda **Dettagli** selezionare gli eventi **PipelineExecutionPlan** e **PipelineExecutionTrees** .  
  
11. Fare clic su **Avanzate** per controllare i dettagli che verranno scritti nel log per ogni evento. Per impostazione predefinita, tutte le categorie delle informazioni vengono automaticamente selezionate per gli eventi specificati.  
  
12. Fare clic su **Standard** per nascondere le categorie delle informazioni.  
  
13. Nel **Provider e log** nella scheda il **Name** colonna, selezionare `Lesson 3 Log File`. Dopo aver creato un provider di log per il pacchetto, è possibile disabilitare temporaneamente la registrazione senza la necessità di eliminarlo e ricrearlo.  
  
14. Fare clic su **OK**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 [Passaggio 3: Il pacchetto della lezione 3 dell'esercitazione di test](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
  
