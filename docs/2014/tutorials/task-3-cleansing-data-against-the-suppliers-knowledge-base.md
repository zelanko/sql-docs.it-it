---
title: 'Attività 3: Pulizia dei dati rispetto alla Knowledge Base Suppliers | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 647c924a-9b91-4294-8d96-e81416e4e90e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 53dde66e84dd7304f81c4b6fd7de8dbe939d22d4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250161"
---
# <a name="task-3-cleansing-data-against-the-suppliers-knowledge-base"></a>Attività 3: Pulizia dei dati fornitore rispetto alla Knowledge Base Suppliers
  In questa attività viene eseguito il processo di pulizia computerizzato. In DQS vengono utilizzati algoritmi e livelli di probabilità avanzati basati sui valori soglia specificati per analizzare i dati rispetto alla Knowledge Base selezionata e procedere quindi alla relativa pulizia. Visualizzare [pulizia dei dati mediante DQS (interna) Knowledge](https://msdn.microsoft.com/library/hh213061.aspx) per altri dettagli.  
  
1.  Fare clic su **avviare** per avviare il processo di pulizia computerizzato.  
  
     ![Pagina del processo di pulizia Pulisci](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-01.jpg "pulire pagina del processo di pulizia")  
  
2.  Quando viene completato il processo di pulizia, esaminare **statistiche** nel **Profiler** scheda. Le statistiche di origine specificare il numero di record elaborati, numero di record che risultano corrette, il numero di record che DQS consente di correggere, numero di record che hanno suggerite modifiche da DQS e il numero di record che non sono validi. Nella casella di riepilogo a destra è possibile visualizzare i valori corretti, quelli suggeriti, nonché la completezza (l'entità della presenza dei dati) e l'accuratezza (la misura entro cui i dati possono essere utilizzati per gli scopi previsti) dei valori per ogni dominio interessato dal processo di pulizia.  
  
     ![Risultati della pulizia](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-02.jpg "dei risultati della pulizia")  
  
3.  Fare clic su **successivo** per passare alla **Gestisci e Visualizza risultati** pagina.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 4: Gestione e visualizzazione dei risultati](../../2014/tutorials/task-4-manaing-and-viewing-results.md)  
  
  
