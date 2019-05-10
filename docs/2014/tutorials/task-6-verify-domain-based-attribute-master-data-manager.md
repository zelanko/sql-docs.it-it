---
title: "Attività 6: Verificare che l'attributo basato su dominio viene creato tramite Gestione dati Master | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6e90517a-910c-4c33-8f11-92ac3cff4fdc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: fe3f404d4f41e2977ef389216dcbc9106327266a
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488956"
---
# <a name="task-6-verify-that-the-domain-based-attribute-is-created-using-master-data-manager"></a>Attività 6: Verifica della creazione dell'attributo basato su dominio tramite Gestione dati master
  In questa attività si verifica che l'entità **State** venga creata in **MDS** e che l'attributo **State** dell'entità **Supplier** sia un attributo basato su dominio che dipende dall'entità **State** tramite **Gestione dati master**.  
  
1.  Passare all'applicazione Web **Gestione dati master**.  
  
2.  Fare clic su **SQL Server 2012 Master Data Services** in alto per tornare alla home page.  
  
3.  Assicurarsi che il modello **Suppliers** sia selezionato e fare clic su **Esplora risorse**. Se **Esplora risorse** è già aperto è possibile aggiornare la pagina.  
  
4.  Posizionare il mouse sopra **entità** nella barra dei menu e si noti che ora sono presenti due entità: **Supplier** e **stato**.  
  
     ![Menu entità con stato e fornitore](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-01.jpg "Menu entità con stato e fornitore")  
  
5.  Fare clic su **State** se l'entità non è già aperta.  
  
6.  Selezionare **GA** nell'elenco.  
  
7.  Nel riquadro **Dettagli** a destra modificare il **Nome** in **Georgia** nel **riquadro destro** e fare clic su **OK**.  
  
8.  Ripetere i passaggi precedenti per gli altri stati.  
  
    |Codice|nome|  
    |----------|----------|  
    |CA|California|  
    |CO|Colorado|  
    |IL|Illinois|  
    |DC|District of Columbia|  
    |FL|Florida|  
    |AL|Alabama|  
    |KY|Kentucky|  
    |MA|Massachusetts|  
    |AZ|Arizona|  
    |MI|Michigan|  
    |MN|Minnesota|  
    |NJ|New Jersey|  
    |NV|Nevada|  
    |NY|New York|  
    |OH|Ohio|  
    |OK|Oklahoma|  
    |o|Oregon|  
    |PA|Pennsylvania|  
    |SC|South Carolina|  
    |KS|Kansas|  
    |TN|Tennessee|  
    |TX|Texas|  
    |UT|Utah|  
    |VA|Virginia|  
    |WA|Washington|  
    |WI|Wisconsin|  
    |HI|Hawaii|  
    |MD|Maryland|  
    |CT|Connecticut|  
  
9. Selezionare una delle voci degli stati e fare clic su **Visualizza transazioni** nella barra degli strumenti. La transazione per l'aggiornamento appena effettuato viene visualizzata nell'elenco di transazioni.  
  
10. Passare il puntatore sul menu **Entità** e fare clic su **Supplier**.  
  
11. A questo punto si noti che un valore per il campo **Stato** può essere modificato nel riquadro **Dettagli** tramite l'elenco a discesa. È anche possibile osservare che, nell'elenco a sinistra e nell'elenco a discesa nel riquadro **Dettagli**, viene prima visualizzato il codice e poi il nome tra parentesi graffe. È possibile modificare anche qualsiasi altro valore nel riquadro **Dettagli**.  
  
     ![Stato attributo con codici e nomi aggiornati](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-02.jpg "stato attributo con codici e nomi aggiornati")  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 7: Visualizzazione degli aggiornamenti eseguiti tramite Gestione dati Master in Excel](../../2014/tutorials/task-7-viewing-updates-made-using-master-data-manager-in-excel.md)  
  
  
