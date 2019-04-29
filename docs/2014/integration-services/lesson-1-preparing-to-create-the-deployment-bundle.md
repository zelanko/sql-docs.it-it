---
title: 'Lezione 1: Preparazione alla creazione del pacchetto di distribuzione | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b6fe283c-9856-4ba1-a497-e3912424fd18
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9e4695575aba2e43435c4e26d5a47ccb2cfa39d6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62891918"
---
# <a name="lesson-1-preparing-to-create-the-deployment-bundle"></a>Lezione 1: Preparazione alla creazione del pacchetto di distribuzione
  In questa lezione verranno illustrate le procedure per creare le cartelle di lavoro e le variabili di ambiente a supporto dell'esercitazione, per creare un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , per aggiungere diversi pacchetti e i rispettivi file di supporto al progetto, nonché per implementare le configurazioni nei pacchetti.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] consente di distribuire i pacchetti in base a un progetto. Il primo passaggio della creazione del pacchetto di distribuzione consiste pertanto nella raccolta di tutti i pacchetti e delle rispettive dipendenze in un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Risulta spesso utile includere altre informazioni nei pacchetti distribuiti, ad esempio un file Leggimi contenente la documentazione di base relativa al gruppo di pacchetti.  
  
 Dopo aver aggiunto i pacchetti e i file, si procederà all'aggiunta delle configurazioni ai pacchetti nei quali non sono ancora utilizzate. Le configurazioni consentono di aggiornare le proprietà dei pacchetti e gli oggetti dei pacchetti in fase di esecuzione. In una lezione successiva si procederà alla modifica dei valori di tali configurazioni durante la distribuzione dei pacchetti allo scopo di supportare i pacchetti nell'ambiente di destinazione della distribuzione.  
  
 Dopo aver aggiunto le configurazioni, è consigliabile aprire i pacchetti in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] , ovvero lo strumento grafico di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per la compilazione di pacchetti ETL, ed esaminare le proprietà di pacchetti e relativi elementi, nonché le configurazioni dei pacchetti per acquisire una migliore comprensione delle problematiche correlate alle esigenze di distribuzione. Uno dei pacchetti estrae ad esempio i dati da file di testo. Ai fini della corretta esecuzione dei pacchetti distribuiti, è pertanto necessario che il percorso dei file di dati venga aggiornato.  
  
 **Tempo stimato per il completamento della lezione:** 1 ora  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione sono incluse le attività seguenti:  
  
-   [Passaggio 1: Creazione di cartelle di lavoro e variabili di ambiente](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
-   [Passaggio 2: Creazione del progetto di distribuzione](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
-   [Passaggio 3: Aggiunta di pacchetti e altri file](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
-   [Passaggio 4: Aggiunta di configurazioni pacchetto](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
-   [Passaggio 5: Test dei pacchetti aggiornati](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
 [Passaggio 1: Creazione di cartelle di lavoro e variabili di ambiente](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
![Icona di Integration Services (piccola)](media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
  
