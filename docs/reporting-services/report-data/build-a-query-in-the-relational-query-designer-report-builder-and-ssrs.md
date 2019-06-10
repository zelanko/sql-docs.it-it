---
title: Compilare una query in Progettazione query relazionale (Generatore report e SSRS)
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/25/2019
ms.openlocfilehash: 400e96771d54e090e9e3b2bc03967d26b50a6590
ms.sourcegitcommit: 1800fc15075bb17b50d0c18b089d8a64d87ae726
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2019
ms.locfileid: "66500491"
---
# <a name="build-a-query-in-the-relational-query-designer-report-builder-and-ssrs"></a>Compilare una query in Progettazione query relazionale (Generatore report e SSRS)

Una finestra Progettazione query consente di specificare i dati da recuperare da un'origine dati esterna per un set di dati del report. Si utilizza la finestra Progettazione query quando si compila una query in una procedura guidata o si crea una query del set di dati.  
  
> [!NOTE]  
> [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Un set di dati è basato su un'origine dati. Il tipo di origine dati e l'ambiente di creazione determinano la finestra Progettazione query da visualizzare quando si definisce la query del set di dati. Le funzionalità di Progettazione query variano in base all'origine dati sottostante. Per altre informazioni sui livelli di dati, vedere [Connessioni dati, origini dati e stringhe di connessione in Generatore report](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).

 È possibile utilizzare una finestra Progettazione query per le attività seguenti:  
  
-   Esplorare i metadati per più schemi nell'origine dati esterna  
  
-   Specificare i campi da recuperare per il set di dati  
  
-   Specificare le relazioni tra due oggetti quali tabelle  
  
-   Specificare i filtri per limitare i dati prima che vengono recuperati come dati del report  
  
-   Indicare se creare parametri  
  
-   Specificare le aggregazioni per eseguire i calcoli nell'origine dati esterna  
  
 Dopo avere visualizzato una finestra Progettazione query, è possibile compilare una query nello stesso modo per un set di dati incorporato o un set di dati condiviso. Nelle procedure riportate di seguito viene utilizzata una query del set di dati incorporato.  
  
 Per altre informazioni, vedere [Interfaccia utente di Progettazione query relazionale &#40;Generatore report&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md).  
  
### <a name="to-build-a-query-for-an-embedded-dataset-in-report-design-view"></a>Per compilare una query per un set di dati incorporato nella visualizzazione Struttura report  
  
1.  Aprire la finestra Progettazione query. Nel riquadro dei dati del report fare clic con il pulsante destro del mouse sul set di dati e quindi scegliere **Query**.  
  
     Verrà visualizzata la finestra Progettazione query associata all'origine dati.  
  
2.  Nel riquadro Vista di database espandere le cartelle in cui viene visualizzata una vista gerarchica di oggetti dello schema di database quali tabelle, viste e stored procedure. Fare clic sulla casella scelta per selezionare tutti i campi per un oggetto o espandere il nodo per selezionare i singoli campi.  
  
     Quando si selezionano i campi dal riquadro Vista di database, le scelte vengono visualizzate nel riquadro **Seleziona campi** .  
  
     Se si selezionano campi da più tabelle di database correlate, utilizzare il riquadro Relazioni per visualizzare le relazioni tra tabelle rilevate dallo schema del database.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     L'elenco di campi del set di dati viene visualizzato nel riquadro dei dati del report.  
  
### <a name="to-specify-limits-for-a-query"></a>Per specificare i limiti per una query  
  
1.  In Progettazione query relazionale verificare di aver selezionato i campi e che questi vengano visualizzati nel riquadro **Campi selezionati** .  
  
2.  Nella barra degli strumenti del riquadro Filtri applicati fare clic su **Aggiungi filtro**. Verrà visualizzata una nuova riga del filtro.  
  
3.  In **Nome campo**fare clic per visualizzare l'elenco a discesa dei campi e quindi fare clic sul nome del campo in base al quale si vuole filtrare. Per filtrare ad esempio in base alla quantità, fare clic sul campo che contiene il numero di elementi.  
  
4.  In **Operatore**fare clic per visualizzare l'elenco a discesa degli operatori e quindi selezionare l'operatore di confronto da usare nel filtro.  
  
5.  In **Valore**digitare il valore in base al quale si vuole filtrare. Per filtrare ad esempio in base a una quantità maggiore di 100, digitare 100.  
  
6.  Selezionare l'opzione di parametro in questa riga per creare un parametro del set di dati per consentire a un utente di specificare un valore di filtro. Un parametro del report che corrisponde al parametro del set di dati viene creato automaticamente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 L'elenco di campi del set di dati viene visualizzato nel riquadro dei dati del report.  
  
### <a name="to-view-a-query-result-set"></a>Per visualizzare un set di risultati della query  
  
1.  Sulla barra degli strumenti di Progettazione query fare clic su **Esegui query (!)** .  
  
    > [!NOTE]  
    >  Nella finestra Progettazione query vengono utilizzate le credenziali della fase di progettazione per eseguire la query e recuperare il set di risultati. Per altre informazioni, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](specify-credential-and-connection-information-for-report-data-sources.md).  
  
 La query viene eseguita sull'origine dati e i dati di esempio vengono restituiti nel riquadro Risultati query.  
  
## <a name="see-also"></a>Vedere anche  
 [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)   
 [Strumenti di progettazione query &#40;SSRS&#41;](query-design-tools-ssrs.md)   
 [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Visualizzazione di progettazione report &#40;Generatore report&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [Visualizzazione di progettazione set di dati condivisi &#40;Generatore report&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
 [Strumenti di progettazione query in Reporting Services](https://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)  
  
  
