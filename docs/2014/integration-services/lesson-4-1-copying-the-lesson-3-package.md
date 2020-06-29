---
title: 'Passaggio 1: Copia del pacchetto della lezione 3 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1645a1dee923da3913d12e36bdd60829918bbf7b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440478"
---
# <a name="step-1-copying-the-lesson-3-package"></a>Passaggio 1: Copia del pacchetto della lezione 3
  In questa attività si creerà una copia del pacchetto della lezione 3, denominato Lesson 3.dtsx. In alternativa, se non è stata completata la lezione 3, è possibile aggiungere al progetto il pacchetto completo della lezione 3 incluso nell'esercitazione e quindi effettuarne una copia. Questa nuova copia verrà usata nella lezione 4.  
  
### <a name="to-create-the-lesson-4-package"></a>Per creare il pacchetto della lezione 4  
  
1.  Se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools non è già aperto, fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server**e selezionare **SQL Server Data Tools**.  
  
2.  Scegliere **Apri** dal menu **File**, fare clic su **Progetto/Soluzione**, selezionare **SSIS Tutorial** e fare clic su **Apri**, quindi fare doppio clic su **SSIS Tutorial.sln**.  
  
3.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Lesson 3.dtsx**e scegliere **Copia**.  
  
4.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **pacchetti SSIS**e quindi scegliere **Incolla**.  
  
     Per impostazione predefinita, il pacchetto copiato viene denominato Lesson 4.dtsx.  
  
5.  In Esplora soluzioni fare doppio clic su **Lesson 4. dtsx** per aprire il pacchetto.  
  
6.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dello sfondo della scheda **Flusso di controllo** e scegliere **Proprietà**.  
  
7.  Nella Finestra Proprietà aggiornare la `Name` proprietà a `Lesson 4` .  
  
8.  Fare clic sulla casella relativa alla proprietà **ID** , e poi nell'elenco selezionare **\<Generate New ID>**.  
  
### <a name="to-add-the-completed-lesson-3-package"></a>Per aggiungere il pacchetto della lezione 3 completato  
  
1.  Aprire [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e aprire il progetto SSIS Tutorial.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **pacchetti SSIS**e scegliere **Aggiungi pacchetto esistente**.  
  
3.  Nella finestra **di dialogo Aggiungi copia del pacchetto esistente** , in **Posizione pacchetto**, selezionare **file System**.  
  
4.  Fare clic sul pulsante Sfoglia **(...)** , passare a Lesson 3. dtsx nel computer e quindi fare clic su **Apri**.  
  
     Per scaricare tutti i pacchetti di lezioni di questa esercitazione, effettuare le operazioni seguenti.  
  
    1.  Passare alla pagina relativa agli [esempi di prodotti di Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Fare clic sulla scheda **Downloads** .  
  
    3.  Fare clic sul file SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copiare e incollare il pacchetto della lezione 3, come illustrato nei passaggi 3-8 della procedura precedente.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 2: Creazione di un file danneggiato](lesson-4-2-creating-a-corrupted-file.md)  
  
  
