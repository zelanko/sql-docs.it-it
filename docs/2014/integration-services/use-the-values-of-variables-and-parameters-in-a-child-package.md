---
title: Usare i valori delle variabili e parametri in un pacchetto figlio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- configurations [Integration Services]
- packages [Integration Services], configurations
- variables [Integration Services], adding
ms.assetid: 9b939edb-4e17-48e5-8428-855beb10049c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c1e942df4681595be19f31aa6a9d7c6fd3a6dd12
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766104"
---
# <a name="use-the-values-of-variables-and-parameters-in-a-child-package"></a>Utilizzare i valori di variabili e parametri in un pacchetto figlio
  In questa procedura viene descritto come creare una configurazione di pacchetto in cui viene utilizzato il tipo di configurazione variabile padre. Questo tipo di configurazione consente a un pacchetto figlio eseguito da un pacchetto padre di accedere a una variabile del pacchetto padre.  
  
> [!NOTE]  
>  È inoltre possibile passare valori a un pacchetto figlio configurando l'attività Esegui pacchetto per eseguire il mapping delle variabili o dei parametri del pacchetto padre o dei parametri del progetto ai parametri del pacchetto figlio. Per altre informazioni, vedere [Attività Esegui pacchetto](control-flow/execute-package-task.md).  
  
 Non è necessario creare la variabile nel pacchetto padre prima di creare la configurazione di pacchetto nel pacchetto figlio. La variabile può essere aggiunta al pacchetto padre in qualsiasi momento, ma nella configurazione di pacchetto è necessario utilizzare il nome esatto della variabile padre. Affinché sia possibile creare una configurazione che utilizza la variabile padre, tuttavia, nel pacchetto figlio deve essere presente una variabile che possa essere aggiornata dalla configurazione. Per altre informazioni sull'aggiunta e la configurazione di variabili, vedere [Aggiungere, eliminare o modificare l'ambito di una variabile definita dall'utente in un pacchetto](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md).  
  
 Come ambito per la variabile del pacchetto padre utilizzata nella configurazione di tipo Variabile pacchetto padre è possibile impostare l'attività Esegui pacchetto, il contenitore che include l'attività o il pacchetto. Se in uno stesso pacchetto sono definite più variabili con lo stesso nome, verrà utilizzata quella con ambito più vicino all'attività Esegui pacchetto. L'ambito più vicino all'attività Esegui pacchetto è l'attività stessa.  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>Per aggiungere una variabile a un pacchetto padre  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contenente il pacchetto a cui si desidera aggiungere una variabile da passare a un pacchetto figlio.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] eseguire una delle operazioni seguenti per definire l'ambito della variabile:  
  
    -   Per impostare il pacchetto come ambito, fare clic in un punto qualsiasi dell'area di progettazione della scheda **Flusso di controllo** .  
  
    -   Per impostare come ambito un contenitore padre dell'attività Esegui pacchetto, fare clic sul contenitore.  
  
    -   Per impostare l'ambito sull'attività Esegui pacchetto, fare clic sull'attività.  
  
4.  Aggiungere e configurare una variabile.  
  
    > [!NOTE]  
    >  Selezionare un tipo di dati compatibile con i dati che verranno memorizzati nella variabile.  
  
5.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
### <a name="to-add-a-variable-to-a-child-package"></a>Per aggiungere una variabile a un pacchetto figlio  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contenente il pacchetto a cui si vuole aggiungere una configurazione di variabile padre.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] , per impostare il pacchetto come ambito, fare clic in un punto qualsiasi dell'area di progettazione della scheda **Flusso di controllo** .  
  
4.  Aggiungere e configurare una variabile.  
  
    > [!NOTE]  
    >  Selezionare un tipo di dati compatibile con i dati che verranno memorizzati nella variabile.  
  
5.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
### <a name="to-add-a-parent-package-configuration-to-a-child-package"></a>Per aggiungere a un pacchetto figlio una configurazione di tipo Variabile pacchetto padre  
  
1.  Se necessario, aprire il pacchetto figlio in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Fare clic in un punto qualsiasi dell'area di progettazione della scheda **Flusso di controllo** .  
  
3.  Scegliere **Configurazioni pacchetto** dal menu **SSIS**.  
  
4.  Nella finestra di dialogo **Libreria configurazioni pacchetto** selezionare **Abilita configurazioni pacchetto**e quindi fare clic su **Aggiungi**.  
  
5.  Nella pagina iniziale di Configurazione guidata pacchetto fare clic su **Avanti**.  
  
6.  Nella pagina Selezione tipo di configurazione selezionare **Variabile pacchetto padre** nell'elenco **Tipo configurazione** ed eseguire una delle operazioni seguenti:  
  
    -   Selezionare **Usa le impostazioni di configurazione specificate di seguito**e quindi specificare nella casella **Variabile padre** il nome della variabile del pacchetto padre da usare nella configurazione.  
  
        > [!IMPORTANT]  
        >  Per i nomi delle variabili viene fatta distinzione tra maiuscole e minuscole.  
  
    -   Selezionare **Percorso della configurazione memorizzato in una variabile di ambiente** e quindi selezionare nell'elenco **Variabile di ambiente**la variabile di ambiente che contiene il nome della variabile.  
  
7.  Scegliere **Avanti**.  
  
8.  Nella pagina Selezione proprietà di destinazione espandere il nodo **Variabile** , espandere il nodo **Proprietà** della variabile da configurare e quindi fare clic sulla proprietà che deve essere impostata dalla configurazione.  
  
9. Scegliere **Avanti**.  
  
10. Nella pagina Completamento procedura guidata modificare facoltativamente il nome predefinito della configurazione e verificare le informazioni relative alla configurazione.  
  
11. Scegliere **Fine** per completare la procedura guidata e tornare alla finestra di dialogo **Libreria configurazioni pacchetto** .  
  
12. Nella finestra di dialogo **Libreria configurazioni pacchetto** la nuova configurazione è elencata nella casella **Configurazione** .  
  
13. Scegliere **Chiudi**.  
  
## <a name="see-also"></a>Vedere anche  
 [SSIS](../../2014/integration-services/package-configurations.md)   
 [Creazione di configurazioni dei pacchetti](../../2014/integration-services/create-package-configurations.md)   
 [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)   
 [Utilizzo di variabili nei pacchetti](../../2014/integration-services/use-variables-in-packages.md)  
  
  
