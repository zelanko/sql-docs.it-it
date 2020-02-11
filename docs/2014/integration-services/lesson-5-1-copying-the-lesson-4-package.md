---
title: 'Passaggio 1: Copia del pacchetto della lezione 4 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3cf58665c69c744b35c8703f7f00fc07e0b8aafc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62891172"
---
# <a name="step-1-copying-the-lesson-4-package"></a>Passaggio 1: Copia del pacchetto della lezione 4
  In questa attività si procederà alla creazione di una copia del pacchetto creato nella lezione 4, denominato Lesson 4.dtsx. In alternativa, è possibile aggiungere al progetto il pacchetto completo della lezione 4 incluso nell'esercitazione e, successivamente, copiarlo. Questa nuova copia verrà usata per tutto il seguito della lezione 5.  
  
### <a name="to-copy-the-lesson-4-package"></a>Per copiare il pacchetto della lezione 4  
  
1.  Se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools non è già aperto, fare clic su **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server 2012**, quindi selezionare **SQL Server Data Tools**.  
  
2.  Scegliere **Apri**dal menu **file** , fare clic su **progetto/soluzione**, selezionare **SSIS Tutorial** , fare clic su **Apri**, quindi fare doppio clic su **SSIS Tutorial. sln**.  
  
3.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Lesson 4.dtsx**e quindi scegliere **Copia**.  
  
4.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **pacchetti SSIS**e quindi scegliere **Incolla**.  
  
     Per impostazione predefinita, il pacchetto copiato viene denominato Lesson 5.dtsx.  
  
5.  In Esplora soluzioni fare doppio clic su **Lesson 5.dtsx** per aprire il pacchetto.  
  
6.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dello sfondo della scheda **flusso di controllo** e quindi scegliere **Proprietà**.  
  
7.  Nella Finestra Proprietà aggiornare la `Name` proprietà a. `Lesson 5`  
  
8.  Fare clic sulla casella relativa alla proprietà **ID** , fare clic sulla freccia a discesa e quindi fare clic su ** \<genera nuovo ID>**.  
  
### <a name="to-add-the-completed-lesson-4-package"></a>Per aggiungere il pacchetto della lezione 4 completato  
  
1.  Aprire [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools e il progetto SSIS Tutorial.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **pacchetti SSIS**e scegliere **Aggiungi pacchetto esistente**.  
  
3.  Nella finestra **di dialogo Aggiungi copia del pacchetto esistente** , in **Posizione pacchetto**, selezionare **file System**.  
  
4.  Fare clic sul pulsante sfoglia **(...)**, passare a **Lesson 4.dtsx** nel computer, quindi fare clic su **Apri**.  
  
     Per scaricare tutti i pacchetti di lezioni di questa esercitazione, effettuare le operazioni seguenti.  
  
    1.  Passare alla pagina relativa agli [esempi di prodotti di Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Fare clic sulla scheda **Downloads** .  
  
    3.  Fare clic sul file SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copiare e incollare il pacchetto della lezione 4, come illustrato nei passaggi 3-8 della procedura precedente.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 2: Abilitazione e impostazione delle configurazioni dei pacchetti](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
  
