---
description: 'Lezione 5-1: Copiare il pacchetto della lezione 4'
title: 'Passaggio 1: Copiare il pacchetto della lezione 4 | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 95eca1c1b598387d7ff2c9bab688c022f76e73c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88345607"
---
# <a name="lesson-5-1-copy-the-lesson-4-package"></a>Lezione 5-1: Copiare il pacchetto della lezione 4

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



In questa attività si crea una copia del pacchetto **Lesson 4.dtsx** creato nella lezione 4. Se non è stata completata la lezione 4, è possibile aggiungere al progetto il pacchetto della lezione 4 completata incluso nell'esercitazione e quindi effettuarne una copia. Questa nuova copia verrà usata per tutto il seguito della lezione 5.  
  
## <a name="create-the-lesson-5-package"></a>Creare il pacchetto della lezione 5  
  
Attenersi alla procedura seguente se si sta copiando la lezione 4 completata.  Per copiare la lezione 4 di esempio, vedere la sezione successiva.

1.  Se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools non è già aperto, selezionare **Start** > **Tutti i programmi** > **Microsoft SQL Server 2017** e quindi selezionare **SQL Server Data Tools**.

2.  Nel menu **File** selezionare **Apri** > **Progetto/Soluzione**, selezionare la cartella **SSIS Tutorial** e selezionare **Apri**.  Quindi, fare doppio clic su **SSIS Tutorial.sln**.

3.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Lesson 4.dtsx** e quindi selezionare **Copia**.

4.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Pacchetti SSIS** e quindi selezionare **Incolla**.

    Il nome predefinito del pacchetto copiato è **Lesson 4.dtsx**.

5.  In **Esplora soluzioni** fare doppio clic su **Lesson 4.dtsx** per aprire il pacchetto.

6.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dell'area di progettazione **Flusso di controllo** e selezionare **Proprietà**.

7.  Nella finestra **Proprietà** aggiornare la proprietà **Name** impostandola su **Lesson 5**.

8.  Selezionare la casella relativa alla proprietà **ID**, fare clic sulla freccia a discesa e quindi selezionare **\<Generate New ID>** .

## <a name="add-the-completed-lesson-4-package"></a>Aggiungere il pacchetto della lezione 4 completato

1.  Aprire [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools e il progetto SSIS Tutorial.

2.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Pacchetti SSIS** e selezionare **Aggiungi pacchetto esistente**.

3.  Nella finestra di dialogo **Aggiungi copia del pacchetto esistente** , in **Posizione pacchetto**, selezionare **File system**.

4.  Selezionare il pulsante sfoglia **(...)** , passare a **Lesson 4.dtsx** nel computer e quindi selezionare **Apri**.

5.  Copiare e incollare il pacchetto della lezione 4, come illustrato nei passaggi 3-8 della sezione precedente.
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo  
[Passaggio 2: Abilitare e configurare le configurazioni di pacchetti](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
