---
title: 'Passaggio 1: Copia del pacchetto della lezione 3 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c3a765f23b4bfcdd4d8f0ff84ac8d363424882bc
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377499"
---
# <a name="step-1-copying-the-lesson-3-package"></a>Passaggio 1: Copia del pacchetto della lezione 3
  In questa attività si creerà una copia del pacchetto della lezione 3, denominato Lesson 3.dtsx. In alternativa, se non è stata completata la lezione 3, è possibile aggiungere al progetto il pacchetto completo della lezione 3 incluso nell'esercitazione e quindi effettuarne una copia. Questa nuova copia verrà usata nella lezione 4.  
  
### <a name="to-create-the-lesson-4-package"></a>Per creare il pacchetto della lezione 4  
  
1.  Se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools non è già aperto, fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server**e selezionare **SQL Server Data Tools**.  
  
2.  Scegliere **Apri** dal menu **File**, fare clic su **Progetto/Soluzione**, selezionare **SSIS Tutorial** , fare clic su **Apri**e fare doppio clic su **SSIS Tutorial.sln**.  
  
3.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Lesson 3.dtsx**e scegliere **Copia**.  
  
4.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Pacchetti SSIS**e scegliere **Incolla**.  
  
     Per impostazione predefinita, il pacchetto copiato viene denominato Lesson 4.dtsx.  
  
5.  In Esplora soluzioni fare doppio clic su **Lesson 4.dtsx** per aprire il pacchetto.  
  
6.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dello sfondo della scheda **Flusso di controllo** e scegliere **Proprietà**.  
  
7.  Nella finestra Proprietà aggiornare la `Name` proprietà `Lesson 4`.  
  
8.  Fare clic sulla casella per il **ID** proprietà, quindi nell'elenco, fare clic su  **\<Genera nuovo ID >**.  
  
### <a name="to-add-the-completed-lesson-3-package"></a>Per aggiungere il pacchetto della lezione 3 completato  
  
1.  Aprire [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e aprire il progetto SSIS Tutorial.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Pacchetti SSIS**e selezionare **Aggiungi pacchetto esistente**.  
  
3.  Nella finestra di dialogo **Aggiungi copia del pacchetto esistente** , in **Posizione pacchetto**, selezionare **File system**.  
  
4.  Fare clic sul pulsante sfoglia **(...)**, passare a Lesson 3.dtsx nel computer, quindi fare clic su **Apri**.  
  
     Per scaricare tutti i pacchetti di lezioni di questa esercitazione, effettuare le operazioni seguenti.  
  
    1.  Passare alla pagina degli [esempi del prodotto di Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Fare clic sulla scheda **DOWNLOADS** .  
  
    3.  Fare clic sul file SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copiare e incollare il pacchetto della lezione 3, come illustrato nei passaggi 3-8 della procedura precedente.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 2: Creazione di un File danneggiato](lesson-4-2-creating-a-corrupted-file.md)  
  
  
