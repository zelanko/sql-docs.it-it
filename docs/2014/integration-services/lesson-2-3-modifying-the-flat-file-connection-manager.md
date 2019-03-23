---
title: 'Passaggio 3: Modifica della gestione connessione File Flat | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c251a77d0272e069d57b46940f8fcb06144653a0
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389699"
---
# <a name="step-3-modifying-the-flat-file-connection-manager"></a>Passaggio 3: Modifica della gestione connessione file flat
  In questa attività verrà modificata la gestione connessione file flat creata e configurata nella lezione 1. Al momento della creazione, la gestione connessione file flat era stata configurata per caricare staticamente un singolo file. Per abilitare Gestione connessione file flat affinché carichi i file in modo iterativo, è necessario modificare la proprietà ConnectionString della gestione connessione in modo che accetti la variabile `User:varFileName`definita dall'utente contenente il percorso del file da caricare in fase di esecuzione.  
  
 La modifica della gestione connessione in modo da usare il valore della variabile `User::varFileName`definita dall'utente per popolare la proprietà ConnectionString consente alla gestione connessione di connettersi a file flat diversi. In fase di esecuzione, ogni iterazione del contenitore Ciclo Foreach determina l'aggiornamento dinamico della variabile `User::varFileName` . L'aggiornamento della variabile quindi consente alla gestione connessione di connettersi a un file flat diverso e all'attività Flusso di dati di elaborare un set di dati diverso.  
  
### <a name="to-configure-the-flat-file-connection-manager-to-use-a-variable-for-the-connection-string"></a>Per configurare la gestione connessione file flat in modo da utilizzare una variabile per la stringa di connessione  
  
1.  Nel riquadro **Gestioni connessioni** fare clic con il pulsante destro del mouse su **Sample Flat File Source Data**e scegliere **Proprietà**.  
  
2.  Nella finestra Proprietà fare clic sulla cella vuota relativa a **Espressioni**e fare clic sul pulsante con i puntini di sospensione **(...)**.  
  
3.  Nel **Editor espressioni di proprietà** nella finestra di dialogo il **proprietà** colonna, digitare o selezionare `ConnectionString`.  
  
4.  Nella colonna **Espressione** fare clic sul pulsante con i puntini di sospensione **(...)** per aprire la finestra di dialogo **Generatore di espressioni**.  
  
5.  Nella finestra di dialogo **Generatore di espressioni** espandere il nodo **Variabili** .  
  
6.  Trascinare la variabile **User::varFileName**sulla casella **Espressione** .  
  
7.  Fare clic su **OK** per chiudere la finestra di dialogo **Generatore di espressioni** .  
  
8.  Fare nuovamente clic su **OK** per chiudere la finestra di dialogo **Editor espressioni di proprietà** .  
  
## <a name="next-lesson-task"></a>Attività della lezione successiva  
 [Passaggio 4: Test del pacchetto dell'esercitazione della lezione 2](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
