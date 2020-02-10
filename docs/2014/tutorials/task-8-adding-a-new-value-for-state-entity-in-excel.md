---
title: "Attività 8: aggiunta di un nuovo valore per l'entità state in Excel | Microsoft Docs"
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 831d0b504a65d485413772ee3711e689e29ee2a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489703"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>Attività 8: Aggiunta di un nuovo valore per l'entità State in Excel
  In questa attività viene aggiunto un valore per l'entità State in Excel e viene pubblicata la modifica nel server MDS.  
  
1.  Per aggiungere un **foglio di lavoro** in Excel, fare clic sulla scheda nuovo nella parte inferiore.  
  
     ![Excel - Scheda Nuovo foglio di lavoro](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel - Scheda Nuovo foglio di lavoro")  
  
2.  In **Excel**fare clic sulla scheda **dati master** nel menu, quindi fare clic su **Mostra Esplora** sulla barra multifunzione.  
  
3.  Nel **Esplora dati master**selezionare **Suppliers** per **modello**. Verranno visualizzate due entità: **Supplier** e **state** nell'elenco di entità.  
  
4.  Fare doppio clic su **stato** nell'elenco. Tutti i membri dell'entità **stato** da MDS devono essere visualizzati nel foglio di foglio.  
  
5.  A questo punto, aggiungere una riga alla fine con i valori seguenti: **North Carolina** per **nome** e **NC** per il **codice**. La codifica tramite colori consente di differenziare tutti i record nuovi/aggiornati dagli altri record.  
  
     ![Excel - Aggiungi Nord Carolina agli Stati](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel - Aggiungi Nord Carolina agli Stati")  
  
6.  Fare clic su **pubblica** sulla barra multifunzione per pubblicare la modifica in MDS.  
  
     ![Excel - Pulsante Pubblica nella scheda Dati master](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel - Pulsante Pubblica nella scheda Dati master")  
  
7.  Nella finestra di dialogo **pubblica e annota** si noti che è selezionata l'opzione **Usa la stessa annotazione per tutte le modifiche** . È possibile specificare una sola annotazione per tutte le modifiche apportate in questo punto.  
  
8.  Selezionare l'opzione **Controlla modifiche e fornisci annotazioni singolarmente** per specificare l'annotazione per ogni modifica (in questo caso, solo una).  
  
     ![Excel - Finestra di dialogo Pubblicazione e annotazione](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "Excel - Finestra di dialogo Pubblicazione e annotazione")  
  
9. Fare clic su **pubblica** per pubblicare i dati in MDS.  
  
10. Si noti che la **codifica a colori** per la riga con **North Carolina** come **stato** corrisponde a quella degli altri record ora.  
  
11. **Facoltativo:** Verificare che il nuovo membro (NC) venga aggiunto all'entità **state** utilizzando **esplora risorse** in **Gestione dati master**.  
  
12. In Excel, fare clic con il pulsante destro del mouse sul foglio di lavoro **stato** in basso e fare clic su **Elimina** per eliminare il foglio di lavoro. L'eliminazione del foglio di lavoro non comporta l'eliminazione dei dati dal server MDS.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 9: Creazione di una gerarchia derivata mediante Gestione dati master](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  
