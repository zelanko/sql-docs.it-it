---
title: 'Passaggio 1: Copia del pacchetto della lezione 2 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3ae62c014baffec44c856587b99410b9c7228e6a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965271"
---
# <a name="step-1-copying-the-lesson-2-package"></a>Passaggio 1: Copia del pacchetto della lezione 2
  In questa attività si procederà alla creazione di una copia del pacchetto della lezione 2, denominato Lesson 2.dtsx. In alternativa è possibile aggiungere al progetto il pacchetto completo della lezione 2 incluso nell'esercitazione e successivamente copiarlo. Questa nuova copia verrà usata per il resto della lezione 3.  
  
### <a name="to-create-the-lesson-3-package"></a>Per creare il pacchetto della lezione 3  
  
1.  Se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools non è già aperto, fare clic su **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server 2012**, quindi selezionare **SQL Server Data Tools**.  
  
2.  Scegliere **Apri** dal menu **File**, fare clic su **Progetto/Soluzione**, selezionare **SSIS Tutorial** e fare clic su **Apri**, quindi fare doppio clic su **SSIS Tutorial.sln**.  
  
3.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Lesson 2.dtsx**e fare clic su **Copia**.  
  
4.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **pacchetti SSIS**e quindi scegliere **Incolla**.  
  
     Per impostazione predefinita, il pacchetto copiato viene denominato Lesson 3.dtsx.  
  
5.  In Esplora soluzioni fare doppio clic su **Lesson 3. dtsx** per aprire il pacchetto.  
  
6.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dello sfondo della scheda **Flusso di controllo** e scegliere **Proprietà**.  
  
7.  Nella Finestra Proprietà aggiornare la `Name` proprietà a `Lesson 3` .  
  
8.  Fare clic sulla casella relativa alla proprietà **ID** , e poi nell'elenco selezionare **\<Generate New ID>**.  
  
### <a name="to-add-the-completed-lesson2-package"></a>Per aggiungere il pacchetto della lezione 2 completato  
  
1.  Aprire [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e aprire il progetto SSIS Tutorial.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **pacchetti SSIS**e scegliere **Aggiungi pacchetto esistente**.  
  
3.  Nella finestra **di dialogo Aggiungi copia del pacchetto esistente** , in **Posizione pacchetto**, selezionare **file System**.  
  
4.  Fare clic sul pulsante sfoglia **(...)**, passare a **Lesson 2.dtsx** nel computer, quindi fare clic su **Apri**.  
  
     Per scaricare tutti i pacchetti di lezioni di questa esercitazione, effettuare le operazioni seguenti.  
  
    1.  Passare alla pagina relativa agli [esempi di prodotti di Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Fare clic sulla scheda **Downloads** .  
  
    3.  Fare clic sul file SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copiare e incollare il pacchetto della lezione 3, come illustrato nei passaggi 3-8 della procedura precedente.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 2: Aggiunta e configurazione di funzionalità di registrazione](lesson-3-2-adding-and-configuring-logging.md)  
  
  
