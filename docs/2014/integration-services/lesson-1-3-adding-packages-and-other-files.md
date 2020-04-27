---
title: 'Passaggio 3: Aggiunta di pacchetti e altri file | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a7e6ec9c-d31d-4613-9525-8947a7b358f7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7db3e293c95b358d78e445e6b7534f90ea7b9310
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62892132"
---
# <a name="step-3-adding-packages-and-other-files"></a>Passaggio 3: Aggiunta di pacchetti e altri file
  In questa attività verranno aggiunti i pacchetti esistenti, i file ausiliari di supporto a singoli pacchetti e un file Leggimi relativo al progetto Deployment Tutorial creato nell'attività precedente. Verrò aggiunto ad esempio un file di dati XML contenente i dati relativi a un pacchetto e un file di testo che include informazioni su tutti i pacchetti del progetto.  
  
 Quando si distribuiscono i pacchetti in un ambiente di test o produzione, non si includono in genere i file di dati, ma si utilizzano invece le configurazioni per l'aggiornamento dei percorsi delle origini dei dati in modo da poter accedere a versioni di test o produzione dei database o dei file di dati. Questa esercitazione include file di dati nella distribuzione dei pacchetti allo scopo di fornire istruzioni.  
  
 I pacchetti e i dati di esempio utilizzati dai pacchetti vengono installati unitamente agli esempi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Al progetto Deployment Tutorial verranno aggiungi i pacchetti seguenti:  
  
-   **DataTransfer.** Pacchetto di base che estrae i dati da un file flat, valuta i valori delle colonne per mantenere le righe nel set di dati in modo condizionale e carica i dati in una tabella del database AdventureWorks.  
  
-   **LoadXMLData.** Pacchetto di trasferimento dei dati che estrae dati da un file XML, valuta e aggrega i valori delle colonne e carica i dati in una tabella del database AdventureWorks.  
  
 Per supportare la distribuzione di tali pacchetti, verranno aggiunti al progetto Deployment Tutorial i file ausiliari seguenti.  
  
|Pacchetto|File|  
|-------------|----------|  
|DataTransfer|NewCustomers.txt|  
|LoadXMLData|orders.xml e orders.xsd|  
  
 Verrà inoltre aggiunto un file Leggimi, ovvero un file di testo contenente informazioni sul progetto Deployment Tutorial.  
  
 I percorsi utilizzati nelle procedure seguenti fanno riferimento agli esempi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installati nel percorso predefinito, ovvero [!INCLUDE[ssSampPathIS](../includes/sssamppathis-md.md)]. Se gli esempi sono stati installati in un altro percorso, sarà necessario utilizzare quest'ultimo invece di quello indicato nelle procedure.  
  
 Nell'attività successiva si procederà all'aggiunta delle configurazioni per i pacchetti DataTransfer e LoadXMLData. Tutte le configurazioni sono archiviate in file XML il cui percorso verrà specificato mediante l'impostazione di una variabile di ambiente del sistema. Dopo aver creato i file di configurazione, questi ultimi verranno aggiunti al progetto.  
  
### <a name="to-add-packages-to-the-deployment-tutorial-project"></a>Per aggiungere i pacchetti al progetto Deployment Tutorial.  
  
1.  Se [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] non è già aperto, fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server**, quindi fare clic su **SQL Server Data Tools**.  
  
2.  Scegliere **Apri** dal menu **File**, fare clic su **Progetto/Soluzione**, selezionare la cartella **Deployment Tutorial** , fare clic su **Apri**e fare doppio clic su **Deployment Tutorial.sln**.  
  
3.  In Esplora soluzioni fare clic con il pulsante destro del mouse su Deployment Tutorial, scegliere **Aggiungi**e quindi **Pacchetto esistente**.  
  
4.  Nella finestra di dialogo **Aggiungi copia del pacchetto esistente** , in **Posizione pacchetto**, selezionare **File system**.  
  
5.  Fare clic sul pulsante con i puntini di sospensione **(...)** , passare a C:\Programmi\Microsoft SQL Server\100\Samples\Integration ServicesTutorial\Deploying Packages\Completed Packages, selezionare **DataTransfer.dtsx**e quindi fare clic su **Apri**.  
  
6.  Fare clic su **OK**.  
  
7.  Ripetere i passaggi da 3 a 6 per aggiungere questa volta LoadXMLData.dtsx, che si trova in C:\Programmi\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Completed Packages.  
  
### <a name="to-add-ancillary-files-to-the-deployment-tutorial-project"></a>Per aggiungere i file ausiliari al progetto Deployment Tutorial  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse su Deployment Tutorial, scegliere **Aggiungi**e quindi **Elemento esistente**.  
  
2.  Nella finestra di dialogo **Aggiungi elemento esistente - Deployment Tutorial** passare a C:\Programmi\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Sample Data, selezionare orders.xml, orders.xsd e NewCustomers.txt e quindi fare clic su **Aggiungi**.  
  
3.  Nella finestra di dialogo **Aggiungi elemento esistente - Deployment Tutorial** passare a C:\Programmi\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\\, selezionare Readme.txt e fare clic su **Aggiungi**.  
  
4.  Scegliere **Salva tutto**dal menu File.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 4: Aggiunta delle configurazioni dei pacchetti](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
![Integration Services icona (piccola)](media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
  
