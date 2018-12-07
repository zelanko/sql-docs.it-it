---
title: 'Passaggio 1: Copia del pacchetto della lezione 5 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b7d58507dac1d1071f0b546e0610f39381b648de
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52501810"
---
# <a name="lesson-6-1---copying-the-lesson-5-package"></a>Lezione 6-1 - Copia del pacchetto della lezione 5
In questa attività si procederà alla creazione di una copia del pacchetto della lezione 5, denominato Lesson 5.dtsx. In alternativa, è possibile aggiungere al progetto il pacchetto completo della lezione 5 incluso nell'esercitazione e, successivamente, copiarlo. Questa nuova copia verrà utilizzata per tutto il seguito della lezione 6.  
  
### <a name="to-copy-the-lesson-5-package"></a>Per copiare il pacchetto della lezione 5  
  
1.  Se SQL Server Data Tools non è già aperto, fare clic sul pulsante Start, scegliere Tutti i programmi, Microsoft SQL Server 2012, quindi selezionare SQL Server Data Tools.  
  
2.  Scegliere Apri dal menu File, fare clic su Progetto/Soluzione, selezionare SSIS Tutorial fare clic su Apri, quindi fare doppio clic su SSIS Tutorial.sln.  
  
3.  In Esplora soluzioni fare clic con il pulsante destro del mouse su Lesson 5.dtsx e quindi scegliere Copia.  
  
4.  In Esplora soluzioni fare clic con il pulsante destro del mouse su Pacchetti SSIS e quindi scegliere Incolla.  
  
    Per impostazione predefinita, il pacchetto copiato viene denominato Lesson 6.dtsx.  
  
5.  In Esplora soluzioni fare doppio clic su Lesson 6.dtsx per aprire il pacchetto.  
  
6.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dello sfondo della scheda Flusso di controllo e scegliere Proprietà.  
  
7.  Nella finestra Proprietà aggiornare la proprietà Name impostandola su Lesson 6.  
  
8.  Fare clic sulla casella relativa alla proprietà ID, fare clic sulla freccia a discesa, quindi scegliere <Generate New ID>.  
  
### <a name="to-add-the-completed-lesson-5-package"></a>Per aggiungere il pacchetto della lezione 5 completato  
  
1.  Aprire SQL Server Data Tools e il progetto SSIS Tutorial.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse su Pacchetti SSIS e scegliere Aggiungi pacchetto esistente.  
  
3.  Nella finestra di dialogo Aggiungi copia del pacchetto esistente, in Posizione pacchetto, selezionare File system.  
  
4.  Fare clic sul pulsante Sfoglia (...), passare a Lesson 5.dtsx nel computer e quindi fare clic su **Apri**.  
  
    Per scaricare tutti i pacchetti di lezioni di questa esercitazione, effettuare le operazioni seguenti.  
  
    1.  Passare alla pagina degli [esempi del prodotto di Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Fare clic sulla scheda **DOWNLOADS** .  
  
    3.  Fare clic sul file SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copiare e incollare il pacchetto della lezione 5, come illustrato nei passaggi 3-8 della procedura precedente.  
  
    Dopo la copia del pacchetto della lezione 5, se si dispone dei pacchetti delle lezioni precedenti nella soluzione, fare clic con il pulsante destro del mouse su ogni pacchetto delle lezioni 1-5 e fare clic su Escludi dal progetto. Al termine sarà presente un solo pacchetto Lesson 6.dtsx nella soluzione.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
[Passaggio 2: Conversione del progetto nel modello di distribuzione del progetto](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
