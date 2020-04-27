---
title: 'Attività 9: creazione di una gerarchia derivata utilizzando Gestione dati master | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7cb2f12115e3fe743c49c2f7e69f765da4501ba2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489529"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>Attività 9: Creazione di una gerarchia derivata tramite Gestione dati master
  In questa attività viene creata una gerarchia derivata mediante Gestione dati master. Questa gerarchia derivata è derivata dalle relazioni tra attributi basati su dominio tra le entità **Supplier** e **state** .  
  
1.  Passare alla pagina principale di **Gestione dati master** facendo clic **SQL Server Master Data Services 2012** nella parte superiore della pagina.  
  
2.  Fare clic su **Amministrazione sistema** nella sezione **attività amministrative** .  
  
3.  Posizionare il mouse su **Gestisci** sulla barra dei menu e fare clic su **gerarchie derivate**.  
  
     ![Menu Gestisci - Gerarchie derivate selezionate](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "Menu Gestisci - Gerarchie derivate selezionate")  
  
4.  Sulla barra degli strumenti fare clic sul pulsante **Aggiungi gerarchia derivata (+)** .  
  
     ![Pulsante Aggiungi gerarchia derivata](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "Pulsante Aggiungi gerarchia derivata")  
  
5.  Digitare **SuppliersInState** per il **nome della gerarchia derivata**.  
  
6.  Fare clic sul pulsante **Salva** sulla barra degli strumenti.  
  
     ![Pulsante Salva gerarchia derivata](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "Pulsante Salva gerarchia derivata")  
  
7.  Trascinare **Supplier** da **livelli disponibili: SuppliersInState** a **livelli correnti: SuppliersInState**.  
  
     ![Entità e gerarchie disponibili a livello corrente](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "Entità e gerarchie disponibili a livello corrente")  
  
8.  Trascinare **lo stato** da **livelli disponibili: SuppliersInState** a **livelli correnti: SuppliersInState**. La schermata deve avere **livelli correnti** , come illustrato nell'immagine seguente.  
  
     ![Livelli correnti e anteprima della gerarchia derivata](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "Livelli correnti e anteprima della gerarchia derivata")  
  
9. Nella finestra di **Anteprima** , espandere **NY {New York}** . verrà visualizzato un fornitore in tale stato, come illustrato nell'immagine precedente.  
  
10. Passare alla pagina principale di **Gestione dati master** facendo clic **SQL Server Master Data Services 2012** nella parte superiore della pagina.  
  
11. Fare clic su **Esplora**.  
  
12. Posizionare il puntatore del mouse su **gerarchie** e fare clic su **derivato: SuppliersInState**.  
  
     ![Gerarchie - Menu Derived:SuppliersInState](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "Gerarchie - Menu Derived:SuppliersInState")  
  
13. Fare clic su un nodo di **stato** nella **visualizzazione albero** per visualizzare i fornitori in tale stato nel riquadro di destra.  
  
     ![Gerarchia derivata in Esplora](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "Gerarchia derivata in Esplora")  
  
## <a name="next-step"></a>passaggio successivo  
 [Lezione 5: Automazione della pulizia e della corrispondenza tramite SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  
