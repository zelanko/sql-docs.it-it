---
title: 'Attività 3: pulizia dei dati rispetto alla Knowledge Base Suppliers | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 647c924a-9b91-4294-8d96-e81416e4e90e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: b13e3d30ac0afce5293cc0e104aa2b291112647f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177281"
---
# <a name="task-3-cleansing-data-against-the-suppliers-knowledge-base"></a>Attività 3: Pulizia dei dati fornitore rispetto alla Knowledge Base Suppliers
  In questa attività viene eseguito il processo di pulizia computerizzato. In DQS vengono utilizzati algoritmi e livelli di probabilità avanzati basati sui valori soglia specificati per analizzare i dati rispetto alla Knowledge Base selezionata e procedere quindi alla relativa pulizia. Per ulteriori informazioni, vedere [pulizia dei dati tramite la Knowledge Base DQS (interna)](https://msdn.microsoft.com/library/hh213061.aspx) .

1.  Fare clic su **Avvia** per avviare il processo di pulizia computerizzato.

     ![Pagina Pulisci del processo di pulizia](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-01.jpg "Pagina Pulisci del processo di pulizia")

2.  Al termine del processo di pulizia, verificare le **statistiche** nella scheda **Profiler** . Le statistiche di origine forniscono il numero di record elaborati, il numero di record risultanti corretti, il numero di record corretti da DQS, il numero di record che presentano modifiche suggerite da DQS e il numero di record non validi. Nella casella di riepilogo a destra è possibile visualizzare i valori corretti, quelli suggeriti, nonché la completezza (l'entità della presenza dei dati) e l'accuratezza (la misura entro cui i dati possono essere utilizzati per gli scopi previsti) dei valori per ogni dominio interessato dal processo di pulizia.

     ![Risultati della pulizia](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-02.jpg "Risultati della pulizia")

3.  Fare clic su **Avanti** per passare alla pagina **Gestisci e visualizza risultati** .

## <a name="next-step"></a>passaggio successivo
 [Attività 4: Gestione e visualizzazione dei risultati](../../2014/tutorials/task-4-manaing-and-viewing-results.md)


