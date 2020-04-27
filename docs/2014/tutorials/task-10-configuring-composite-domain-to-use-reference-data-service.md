---
title: "Attività 10: configurazione del dominio composito per l'utilizzo del servizio dati di riferimento | Microsoft Docs"
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 525e0286d8d82f501981c9e936caca581886b9b4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65481233"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>Attività 10: Configurazione del dominio composito per usare il servizio dati di riferimento
  In questa attività viene configurato il dominio composito **Address Validation** per usare il servizio **Melissa Data-Address Check** . In fase di esecuzione, durante l'attività di pulizia, tramite DQS i valori del dominio Address Validation vengono passati al servizio per la pulizia. Per altri dettagli, vedere [eseguire il mapping di dominio/dominio composito ai dati di riferimento](https://msdn.microsoft.com/library/hh213030.aspx) .  
  
1.  Nella pagina principale del **client DQS**fare clic su **suppliers (Domain Management)** in **Knowledge Base recenti** per avviare la pagina di **gestione del dominio** .  
  
2.  Selezionare il dominio composito **Address Validation** nell' **elenco dei domini**.  
  
3.  Nel riquadro destro passare alla scheda dati di **riferimento** .  
  
     ![Scheda Dati di riferimento](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "Scheda Dati di riferimento")  
  
4.  Fare clic sul pulsante **Sfoglia** sulla barra degli strumenti.  
  
5.  Nella finestra di dialogo **Catalogo dei provider di dati di riferimento online** selezionare la **casella di controllo** accanto a **Melissa Data-verifica indirizzo**.  
  
     ![Selezione di Melissa Data - Controllo indirizzo](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "Selezione di Melissa Data - Controllo indirizzo")  
  
6.  Nel riquadro destro, nella sezione **schema** , eseguire il mapping del dominio della **linea di indirizzo** all'elemento dello schema della **riga dell'indirizzo (M)** utilizzando l'elenco a discesa.  
  
     ![Esecuzione del mapping della voce Schema servizio dati di riferimento al dominio](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "Esecuzione del mapping della voce Schema servizio dati di riferimento al dominio")  
  
7.  Fare clic sul pulsante **Aggiungi voce di schema (+)** nella barra degli strumenti per creare una voce nell'elenco.  
  
     ![Pulsante della barra degli strumenti Aggiungi voce di schema](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "Pulsante della barra degli strumenti Aggiungi voce di schema")  
  
8.  Eseguire il mapping dei domini DQS utilizzando gli elenchi a discesa come illustrato nella figura seguente.  
  
     ![Esecuzione del mapping delle voci Schema servizio dati di riferimento a domini](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "Esecuzione del mapping delle voci Schema servizio dati di riferimento a domini")  
  
9. Fare clic su **OK** per chiudere la finestra di dialogo.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 11: Pubblicazione della Knowledge Base](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  
