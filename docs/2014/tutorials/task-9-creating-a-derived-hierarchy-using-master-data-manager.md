---
title: 'Attività 9: Creazione di una gerarchia derivata mediante gestione dati Master | Microsoft Docs'
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
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489529"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>Attività 9: Creazione di una gerarchia derivata tramite Gestione dati master
  In questa attività viene creata una gerarchia derivata mediante Gestione dati master. Questa gerarchia derivata viene ricavata dalle relazioni tra attributi basati su dominio tra il **Supplier** e **stato** entità.  
  
1.  Passare alla pagina principale del **gestione dati Master** facendo clic **SQL Server 2012 Master Data Services** nella parte superiore della pagina.  
  
2.  Fare clic su **Amministrazione sistema** nel **le attività amministrative** sezione.  
  
3.  Posizionare il mouse sopra **Manage** nella barra dei menu e fare clic su **gerarchie derivate**.  
  
     ![Menu Gestisci - gerarchie derivate selezionate](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "Menu Gestisci - gerarchie derivate selezionate")  
  
4.  Fare clic su **Aggiungi gerarchia derivata (+)** pulsante sulla barra degli strumenti.  
  
     ![Pulsante Aggiungi gerarchia derivata](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "pulsante Aggiungi gerarchia derivata")  
  
5.  Tipo di **SuppliersInState** per il **nome gerarchia derivata**.  
  
6.  Fare clic su **salvare** pulsante sulla barra degli strumenti.  
  
     ![Salva derivata pulsante della gerarchia](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "Salva derivata pulsante della gerarchia")  
  
7.  Trascinare **Supplier** da **livelli disponibili: SuppliersInState** a **livelli correnti: SuppliersInState**.  
  
     ![Entità e gerarchie al livello corrente disponibili](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "entità e gerarchie al livello corrente disponibili")  
  
8.  Trascinare **lo stato** da **livelli disponibili: SuppliersInState** a **livelli correnti: SuppliersInState**. Nella schermata debba già **livelli correnti** come illustrato nell'immagine seguente.  
  
     ![Livelli correnti e anteprima della gerarchia derivata](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "livelli correnti e anteprima della gerarchia derivata")  
  
9. Nel **Preview** finestra, espandere **NY {New York}** dovrebbe essere possibile visualizzare un fornitore di quello stato come illustrato nell'immagine precedente.  
  
10. Passare alla pagina principale del **gestione dati Master** facendo clic **SQL Server 2012 Master Data Services** nella parte superiore della pagina.  
  
11. Fare clic su **Esplora**.  
  
12. Posizionare il mouse sopra **gerarchie** e fare clic su **Derived: SuppliersInState**.  
  
     ![Gerarchie - derivate: Menu SuppliersInState](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "- gerarchie derivate: SuppliersInState Menu")  
  
13. Fare clic su qualsiasi **lo stato** nodo il **visualizzazione ad albero** dovrebbe essere possibile visualizzare i fornitori dello stato nel riquadro di destra.  
  
     ![In Esplora gerarchia derivata](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "Esplora gerarchia derivata")  
  
## <a name="next-step"></a>Passaggio successivo  
 [Lezione 5: Automatizzazione della pulizia e corrispondenza tramite SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  
