---
title: 'Lezione 5: Aggiungere configurazioni del pacchetto SSIS per il modello di distribuzione del pacchetto | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9227f1c3d7cd6e6c6aacfd58c2e3fefa7a19728f
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58282005"
---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>Lezione 5: Aggiungere configurazioni del pacchetto SSIS per il modello di distribuzione del pacchetto

Le configurazioni di pacchetto consentono di impostare variabili e proprietà di runtime all'esterno dell'ambiente di sviluppo. Le configurazioni consentono inoltre di sviluppare pacchetti flessibili e semplici da implementare e distribuire. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sono disponibili i tipi di configurazione seguenti:  
  
-   File di configurazione XML  
  
-   Variabile di ambiente  
  
-   Voce del Registro di sistema  
  
-   Variabile pacchetto padre  
  
-   Tabella [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
In questa lezione si modifica il pacchetto di esempio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] creato nella [Lezione 4: Aggiungere il reindirizzamento del flusso errato con SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md) per usare il modello di distribuzione del pacchetto e le configurazioni del pacchetto. È anche possibile copiare il pacchetto della lezione 4 completato incluso in questa esercitazione. 

La Configurazione guidata pacchetto consente di creare una configurazione XML che aggiorna la proprietà **Directory** del contenitore Ciclo Foreach. Si usa una variabile a livello di pacchetto associata alla proprietà **Directory**. Dopo aver creato il file di configurazione, modificare il valore della variabile dall'esterno dell'ambiente di sviluppo a un nuovo percorso della cartella di dati di esempio. Quando il pacchetto viene eseguito nuovamente, il file di configurazione popola il valore della variabile che aggiorna la proprietà **Directory** . Il pacchetto esegue quindi l'iterazione nei file della nuova cartella di dati, anziché nella cartella hardcoded originale.  
  
> [!NOTE]
> Se non è ancora stato fatto, vedere [Lezione 1: Prerequisiti](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
In questa lezione sono incluse le attività seguenti:  
  
-   [Passaggio 1: Copiare il pacchetto della lezione 4](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [Passaggio 2: Abilitare e configurare le configurazioni di pacchetti](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [Passaggio 3: Modificare il valore di configurazione della proprietà Directory](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [Passaggio 4: Testare il pacchetto della lezione 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
  
-   [Passaggio 1: Copiare il pacchetto della lezione 4](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  
