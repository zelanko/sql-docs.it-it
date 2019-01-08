---
title: 'Passaggio 1: Copia del pacchetto della lezione 2 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2bcc6c331908f33df3b324ff7061b38065e36981
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360888"
---
# <a name="step-1-copying-the-lesson-2-package"></a>Passaggio 1: Copia del pacchetto della lezione 2
  In questa attività si procederà alla creazione di una copia del pacchetto della lezione 2, denominato Lesson 2.dtsx. In alternativa è possibile aggiungere al progetto il pacchetto completo della lezione 2 incluso nell'esercitazione e successivamente copiarlo. Questa nuova copia verrà usata per il resto della lezione 3.  
  
### <a name="to-create-the-lesson-3-package"></a>Per creare il pacchetto della lezione 3  
  
1.  Se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools non è già aperto fare clic su **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server 2012**e quindi fare clic su **SQL Server Data Tools**.  
  
2.  Scegliere **Apri** dal menu **File**, fare clic su **Progetto/Soluzione**, selezionare **SSIS Tutorial** , fare clic su **Apri**e quindi fare doppio clic su **SSIS Tutorial.sln**.  
  
3.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Lesson 2.dtsx**e fare clic su **Copia**.  
  
4.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Pacchetti SSIS**e fare clic su **Incolla**.  
  
     Per impostazione predefinita, il pacchetto copiato viene denominato Lesson 3.dtsx.  
  
5.  In Esplora soluzioni fare doppio clic su **Lesson 3.dtsx** per aprire il pacchetto.  
  
6.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dello sfondo della scheda **Flusso di controllo** e scegliere **Proprietà**.  
  
7.  Nella finestra Proprietà aggiornare la `Name` proprietà `Lesson 3`.  
  
8.  Fare clic sulla casella per il **ID** proprietà, quindi nell'elenco, fare clic su  **\<Genera nuovo ID >**.  
  
### <a name="to-add-the-completed-lesson2-package"></a>Per aggiungere il pacchetto della lezione 2 completato  
  
1.  Aprire [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e aprire il progetto SSIS Tutorial.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Pacchetti SSIS**e selezionare **Aggiungi pacchetto esistente**.  
  
3.  Nella finestra di dialogo **Aggiungi copia del pacchetto esistente** , in **Posizione pacchetto**, selezionare **File system**.  
  
4.  Fare clic sul pulsante sfoglia **(...)**, passare a **Lesson 2.dtsx** nel computer, quindi fare clic su **Apri**.  
  
     Per scaricare tutti i pacchetti di lezioni di questa esercitazione, effettuare le operazioni seguenti.  
  
    1.  Passare alla pagina degli [esempi del prodotto di Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Fare clic sulla scheda **DOWNLOADS** .  
  
    3.  Fare clic sul file SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copiare e incollare il pacchetto della lezione 3, come illustrato nei passaggi 3-8 della procedura precedente.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 2: Aggiunta e configurazione di registrazione](lesson-3-2-adding-and-configuring-logging.md)  
  
  
