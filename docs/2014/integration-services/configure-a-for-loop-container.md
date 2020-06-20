---
title: Configurare un contenitore ciclo for | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: b9cd7ea7-b198-4a35-8b16-6acf09611ca5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 24e2fe71b958395a5be35afad32804d2a748348d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921982"
---
# <a name="configure-a-for-loop-container"></a>Configurazione di un contenitore Ciclo For
  Questa procedura descrive come configurare un contenitore Ciclo For tramite la finestra di dialogo **Editor ciclo For** .  
  
### <a name="to-configure-the-for-loop-container"></a>Per configurare il contenitore Ciclo For  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare doppio clic sul contenitore Ciclo For per aprire la finestra di dialogo **Editor ciclo For**.  
  
2.  Facoltativamente, modificare il nome e la descrizione del contenitore Ciclo For.  
  
3.  Facoltativamente, digitare un'espressione di inizializzazione nella casella di testo **InitExpression** .  
  
4.  Digitare un'espressione di valutazione nella casella di testo **EvalExpression** .  
  
    > [!NOTE]  
    >  L'espressione deve restituire un valore booleano. Quando l'espressione restituisce `false`, l'esecuzione del ciclo viene arrestata.  
  
5.  Facoltativamente, digitare un'espressione di assegnazione nella casella di testo **AssignExpression** .  
  
6.  Facoltativamente, fare clic su **Espressioni** e, nella pagina **Espressioni** , creare espressioni di proprietà per le proprietà del contenitore Ciclo For. Per altre informazioni, vedere [Aggiunta o modifica di un'espressione di proprietà](expressions/add-or-change-a-property-expression.md).  
  
7.  Fare clic su **OK** per chiudere la finestra **Editor ciclo For**.  
  
## <a name="see-also"></a>Vedere anche  
 [Contenitore ciclo for](control-flow/for-loop-container.md)   
 [Integration Services &#40;espressioni di&#41; SSIS](expressions/integration-services-ssis-expressions.md)   
 [utilizzo delle espressioni di proprietà nei pacchetti](expressions/use-property-expressions-in-packages.md)  
  
  
