---
title: 'Passaggio 1: Copiare il pacchetto della lezione 5 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2c4c895e71da13d7de38bf5dfc64f27829206d25
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283119"
---
# <a name="lesson-6-1-copy-the-lesson-5-package"></a>Lezione 6-1: Copiare il pacchetto della lezione 5

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



In questa attività si crea una copia del pacchetto **Lesson 5.dtsx** creato nella lezione 5. Se non è stata completata la lezione 5, è possibile aggiungere al progetto il pacchetto completo della lezione 5 incluso nell'esercitazione e quindi effettuarne una copia. Questa nuova copia verrà usata per tutto il seguito della lezione 6. 

> [!IMPORTANT]
> Dopo la copia del pacchetto della lezione 5, se attualmente si usano i pacchetti delle lezioni precedenti nella soluzione, fare clic con il pulsante destro del mouse su ogni pacchetto delle lezioni da 1 a 5 e selezionare **Escludi dal progetto**. Al termine la soluzione deve contenere solo il pacchetto **Lesson 6.dtsx**.   
  
## <a name="create-the-lesson-6-package"></a>Creare il pacchetto della lezione 6  
  
Attenersi alla procedura seguente se si sta copiando la lezione 5 completata.  Per copiare la lezione 5 di esempio, vedere la sezione successiva.

1.  Se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools non è già aperto, selezionare **Start** > **Tutti i programmi** > **Microsoft SQL Server 2017** e quindi selezionare **SQL Server Data Tools**.

2.  Nel menu **File** selezionare **Apri** > **Progetto/Soluzione**, selezionare la cartella **Esercitazione SSIS** e quindi **Apri** e fare doppio clic su **SSIS Tutorial.sln**.

3.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Lesson 5.dtsx** e quindi selezionare **Copia**.

4.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Pacchetti SSIS** e quindi selezionare **Incolla**.

    Il nome predefinito del pacchetto copiato è **Lesson 5.dtsx**.

5.  In **Esplora soluzioni** fare doppio clic su **Lesson 5.dtsx** per aprire il pacchetto

6.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dell'area di progettazione **Flusso di controllo** e selezionare **Proprietà**.

7.  Nella finestra **Proprietà** aggiornare la proprietà **Name** impostandola su **Lesson 6**.

8.  Selezionare la casella relativa alla proprietà **ID**, fare clic sulla freccia a discesa e quindi selezionare **\<Genera nuovo ID>** .

## <a name="add-the-completed-lesson-5-package"></a>Aggiungere il pacchetto della lezione 5 completato

1.  Aprire [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools e il progetto SSIS Tutorial.

2.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Pacchetti SSIS** e selezionare **Aggiungi pacchetto esistente**.

3.  Nella finestra di dialogo **Aggiungi copia del pacchetto esistente** , in **Posizione pacchetto**, selezionare **File system**.

4.  Selezionare il pulsante sfoglia **(...)** , passare a **Lesson 5.dtsx** nel computer e quindi selezionare **Apri**.

5.  Copiare e incollare il pacchetto della lezione 5, come illustrato nei passaggi 3-8 della sezione precedente.

## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo
[Passaggio 2: Convertire il progetto nel modello di distribuzione del progetto](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
