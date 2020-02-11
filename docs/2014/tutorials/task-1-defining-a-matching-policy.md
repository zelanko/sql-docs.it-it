---
title: 'Attività 1: definizione di criteri di corrispondenza | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6f89a720-fce5-4f60-bef3-a159bbc9f25c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3e4777cf05e7f3eab62c389ace8b8d8a96cae304
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65481309"
---
# <a name="task-1-defining-a-matching-policy"></a>Attività 1: Definizione di criteri di corrispondenza
  In questa attività vengono creati criteri di corrispondenza in cui è contenuta una regola. La regola avrà un prerequisito: **Supplier ID**, che indica che gli ID fornitore devono corrispondere prima di utilizzare gli altri domini nella regola. La regola utilizza altri due domini: **Supplier Name** con il valore di **somiglianza** impostato su **70%** e **Contact email** con il valore di **somiglianza** impostato su **30%**.  
  
1.  Nella pagina principale del **client DQS**fare clic sulla **freccia a destra** accanto alla Knowledge base **Suppliers** e selezionare **criteri di corrispondenza**.  
  
     ![Menu Criteri di corrispondenza nella pagina principale](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "Menu Criteri di corrispondenza nella pagina principale")  
  
2.  Nella pagina **mappa** selezionare file di **Excel** per **origine dati**.  
  
3.  Fare clic su **Sfoglia**, verificare che il filtro sia impostato su **cartella di lavoro di Excel**e selezionare il file **cleaned Supplier List. xls** che è stato esportato dopo l'esecuzione dell'attività di pulizia.  
  
    > [!NOTE]  
    >  Al termine di questa attività, non è possibile esportare i risultati poiché questa attività è mirata principalmente alla definizione di criteri di corrispondenza. Verrà creato un progetto Data Quality per l'attività di corrispondenza che verrà eseguito per rimuovere i duplicati dall'elenco di fornitori utilizzando questi criteri di corrispondenza illustrati nella lezione successiva.  
  
4.  Eseguire il mapping della colonna **SupplierID** al dominio **Supplier ID** , della colonna **Supplier Name** al dominio **Supplier Name** , della colonna **ContactEmailAddress** al dominio **Contact email** . È sufficiente eseguire il mapping delle colonne di origine ai domini che si desidera utilizzare per la definizione dei criteri di corrispondenza. In questo caso, si stanno rendendo disponibili i domini Supplier ID, Supplier Name e Contact Email per l'attività relativa ai criteri di corrispondenza.  
  
     ![Pagina Mapping del processo di definizione dei criteri di corrispondenza](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "Pagina Mapping del processo di definizione dei criteri di corrispondenza")  
  
5.  Fare clic su **Avanti** per passare alla pagina **criteri di corrispondenza** in cui verranno definiti i criteri di corrispondenza con una regola al suo interno.  
  
6.  Fare clic sul pulsante **Crea regola di corrispondenza** sulla barra degli strumenti per creare una regola nel criterio.  
  
     ![Pulsante della barra degli strumenti Crea regola di corrispondenza](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "Pulsante della barra degli strumenti Crea regola di corrispondenza")  
  
7.  Nel riquadro **Dettagli regola** a destra, immettere Rimuovi i **fornitori duplicati** per il **nome della regola**.  
  
8.  Fare clic su **Aggiungi un nuovo elemento di dominio** nella barra degli strumenti nel riquadro di destra.  
  
     ![Dettagli regola - Pulsante Aggiungi nuovo elemento di domino](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "Dettagli regola - Pulsante Aggiungi nuovo elemento di domino")  
  
9. Selezionare **Supplier ID** per il **dominio** e selezionare la casella di controllo **prerequisiti** . Si noti che la **somiglianza** è impostata automaticamente su **exact**. Impostando **Supplier ID** come **prerequisito**, si specifica che i valori per questo campo nei due record devono restituire una corrispondenza del 100%. in caso contrario, i record non vengono considerati corrispondenti e le altre clausole nella regola verranno ignorate.  
  
     ![Definizione regola Rimuovi fornitori duplicati](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "Definizione regola Rimuovi fornitori duplicati")  
  
10. Fare di nuovo clic su **Aggiungi un nuovo elemento di dominio** dalla barra degli strumenti.  
  
11. Selezionare **Supplier Name** Domain, selezionare **simile** alla **somiglianza**e digitare **70** per il **peso**.  In questo caso, si specifica che i nomi dei fornitori non devono essere identici, ma possono essere simili per i record che devono essere considerati corrispondenti. Il peso indica il contributo del punteggio del campo al Punteggio di corrispondenza complessivo.  
  
12. Ripetere i due passaggi precedenti per aggiungere il dominio di **posta elettronica di contatto** con **30** per il **peso**.  
  
13. Si noti che **Il Punteggio di corrispondenza minimo** è impostato su **80%**, ovvero sul valore visualizzato nella scheda **generale** della pagina **configurazione** di **Amministrazione DQS**. Questo punteggio può essere aumentato oltre questo valore soglia solo qui.  
  
14. Si noti che l'opzione **cluster sovrapposti** è selezionata. Con questa opzione, un record può essere visualizzato in più cluster. Se l'impostazione viene modificata su Cluster non sovrapposti, i cluster che presentano record comuni vengono combinati in uno unico.  
  
15. Il pulsante **Avvia** in questa pagina consente di testare separatamente ogni regola nel criterio, mentre il pulsante Avvia nella pagina successiva consente di testare l'intero criterio (tutte le regole nel criterio).  
  
16. Fare clic su **Avanti** per passare alla pagina **Risultati corrispondenza** .  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 2: Test e pubblicazione dei criteri di corrispondenza](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  
