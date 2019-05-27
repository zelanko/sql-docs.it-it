---
title: Spostare o eliminare un elemento (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- moving items
- items [Reporting Services], moving
ms.assetid: 980a66c7-a18b-4af7-8954-45726fa517d6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aafd2ff32e8c554186d18a6329649081e8babe6b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103729"
---
# <a name="move-or-delete-an-item-report-manager"></a>Spostare o eliminare un elemento (Gestione report)
  I report e gli altri elementi relativi ai report pubblicati in un server di report vengono archiviati in cartelle. È possibile spostare gli elementi in una cartella diversa e i riferimenti a tali elementi vengono mantenuti automaticamente dal server di report. Prima di eliminare un elemento, verificare se sono presenti altri elementi che dipendono da esso.  
  
## <a name="move-an-item"></a>Spostare un elemento  
 È possibile spostare gli elementi del server di report in percorsi di cartelle diversi nella gerarchia di cartelle del server di report. Quando si sposta un elemento, tutte le proprietà, incluse le impostazioni di sicurezza, vengono spostate con l'elemento nel nuovo percorso. Quando si sposta una cartella, vengono spostati tutti gli elementi contenuti nella cartella.  
  
 In Gestione report gli elementi che è possibile spostare vengono indicati nella gerarchia di cartelle. Nella tabella seguente sono illustrate le icone di ogni elemento che è possibile spostare.  
  
|Icona|Elemento spostabile|  
|----------|-------------------|  
|![Icona di report](../media/hlp-16doc.gif "Icona di report")|Report|  
|![Icona di report collegato](../media/hlp-16linked.gif "Icona di report collegato")|Report collegato|  
|![Icona di cartella](../media/hlp-16folder.gif "Icona di cartella")|Cartella|  
|![Icona di risorsa generica](../media/hlp-16file.gif "Icona di risorsa generica")|Risorsa generica|  
|![Icona di origine dati condivisa](../media/hlp-16datasource.png "Icona di origine dati condivisa")|Origine dati condivisa|  
||Set di dati condiviso|  
  
 Non tutti gli elementi possono essere spostati. Non è possibile spostare elementi associati a un report, ad esempio le sottoscrizioni o la cronologia del report. Tali elementi si spostano insieme ai report a essi associati. Analogamente, non è possibile spostare elementi disponibili all'esterno della gerarchia di cartelle, ad esempio le pianificazioni condivise. Non è possibile spostare gli elementi se non si dispone delle autorizzazioni appropriate. L'autorizzazione per spostare un elemento verrà comunicata quando vengono selezionate le seguenti operazioni nell'assegnazione di ruolo per l'elemento in questione: "Gestione report," "Gestisci modelli", "Gestione di cartelle" e "Gestione di origini dati".  
  
#### <a name="to-move-an-item-from-within-the-contents-page"></a>Per spostare un elemento dalla pagina Contenuto  
  
1.  Avviare [gestione Report &#40;modalità nativa SSRS&#41;]... / report-manager-ssrs-native-mode.md).  
  
2.  In Gestione report passare alla pagina **Contenuto** e individuare l'elemento da spostare.  
  
3.  Posizionare il puntatore del mouse sull'elemento, quindi fare clic sulla freccia a discesa.  
  
4.  Nel menu a discesa fare clic su **Sposta**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  In **Percorso**specificare la cartella in cui si vuole spostare l'elemento. È possibile digitare il nome completo della cartella oppure utilizzare il controllo dell'albero per passare alla cartella desiderata.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 In alternativa, è possibile passare all'oggetto da spostare, fare clic su **Proprietà**e quindi su **Sposta** nella parte superiore della pagina.  
  
## <a name="delete-an-item"></a>Eliminare un elemento  
 Prima di eliminare un elemento, determinare se è utilizzato da altri elementi. Se ad esempio si elimina un'origine dati condivisa, i report e i modelli che la utilizzano non verranno più eseguiti. Quando si elimina un report, vengono eliminate anche la cronologia del report e le sottoscrizioni associate. Per trovare elementi dipendenti per un elemento, vedere [pagina elementi dipendenti &#40;gestione Report&#41;]... / dipendenti-elementi-pagina-report-manager.md).  
  
#### <a name="to-delete-a-report-or-item"></a>Per eliminare un report o un elemento  
  
1.  Avviare [gestione Report &#40;modalità nativa SSRS&#41;]... / report-manager-ssrs-native-mode.md).  
  
2.  In Gestione report passare alla pagina **Contenuto** e quindi individuare l'elemento da eliminare.  
  
3.  Posizionare il puntatore del mouse sull'elemento, quindi fare clic sulla freccia a discesa.  
  
4.  Scegliere **Elimina**dal menu a discesa.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto della pagina &#40;gestione Report&#41;]... / contenuto-pagina-report-manager.md)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
