---
title: Spostare o eliminare un elemento (Gestione report) | Microsoft Docs
description: Un server di report in Gestione report archivia i report e gli elementi correlati in cartelle. È possibile spostare o eliminare elementi. Il server di report gestisce i riferimenti agli elementi spostati.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- moving items
- items [Reporting Services], moving
ms.assetid: 980a66c7-a18b-4af7-8954-45726fa517d6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c02d85c3230502f3360039b132e8328e40d06d28
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987157"
---
# <a name="move-or-delete-an-item-report-manager"></a>Spostare o eliminare un elemento (Gestione report)
  I report e gli altri elementi relativi ai report pubblicati in un server di report vengono archiviati in cartelle. È possibile spostare gli elementi in una cartella diversa e i riferimenti a tali elementi vengono mantenuti automaticamente dal server di report. Prima di eliminare un elemento, verificare se sono presenti altri elementi che dipendono da esso.  
  
## <a name="move-an-item"></a>Spostare un elemento  
 È possibile spostare gli elementi del server di report in percorsi di cartelle diversi nella gerarchia di cartelle del server di report. Quando si sposta un elemento, tutte le proprietà, incluse le impostazioni di sicurezza, vengono spostate con l'elemento nel nuovo percorso. Quando si sposta una cartella, vengono spostati tutti gli elementi contenuti nella cartella.  
  
 In Gestione report gli elementi che è possibile spostare vengono indicati nella gerarchia di cartelle. Nella tabella seguente sono illustrate le icone di ogni elemento che è possibile spostare.  
  
|Icona|Elemento spostabile|  
|----------|-------------------|  
|![Report icon](../../reporting-services/report-server/media/hlp-16doc.gif "Icona di report")|Report|  
|![Icona di report collegato](../../reporting-services/report-server/media/hlp-16linked.gif "Icona di report collegato")|Report collegato|  
|![Icona Cartella](../../reporting-services/report-server/media/hlp-16folder.gif "Icona Cartella")|Cartella|  
|![Icona di risorsa generica](../../reporting-services/report-server/media/hlp-16file.gif "Icona di risorsa generica")|Risorsa generica|  
|![Shared data source icon](../../reporting-services/report-data/media/hlp-16datasource.png "Icona Origine dati condivisa")|Origine dati condivisa|  
||Set di dati condiviso|  
  
 Non tutti gli elementi possono essere spostati. Non è possibile spostare elementi associati a un report, ad esempio le sottoscrizioni o la cronologia del report. Tali elementi si spostano insieme ai report a essi associati. Analogamente, non è possibile spostare elementi disponibili all'esterno della gerarchia di cartelle, ad esempio le pianificazioni condivise. Non è possibile spostare gli elementi se non si dispone delle autorizzazioni appropriate. L'autorizzazione per lo spostamento di un elemento viene concessa a un utente selezionando le attività seguenti nell'assegnazione di ruolo dell'utente per l'elemento specifico: "Gestione di report", "Gestione modelli", "Gestione di cartelle" e "Gestione di origini dei dati".  
  
#### <a name="to-move-an-item-from-within-the-contents-page"></a>Per spostare un elemento dalla pagina Contenuto  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../web-portal-ssrs-native-mode.md).  
  
2.  In Gestione report passare alla pagina **Contenuto** e individuare l'elemento da spostare.  
  
3.  Posizionare il puntatore del mouse sull'elemento, quindi fare clic sulla freccia a discesa.  
  
4.  Nel menu a discesa fare clic su **Sposta**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  In **Percorso**specificare la cartella in cui si vuole spostare l'elemento. È possibile digitare il nome completo della cartella oppure utilizzare il controllo dell'albero per passare alla cartella desiderata.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 In alternativa, è possibile passare all'oggetto da spostare, fare clic su **Proprietà**e quindi su **Sposta** nella parte superiore della pagina.  
  
## <a name="delete-an-item"></a>Eliminare un elemento  
 Prima di eliminare un elemento, determinare se è utilizzato da altri elementi. Se ad esempio si elimina un'origine dati condivisa, i report e i modelli che la utilizzano non verranno più eseguiti. Quando si elimina un report, vengono eliminate anche la cronologia del report e le sottoscrizioni associate. Per trovare elementi dipendenti per un elemento specifico, vedere [Pagina Elementi dipendenti&#40;Gestione report&#41;](../web-portal-ssrs-native-mode.md).  
  
#### <a name="to-delete-a-report-or-item"></a>Per eliminare un report o un elemento  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../web-portal-ssrs-native-mode.md).  
  
2.  In Gestione report passare alla pagina **Contenuto** e quindi individuare l'elemento da eliminare.  
  
3.  Posizionare il puntatore del mouse sull'elemento, quindi fare clic sulla freccia a discesa.  
  
4.  Scegliere **Elimina**dal menu a discesa.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Pagina Contenuto &#40;Gestione report&#41;](/previous-versions/sql/sql-server-2016/ms186470(v=sql.130))   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
