---
title: Creare un percorso attendibile per siti PowerPivot in Amministrazione centrale | Microsoft Docs
ms.custom: ''
ms.date: 04/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a666f365-cd93-43a3-9d3d-e429dfc19b66
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b54c06d86490c92936d147f2876d663f43d99fac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071592"
---
# <a name="create-a-trusted-location-for-powerpivot-sites-in-central-administration"></a>Creare un percorso attendibile per i siti PowerPivot in Amministrazione centrale
  Excel Services consente di specificare i percorsi che rappresentano repository validi per le cartelle di lavoro che vengono aperte in un server SharePoint. Questi percorsi vengono chiamati "percorsi attendibili" ed è possibile utilizzare impostazioni di configurazione diverse per ogni percorso attendibile creato. Per una distribuzione di PowerPivot per SharePoint, è necessario considerare la creazione di un percorso attendibile per i siti che contengono cartelle di lavoro di PowerPivot in modo che sia possibile applicare le impostazioni che funzionano meglio per l'accesso ai dati PowerPivot mantenendo le impostazioni predefinite per il resto della farm.  
  
  
  
## <a name="prerequisites"></a>Prerequisiti  
 È necessario essere un amministratore del servizio o della farm per definire un URL come percorso attendibile.  
  
 È necessario conoscere l'indirizzo URL del sito di SharePoint contenente la raccolta PowerPivot o un'altra libreria che archivia le cartelle di lavoro. Per ottenere l'indirizzo, aprire il sito che contiene la raccolta, fare doppio clic su **raccolta PowerPivot**, selezionare **proprietà**e quindi copiare la prima parte dell'indirizzo (URL) che contiene il nome del server e il sito percorso.  
  
##  <a name="overview"></a> Panoramica  
 Un'installazione iniziale di Excel Services specifica "http://" come percorso attendibile, pertanto, nel server, possono essere aperte cartelle di lavoro di qualsiasi sito della farm. Se è necessario un controllo più rigido sui percorsi considerati attendibili, è possibile creare nuovi percorsi attendibili che eseguono il mapping a siti specifici della farm, quindi variare le impostazioni e le autorizzazioni per ognuno.  
  
 La creazione di un nuovo percorso attendibile per siti che ospitano cartelle di lavoro di PowerPivot è utile soprattutto se si desidera mantenere i valori predefiniti per il resto della farm e applicare impostazioni diverse che funzionano meglio per l'accesso ai dati PowerPivot. Ad esempio, un percorso attendibile ottimizzato per le cartelle di lavoro di PowerPivot potrebbe disporre di una cartella di lavoro di dimensioni massime pari a 50 MB, mentre il resto della farm utilizza il valore predefinito di 10 MB.  
  
 La creazione di un percorso attendibile è consigliata se si utilizzano le librerie della raccolta PowerPivot per visualizzare in anteprima le cartelle di lavoro pubblicate e vengono rilevati avvisi di aggiornamento dati anziché l'immagine di anteprima prevista. La raccolta PowerPivot esegue il rendering delle immagini di anteprima dei report e delle cartelle di lavoro tramite dati e informazioni di presentazione all'interno del documento. Se l'opzione Avvisa in caso di aggiornamento è abilitata per un percorso attendibile, la raccolta PowerPivot potrebbe non disporre di autorizzazioni sufficienti per eseguire l'aggiornamento, provocando la visualizzazione di un errore al posto di un'immagine di anteprima. L'aggiunta di un sito che contiene la raccolta PowerPivot come nuovo percorso attendibile può risolvere questo problema.  
  
##  <a name="create"></a> Creare un percorso attendibile per accedere ai dati PowerPivot  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sull'applicazione di servizio Excel Services.  
  
3.  Fare clic su **Posizioni attendibili file**.  
  
4.  Fare clic su **Aggiungi posizione attendibile file**.  
  
5.  Immettere l'URL di un sito che contiene una libreria della raccolta PowerPivot.  
  
6.  In Tipo percorso selezionare **Microsoft SharePoint Foundation**.  
  
    > [!IMPORTANT]  
    >  I tipi di percorsi UNC e HTTP non sono supportati per l'accesso ai dati PowerPivot.  
  
7.  Accettare tutte le impostazioni predefinite per le proprietà in Gestione sessioni, Proprietà cartella di lavoro e Comportamento calcolo.  
  
8.  In Proprietà cartella di lavoro impostare **Dimensioni massime cartella di lavoro** su **50**. In questo modo, il limite superiore per le dimensioni del file della cartella di lavoro viene allineato al limite superiore per i caricamenti del file nell'applicazione Web padre. Se le dimensioni delle cartelle di lavoro superano i 50 megabyte, è necessario aumentare ulteriormente il limite della dimensione del file. Per altre informazioni, vedere [configurare dimensioni di caricamento File massime &#40;PowerPivot per SharePoint&#41;](configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
9. In Dati esterni verificare che l'opzione Impostazione dati esterni consentiti sia impostata su **Raccolte di connessioni dati attendibili e connessioni incorporate**. Questa impostazione è necessaria per l'accesso ai dati PowerPivot in una cartella di lavoro.  
  
10. Anche in Dati esterni, per Avviso in caso di aggiornamento, deselezionare la casella di controllo **Attiva avviso di aggiornamento**. Se si deseleziona la casella di controllo, la raccolta PowerPivot può ignorare i messaggi di avviso della routine e vengono invece visualizzate le immagini di anteprima di una cartella di lavoro.  
  
11. Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta PowerPivot](../../2014-toc/books-online-for-sql-server-2014.md)   
 [Creare e personalizzare la raccolta PowerPivot](create-and-customize-power-pivot-gallery.md)   
 [Usare la raccolta PowerPivot](use-power-pivot-gallery.md)  
  
  
