---
title: Compilare una query in Progettazione query relazionale (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 28b25861-f3b4-4c3e-a9b0-03d6e4cfea26
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 901abf5be70f0b3c70b89b0415c59f19a9327b29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107441"
---
# <a name="build-a-query-in-the-relational-query-designer-report-builder-and-ssrs"></a>Compilare una query in Progettazione query relazionale (Generatore report e SSRS)
  Una finestra Progettazione query consente di specificare i dati da recuperare da un'origine dati esterna per un set di dati del report. Si utilizza la finestra Progettazione query quando si compila una query in una procedura guidata o si crea una query del set di dati.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Un set di dati è basato su un'origine dati. Il tipo di origine dati e l'ambiente di creazione determinano la finestra Progettazione query da visualizzare quando si definisce la query del set di dati. Le funzionalità di Progettazione query variano in base all'origine dati sottostante. Per ulteriori informazioni sui livelli di dati, vedere [connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md) o [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 È possibile utilizzare una finestra Progettazione query per le attività seguenti:  
  
-   Esplorare i metadati per più schemi nell'origine dati esterna  
  
-   Specificare i campi da recuperare per il set di dati  
  
-   Specificare le relazioni tra due oggetti quali tabelle  
  
-   Specificare i filtri per limitare i dati prima che vengono recuperati come dati del report  
  
-   Indicare se creare parametri  
  
-   Specificare le aggregazioni per eseguire i calcoli nell'origine dati esterna  
  
 Dopo avere visualizzato una finestra Progettazione query, è possibile compilare una query nello stesso modo per un set di dati incorporato o un set di dati condiviso. Nelle procedure riportate di seguito viene utilizzata una query del set di dati incorporato.  
  
 Per altre informazioni, vedere [Interfaccia utente di Progettazione query relazionale &#40;Generatore report&#41;](relational-query-designer-user-interface-report-builder.md).  
  
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
  
1.  Sulla barra degli strumenti di Progettazione query fare clic su **Esegui query (!)**.  
  
    > [!NOTE]  
    >  Nella finestra Progettazione query vengono utilizzate le credenziali della fase di progettazione per eseguire la query e recuperare il set di risultati. Per altre informazioni, vedere [Specifica di credenziali in Generatore report](../specify-credentials-in-report-builder.md).  
  
 La query viene eseguita sull'origine dati e i dati di esempio vengono restituiti nel riquadro Risultati query.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere dati a un report &#40;Generatore report e SSRS&#41;](report-datasets-ssrs.md)   
 [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md)   
 [Progettazione query &#40;Generatore report&#41;](../query-designers-report-builder.md)   
 [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Visualizzazione di progettazione report &#40;Generatore report&#41;](../report-builder/report-design-view-report-builder.md)   
 [Visualizzazione di progettazione del set di dati condiviso &#40;Generatore report&#41;](../report-builder/shared-dataset-design-view-report-builder.md)   
 [Strumenti di progettazione query in Reporting Services](../reporting-services-query-designers.md)  
  
  
