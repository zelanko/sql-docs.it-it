---
title: 'Attività 7: creazione di un dominio composito | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 42936d25e267bcad5ba8ae512750f9e12f041579
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064723"
---
# <a name="task-7-creating-a-composite-domain"></a>Attività 7: Creazione di un dominio composito
  In questa attività viene creato un dominio composito, la **convalida dell'indirizzo**, che include i domini della riga dell' **Indirizzo**, **della città**, **dello stato**e del file **zip** . Un dominio composito consente di definire una regola tra domini che interessa più domini di una regola. Vi sono altri vantaggi correlati a un dominio composito, quale la possibilità di analizzare un valore di campo in più domini.  Ad esempio, un valore per un campo Nome completo può essere analizzato in domini diversi First Name, Middle Name e Last Name. In questa esercitazione viene definita solo una regola tra domini. Per altri dettagli, vedere [gestione di un dominio composito](https://msdn.microsoft.com/library/hh510399.aspx) .  
  
1.  Nel riquadro sinistro fare clic sul pulsante **Crea un dominio composito** sulla barra degli strumenti.  
  
     ![Pulsante della barra degli strumenti Crea un dominio composito](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "Pulsante della barra degli strumenti Crea un dominio composito")  
  
2.  Immettere la **convalida degli indirizzi** per il nome di **dominio composito**.  
  
     ![Dominio composito di convalida indirizzi](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "Dominio composito di convalida indirizzi")  
  
3.  Dall'elenco di domini selezionare **Indirizzo riga**, **città**, **stato**e **Cap** , quindi fare clic sulla **freccia destra** per aggiungerli all'elenco **domini in domini compositi** .  
  
4.  Fare clic su **OK** per chiudere la finestra di dialogo.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 8: Creazione di una regola per un dominio composito](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  
