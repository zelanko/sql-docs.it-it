---
title: 'Passaggio 3: Modificare la gestione connessione file flat | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1de57ab14dc4dcfc07f838494ca48f8b12da6660
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143561"
---
# <a name="lesson-2-3-modify-the-flat-file-connection-manager"></a>Lezione 2-3: Modificare la gestione connessione file flat

In questa attività viene modificata la gestione connessione file flat della lezione 1. Tale gestione connessione file flat era stata configurata per caricare staticamente un singolo file. Per abilitare la gestione connessione file flat affinché carichi i file in modo iterativo, modificare la proprietà ConnectionString della gestione connessione in modo che usi la variabile `User::varFileName` definita dall'utente contenente il percorso del file da caricare in fase di esecuzione.  
  
Modificando la gestione connessione in modo che usi il valore della variabile definita dall'utente per cambiare la proprietà ConnectionString, la gestione connessione si connette a file flat diversi. In fase di esecuzione, ogni iterazione del contenitore Ciclo Foreach determina l'aggiornamento della variabile `User::varFileName`. L'aggiornamento della variabile quindi consente alla gestione connessione di connettersi a un file flat diverso e all'attività Flusso di dati di elaborare un set di dati diverso.  
  
## <a name="configure-the-flat-file-connection-manager-to-use-a-variable"></a>Configurare la gestione connessione file flat in modo che usi una variabile  
  
1.  Nel riquadro **Gestioni connessioni** fare clic con il pulsante destro del mouse su **Sample Flat File Source Data**e scegliere **Proprietà**.  
  
2.  Nella finestra **Proprietà** fare clic sulla cella vuota relativa a **Espressioni** e fare clic sul pulsante con i puntini di sospensione **(...)**.  
  
3.  Nella colonna **Proprietà** della finestra di dialogo **Editor espressioni di proprietà** selezionare **ConnectionString**.  
  
4.  Nella colonna **Espressione** selezionare il pulsante con i puntini di sospensione **(...)** per aprire la finestra di dialogo **Generatore di espressioni**.  
  
5.  Nella finestra di dialogo **Generatore di espressioni** espandere il nodo **Variabili**.  
  
6.  Trascinare la variabile **User::varFileName** nella casella **Espressione**.  
  
7.  Selezionare **OK** per chiudere la finestra di dialogo **Generatore di espressioni**.  
  
8.  Selezionare nuovamente **OK** per chiudere la finestra di dialogo **Editor espressioni di proprietà**.  
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo  
[Passaggio 4: Testare il pacchetto creato nella lezione 2 dell'esercitazione](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
  
