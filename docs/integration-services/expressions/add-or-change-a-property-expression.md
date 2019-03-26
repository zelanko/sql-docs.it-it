---
title: Aggiungere o modificare un'espressione di proprietà | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], creating
- expressions [Integration Services], property expressions
ms.assetid: cb5da499-065f-4fa6-9f6d-5bc5f385241e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d47462eeb7259b0289f7c554c0c6a4bd30dbb995
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275243"
---
# <a name="add-or-change-a-property-expression"></a>Aggiunta o modifica di un'espressione di proprietà
  È possibile creare espressioni di proprietà per pacchetti, attività, contenitori Ciclo Foreach, contenitori Ciclo For, contenitori Sequenza, gestori di eventi, gestioni connessioni a livello di pacchetto e progetto e provider di log.  
  
 Per creare o modificare espressioni di proprietà, è possibile usare l' **Editor espressioni di proprietà** o il **Generatore di espressioni**. È possibile accedere all' **Editor espressioni di proprietà** dagli editor personalizzati disponibili per attività e contenitori o dalla finestra **Proprietà** . È possibile accedere al**Generatore di espressioni** dall' **Editor espressioni di proprietà**. È possibile scrivere espressioni sia nell'**Editor espressioni di proprietà** che nel **Generatore di espressioni**, tuttavia **Generatore di espressioni** offre un set di strumenti dell'interfaccia grafica che semplificano la compilazione di espressioni complesse.  
  
 Per sapere di più sulla sintassi, gli operatori e le funzioni offerti da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md) e [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md). Gli argomenti relativi a ogni operatore e funzione includono esempi di utilizzo dell'operatore o della funzione in un'espressione. Per esempi di espressioni più complesse, vedere [Utilizzo delle espressioni di proprietà nei pacchetti](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
### <a name="to-create-or-change-a-property-expression"></a>Per creare o modificare un'espressione di proprietà  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto che contiene il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo e quindi eseguire una delle operazioni seguenti.  
  
    -   Nel caso di un'attività o di un contenitore, fare doppio clic sull'elemento e quindi su **Espressioni** nell'editor.  
  
    -   Fare clic con il pulsante destro del mouse sull'elemento e scegliere **Proprietà**.  
  
3.  Fare clic nella casella **Espressioni** e quindi sui puntini di sospensione (...).  
  
4.  Nell' **Editor espressioni di proprietà**selezionare una proprietà nell'elenco **Proprietà** ed eseguire una delle operazioni seguenti:  
  
    -   Digitare o modificare direttamente l'espressione di proprietà nella colonna **Espressione** , quindi fare clic su **OK**.  
  
         oppure  
  
    -   Fare clic sui puntini di sospensione (...) nella riga dell'espressione della proprietà per aprire il **Generatore di espressioni**.  
  
5.  (Facoltativo) Nel **Generatore di espressioni**, eseguire una delle attività seguenti:  
  
    -   Per accedere a variabili definite dal sistema e dall'utente, espandere **Variabili**.  
  
    -   Per accedere alle funzioni, ai cast e agli operatori del linguaggio delle espressioni di [!INCLUDE[ssIS](../../includes/ssis-md.md)] , espandere i nodi **Funzioni matematiche**, **Funzioni per i valori stringa**, **Funzioni di data/ora**, **Funzioni NULL**, **Cast di tipo**e **Operatori**.  
  
    -   Per compilare o modificare un'espressione nel **Generatore di espressioni**, trascinare le variabili, le colonne, le funzioni, gli operatori e i cast nella casella **Espressione** oppure digitare direttamente l'espressione nella casella.  
  
    -   Per visualizzare il risultato della valutazione dell'espressione, fare clic su **Valuta espressione** nel **Generatore di espressioni**.  
  
         Se l'espressione non è valida, viene visualizzato un avviso che evidenzia gli errori di sintassi.  
  
        > [!NOTE]  
        >  Quando si valuta un'espressione, il risultato della valutazione non viene assegnato alla proprietà.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni di Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)   
 [Utilizzo delle espressioni di proprietà nei pacchetti](../../integration-services/expressions/use-property-expressions-in-packages.md)   
 [Pacchetti di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md)   
 [Contenitori in Integration Services](../../integration-services/control-flow/integration-services-containers.md)   
 [Attività di Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Gestori eventi di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md)   
 [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Registrazione di Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
