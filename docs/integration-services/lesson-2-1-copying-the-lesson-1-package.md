---
title: 'Passaggio 1: Copiare il pacchetto della lezione 1 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e73ea716252368e15dcba56242e803d6c1bf93d9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71283730"
---
# <a name="lesson-2-1-copy-the-lesson-1-package"></a>Lezione 2-1: Copiare il pacchetto della lezione 1

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



In questa attività si procederà alla creazione di una copia del pacchetto **Lesson 1.dts**. Se non è stata completata la lezione 1, è possibile usare il pacchetto della lezione 1 completato incluso in questa esercitazione. Questa nuova copia verrà usata per tutto il seguito della lezione 2.  
  
## <a name="create-the-lesson-2-package"></a>Creare il pacchetto della lezione 2  

Attenersi alla procedura seguente se si sta copiando la lezione 1 completata.  Per copiare la lezione 1 di esempio, vedere la sezione successiva.
  
1.  Se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools non è già aperto, selezionare **Start** > **Tutti i programmi** > **Microsoft SQL Server 2017** e quindi selezionare **SQL Server Data Tools**.  
  
2.  Nel menu **File** selezionare **Apri** > **Progetto/Soluzione**, selezionare la cartella **Esercitazione SSIS** e quindi **Apri** e fare doppio clic su **SSIS Tutorial.sln**.  
  
3.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Lesson 1.dtsx** e quindi selezionare **Copia**.  
  
4.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Pacchetti SSIS** e quindi selezionare **Incolla**.  
  
    Per impostazione predefinita, il pacchetto copiato viene denominato **Lesson 2.dtsx**.  
  
5.  In **Esplora soluzioni** fare doppio clic su **Lesson 2.dtsx** per aprire il pacchetto  
  
6.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dell'area di progettazione **Flusso di controllo** e selezionare **Proprietà**.  
  
7.  Nella finestra **Proprietà** aggiornare la proprietà **Name** impostandola su **Lesson 2**.  
  
8.  Selezionare la casella relativa alla proprietà **ID**, fare clic sulla freccia a discesa e quindi selezionare **\<Genera nuovo ID>** .  
  
## <a name="use-the-sample-lesson-1-package"></a>Usare il pacchetto della lezione 1 di esempio  
  
1.  Aprire [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools e il progetto SSIS Tutorial.  
  
2.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Pacchetti SSIS** e selezionare **Aggiungi pacchetto esistente**.  
  
3.  Nella finestra di dialogo **Aggiungi copia del pacchetto esistente** in **Posizione pacchetto** selezionare **File system**.  
  
4.  Selezionare il pulsante sfoglia **(...)** , passare a **Lesson 1.dtsx** nel computer e quindi selezionare **Apri**.  
  
5.  Copiare e incollare il pacchetto della lezione 1, come illustrato nei passaggi 3-8 della sezione precedente.  
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo

[Passaggio 2: Aggiungere e configurare il contenitore Ciclo Foreach](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
