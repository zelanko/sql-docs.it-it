---
title: Aggiungere un parametro multivalore a un report | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 12ad0e77-4c28-4bbb-ab11-473ae89ec9f1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 72a827e8f15627e986008e57ecb9a180b715a8a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106808"
---
# <a name="add-a-multi-value-parameter-to-a-report"></a>Aggiunta di un parametro multivalore a un report
  È possibile aggiungere un parametro a un report che consente all'utente di selezionare più valori per il parametro.  
  
 È possibile passare più valori di parametro al report nell'URL del report. Per un esempio di URL in cui è incluso un parametro multivalore, vedere [Passare un parametro del report in un URL](../pass-a-report-parameter-within-a-url.md).  
  
 Per informazioni su come passare più valori di parametro a una stored procedure, vedere [Working With Multi-Select Parameters for SSRS Reports](https://go.microsoft.com/fwlink/?LinkId=321529) (Utilizzo di parametri a selezione multipla per report SSRS) nel sito Web mssqltips.com.  
  
### <a name="to-add-a-multi-value-parameter"></a>Per aggiungere un parametro multivalore  
  
1.  In Generatore report aprire il report a cui si desidera aggiungere il parametro multivalore.  
  
2.  Fare clic con il pulsante destro del mouse sul set di dati del report e quindi scegliere **Proprietà set di dati**.  
  
3.  Aggiungere una variabile alla query del set di dati modificando il testo della query nella casella **Query** o aggiungendo un filtro mediante la finestra Progettazione query. Per altre informazioni, vedere [Compilare una query in Progettazione query relazionale &#40;Generatore report e SSRS&#41;](../report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md).  
  
    > [!IMPORTANT]  
    >  Il testo della query non deve includere l'istruzione DECLARE per la variabile di query.  
  
    > [!IMPORTANT]  
    >  Il testo per la variabile di query deve includere l'operatore `IN`, come mostrato nell'esempio seguente.  
  
    ```  
    WHERE  
      Production.ProductInventory.ProductID IN (@ProductID)  
    ```  
  
    > [!IMPORTANT]  
    >  Se non si includono le parentesi attorno alla variabile come illustrato in precedenza, il rendering del report non viene eseguito e viene visualizzato l'errore "dichiarare la variabile scalare".  
  
     Un parametro del set di dati per un set di dati incorporato o un set di dati condiviso viene creato automaticamente per la variabile di query. Un parametro del report viene creato automaticamente per il parametro del set di dati.  
  
4.  Nel riquadro **Dati report** espandere il nodo **Parametri** , fare clic con il pulsante destro del mouse sul parametro del report che è stato creato automaticamente per il parametro del set di dati e quindi scegliere **Proprietà parametri**.  
  
5.  Nella scheda **Generale** selezionare **Consenti più valori** per consentire a un utente di selezionare più valori per il parametro.  
  
6.  Facoltativamente, nella scheda dei valori **Disponibile** specificare un elenco di valori disponibili da visualizzare all'utente.  
  
     Tale elenco limita le scelte dell'utente ai soli valori validi per il parametro. Per più valori, la funzionalità **Seleziona tutto** è disponibile all'inizio dell'elenco, in modo che l'utente possa selezionare o deselezionare tutti i valori con un solo clic. Se si sceglie di ottenere i valori disponibili per il parametro del report da una query del set di dati, assicurarsi di selezionare un set di dati che non contenga la variabile di query associata allo stesso parametro del report.  
  
     Per altre informazioni, vedere [Aggiungere, modificare o eliminare valori disponibili per un parametro di report &#40;Generatore report e SSRS&#41;](add-change-or-delete-available-values-for-a-report-parameter.md).  
  
### <a name="to-add-a-multi-value-parameter"></a>Per aggiungere un parametro multivalore  
  
1.  In Generatore report aprire il report a cui si desidera aggiungere il parametro multivalore.  
  
2.  Fare clic con il pulsante destro del mouse sul set di dati del report e quindi scegliere **Proprietà set di dati**.  
  
3.  Aggiungere una variabile alla query del set di dati modificando il testo della query nella casella **Query** o aggiungendo un filtro mediante la finestra Progettazione query. Per altre informazioni, vedere [Compilare una query in Progettazione query relazionale &#40;Generatore report e SSRS&#41;](../report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md).  
  
    > [!IMPORTANT]  
    >  Il testo della query non deve includere l'istruzione DECLARE per la variabile di query.  
  
    > [!IMPORTANT]  
    >  Il testo per la variabile di query deve includere l'operatore `IN`, come mostrato nell'esempio seguente.  
  
    ```  
    WHERE  
      Production.ProductInventory.ProductID IN (@ProductID)  
    ```  
  
    > [!IMPORTANT]  
    >  Se non si includono le parentesi attorno alla variabile come illustrato in precedenza, il rendering del report non viene eseguito e viene visualizzato l'errore "dichiarare la variabile scalare".  
  
     Un parametro del set di dati per un set di dati incorporato o un set di dati condiviso viene creato automaticamente per la variabile di query. Un parametro del report viene creato automaticamente per il parametro del set di dati.  
  
4.  Nel riquadro **Dati report** espandere il nodo **Parametri** , fare clic con il pulsante destro del mouse sul parametro del report che è stato creato automaticamente per il parametro del set di dati e quindi scegliere **Proprietà parametri**.  
  
5.  Nella scheda **Generale** selezionare **Consenti più valori** per consentire a un utente di selezionare più valori per il parametro.  
  
6.  Facoltativamente, nella scheda dei valori **Disponibile** specificare un elenco di valori disponibili da visualizzare all'utente.  
  
     Tale elenco limita le scelte dell'utente ai soli valori validi per il parametro. Per più valori, la funzionalità **Seleziona tutto** è disponibile all'inizio dell'elenco, in modo che l'utente possa selezionare o deselezionare tutti i valori con un solo clic. Se si sceglie di ottenere i valori disponibili per il parametro del report da una query del set di dati, assicurarsi di selezionare un set di dati che non contenga la variabile di query associata allo stesso parametro del report.  
  
     Per altre informazioni, vedere [Aggiungere, modificare o eliminare valori disponibili per un parametro di report &#40;Generatore report e SSRS&#41;](add-change-or-delete-available-values-for-a-report-parameter.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiunta di parametri di propagazione a un report &#40;Generatore report e SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Aggiungere, modificare o eliminare un parametro di report &#40;Generatore report e SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)  
  
  
