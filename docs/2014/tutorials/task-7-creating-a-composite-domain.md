---
title: 'Attività 7: Creazione di un dominio composito | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c48144ca3720565c3c745ffd8aa39b0896e1fb66
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62866284"
---
# <a name="task-7-creating-a-composite-domain"></a>Attività 7: Creazione di un dominio composito
  In questa attività si crea un dominio composito, **Address Validation**, che comprende **Address Line**, **City**, **stato**e  **Codice postale** domini. Un dominio composito consente di definire una regola tra domini che interessa più domini di una regola. Vi sono altri vantaggi correlati a un dominio composito, quale la possibilità di analizzare un valore di campo in più domini.  Ad esempio, un valore per un campo Nome completo può essere analizzato in domini diversi First Name, Middle Name e Last Name. In questa esercitazione viene definita solo una regola tra domini. Visualizzare [Managing a Composite Domain](https://msdn.microsoft.com/library/hh510399.aspx) per altri dettagli.  
  
1.  Nel riquadro sinistro, fare clic su **crea un dominio composito** pulsante sulla barra degli strumenti.  
  
     ![Creare un pulsante della barra degli strumenti di dominio composito](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "creare un pulsante della barra degli strumenti di dominio composito")  
  
2.  Immettere **indirizzi convalida** per il **nome dominio composito**.  
  
     ![Risolvere la convalida dominio composito](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "risolvere la convalida dominio composito")  
  
3.  Dall'elenco di domini selezionare **Address Line**, **City**, **stato**, e **codice postale** e fare clic su **freccia destra** per aggiungerle al **domini nel dominio composito** elenco.  
  
4.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 8: Creazione di una regola dominio composito](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  
