---
title: 'Attività 2 (facoltativa): Creazione di viste sottoscrizioni MDS tramite Gestione dati Master | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4596485b4eebeba66028d03f5a54b3ee2461205b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56015282"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>Attività 2 (facoltativa): Creazione di viste sottoscrizioni MDS tramite Gestione dati master
  In questa attività si crea una vista sottoscrizioni per esporre il **Supplier** entità nel **Suppliers** modello ad altre applicazioni. Questa vista non viene utilizzata nella versione corrente dell'esercitazione.  
  
1.  Passare alla pagina principale del **gestione dati Master** ([http://localhost/MDS](http://localhost/MDS)), fare clic su **SQL Server 2012 Master Data Services** nella parte superiore.  
  
2.  Fare clic su **Gestione integrazione**.  
  
3.  Fare clic su **creare visualizzazioni** nella barra dei menu.  
  
     ![Aggiungere un nuovo pulsante di visualizzazione di abbonamento](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "aggiungere un nuovo pulsante di visualizzazione di sottoscrizione")  
  
4.  Fare clic su **+ (segno più)** icona sulla barra degli strumenti per creare una vista sottoscrizioni.  
  
5.  Nel **Crea vista sottoscrizioni** riquadro, digitare **Suppliers** per **nome vista sottoscrizioni**.  
  
6.  Selezionare **Suppliers** per **modello**.  
  
7.  Selezionare **VERSION_1** per **versione**.  
  
8.  Selezionare **Supplier** per **entità**.  
  
9. Selezionare **i membri foglia** per **formato**.  
  
     ![Pulsante Salva vista sottoscrizione](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "pulsante Salva vista sottoscrizione")  
  
10. Fare clic su **salvare** sulla barra degli strumenti per salvare la vista sottoscrizioni. Questa azione consente di creare una vista in SQL Server denominata **Suppliers**. Per verificarla, utilizzare SQL Server Management Studio (SSMS).  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 3 &#40;facoltativo&#41;: Verifica delle viste sottoscrizioni](task-3-optional-reviewing-the-subscription-views.md)  
  
  
