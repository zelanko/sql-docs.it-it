---
title: 'Attività 2 (facoltativo): Creazione di una vista sottoscrizioni MDS utilizzando Master Data Manager Documenti Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: cc923792adc3fefb5ebaab9e225169648394c71f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484711"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>Attività 2 (facoltativa): Creazione di viste sottoscrizioni MDS tramite Gestione dati master
  In questa attività viene creata una vista sottoscrizioni per esporre l'entità **Fornitore** nel modello **Fornitori** ad altre applicazioni. Questa vista non viene utilizzata nella versione corrente dell'esercitazione.  
  
1.  Passare alla pagina principale di`http://localhost/MDS`Master Data **Manager** ( ) facendo clic su SQL Server **2012 Master Data Services** nella parte superiore.  
  
2.  Fare clic su **Gestione integrazione**.  
  
3.  Fare clic su **Crea viste** sulla barra dei menu.  
  
     ![Pulsante Aggiungi nuova vista sottoscrizione](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "Pulsante Aggiungi nuova vista sottoscrizione")  
  
4.  Per creare una vista sottoscrizioni, fare clic sull'icona **(più)** sulla barra degli strumenti.  
  
5.  Nel riquadro **Crea vista sottoscrizioni** digitare **Fornitori** per **Nome vista sottoscrizioni**.  
  
6.  Selezionare **Fornitori** per **Modello**.  
  
7.  Selezionare **VERSION_1** per **Versione**.  
  
8.  Selezionare **Fornitore** per **Entità**.  
  
9. Selezionare **Membri foglia** per **Formato**.  
  
     ![Pulsante Salva vista sottoscrizione](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "Pulsante Salva vista sottoscrizione")  
  
10. Fare clic su **Salva** sulla barra degli strumenti per salvare la vista sottoscrizioni. Questa azione consente di creare una vista in SQL Server denominata **Suppliers**. Per verificarla, utilizzare SQL Server Management Studio (SSMS).  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 3 &#40;&#41; facoltative: Revisione delle visualizzazioni sottoscrizioniTask 3 to Optional&#41;: Reviewing the Subscription Views](task-3-optional-reviewing-the-subscription-views.md)  
  
  
