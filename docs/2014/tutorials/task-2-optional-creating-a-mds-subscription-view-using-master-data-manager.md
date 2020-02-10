---
title: 'Attività 2 (facoltativo): creazione di una vista sottoscrizioni MDS con Gestione dati master | Microsoft Docs'
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
ms.openlocfilehash: e6cbed42d059714dde1c82dbb50edf8ccc1dd65b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484721"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>Attività 2 (facoltativa): Creazione di viste sottoscrizioni MDS tramite Gestione dati master
  In questa attività viene creata una vista sottoscrizioni per esporre l'entità **Supplier** nel modello **Suppliers** ad altre applicazioni. Questa vista non viene utilizzata nella versione corrente dell'esercitazione.  
  
1.  Passare alla pagina principale di **Gestione dati master** ([http://localhost/MDS](http://localhost/MDS)) facendo clic **SQL Server Master Data Services 2012** nella parte superiore.  
  
2.  Fare clic su **Gestione integrazione**.  
  
3.  Fare clic su **Crea viste** sulla barra dei menu.  
  
     ![Pulsante Aggiungi nuova vista sottoscrizione](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "Pulsante Aggiungi nuova vista sottoscrizione")  
  
4.  Fare clic sull'icona **+ (segno più)** sulla barra degli strumenti per creare una vista sottoscrizioni.  
  
5.  Nel riquadro **Crea vista sottoscrizioni** digitare **Suppliers** per **nome vista**sottoscrizioni.  
  
6.  Selezionare **Suppliers** per **modello**.  
  
7.  Selezionare **VERSION_1** per **versione**.  
  
8.  Selezionare **Supplier** per **Entity**.  
  
9. Selezionare **membri foglia** per **formato**.  
  
     ![Pulsante Salva vista sottoscrizione](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "Pulsante Salva vista sottoscrizione")  
  
10. Fare clic su **Salva** sulla barra degli strumenti per salvare la vista sottoscrizioni. Questa azione consente di creare una vista in SQL Server **Suppliers**. Per verificarla, utilizzare SQL Server Management Studio (SSMS).  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 3 &#40;&#41; facoltativo: Revisione delle viste sottoscrizioni](task-3-optional-reviewing-the-subscription-views.md)  
  
  
