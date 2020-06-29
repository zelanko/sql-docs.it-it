---
title: Editor vincoli di precedenza | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.precedenceconstraint.f1
helpviewer_keywords:
- Precedence Constraint Editor dialog box
ms.assetid: b10d4330-6e35-4037-b309-ef56efcd60c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ba2c9c0c870294069dd1feb4eaabb72211877cc4
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423198"
---
# <a name="precedence-constraint-editor"></a>Editor vincoli di precedenza
  Utilizzare la finestra di dialogo **Editor vincoli di precedenza** per configurare i vincoli di precedenza.  
  
## <a name="options"></a>Opzioni  
 **Operazione di valutazione**  
 Consente di specificare l'operazione di valutazione utilizzata dal vincolo di precedenza. Le operazioni sono **Vincolo**, **Espressione**, **Espressione e vincolo**e **Espressione o vincolo**.  
  
 **Valore**  
 Consente di specificare il valore di vincolo, ovvero **Operazione completata**, **Errore**oppure **Completamento**.  
  
> [!NOTE]  
>   La riga del vincolo di precedenza è di colore verde in caso di **Esito positivo**, evidenziata per **Esito negativo**e blu per **Completamento**.  
  
 **Expression**  
 Se si usano le operazioni **Espressione**, **Espressione e vincolo**o **Espressione o vincolo**, digitare un'espressione o avviare Generatore di espressioni per creare l'espressione. L'espressione deve restituire un valore booleano.  
  
 **Test**  
 Consente di convalidare l'espressione.  
  
 **AND logico**  
 Selezionare questa opzione per specificare che devono essere valutati contemporaneamente più vincoli di precedenza nello stesso file eseguibile. Tutti i vincoli devono restituire `True`.  
  
> [!NOTE]  
>  Questo tipo di vincolo di precedenza viene visualizzato come riga di colore verde, evidenziata o blu continua.  
  
 **OR logico**  
 Selezionare questa opzione per specificare che devono essere valutati contemporaneamente più vincoli di precedenza nello stesso file eseguibile. Almeno un vincolo deve restituire `True`.  
  
> [!NOTE]  
>  Questo tipo di vincolo di precedenza viene visualizzato come riga di colore verde, evidenziata o blu tratteggiata.  
  
## <a name="see-also"></a>Vedere anche  
 [Vincoli di precedenza](control-flow/precedence-constraints.md)   
 [Attività Integration Services](control-flow/integration-services-tasks.md)   
 [Contenitori di Integration Services](control-flow/integration-services-containers.md)   
 [Espressioni di Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md)  
  
  
