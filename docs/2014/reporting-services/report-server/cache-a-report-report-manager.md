---
title: Memorizzare un report nella cache (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- cached reports [Reporting Services]
- schedules [Reporting Services], report expiration
- expiration [Reporting Services]
ms.assetid: 723d1cb0-c2e7-4763-8690-a6a7a8bbbb90
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 4269c5219dc52df82f46f1d495d895321fc6f276
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023592"
---
# <a name="cache-a-report-report-manager"></a>Memorizzare un report nella cache (Gestione report)
  Per ottimizzare le prestazioni, è possibile configurare le proprietà relative alla memorizzazione nella cache per un report. Quando un report viene memorizzato nella cache, una copia del report visualizzabile viene salvata per un breve periodo di tempo. Il primo utente che richiede il report deve attendere il completamento di tutte le elaborazioni prima di visualizzare il report. Gli utenti successivi che richiedono il report all'interno del periodo di memorizzazione nella cache possono visualizzarlo immediatamente perché l'elaborazione è già stata eseguita.  
  
 Sono presenti restrizioni sui tipi di report che è possibile memorizzare nella cache. Ad esempio, un report non può essere memorizzato nella cache se l'output del report varia in base all'identità utente o se i dati vengono recuperati utilizzando il token di sicurezza dell'utente che richiede il report. Per altre informazioni, vedere [Memorizzazione dei report nella cache &#40;SSRS&#41;](caching-reports-ssrs.md).  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>Per pianificare la scadenza di un report memorizzato nella cache  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  In Gestione report passare alla pagina **Contenuto** . quindi passare al report per il quale si desidera impostare le proprietà relative alla memorizzazione nella cache, posizionare il puntatore del mouse sull'elemento e fare clic sulla freccia a discesa.  
  
3.  Nel menu a discesa fare clic su **Gestisci**.  
  
4.  Nel riquadro di sinistra fare clic sulla scheda **Opzioni di elaborazione**.  
  
5.  Nella pagina scegliere **Eseguire sempre questo report con i dati più recenti**.  
  
6.  Selezionare una delle due opzioni cache seguenti e configurare la scadenza come segue:  
  
    -   Per configurare una copia memorizzata nella cache in modo che scada dopo un periodo di tempo specifico, fare clic su **Memorizza nella cache una copia temporanea del report. La copia del report scadrà dopo il numero di minuti seguente**. Digitare il numero di minuti alla scadenza del report.  
  
    -   Per configurare una copia memorizzata nella cache affinché scada in base a una pianificazione, fare clic su **Memorizza nella cache una copia temporanea del report. La scadenza della copia è determinata dalla pianificazione seguente.** Fare clic su **Configura**oppure selezionare una pianificazione condivisa per controllare la scadenza del report.  
  
7.  Fare clic su **Applica**.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare proprietà di elaborazione dei report](set-report-processing-properties.md)   
 [Memorizzazione dei report nella cache &#40;SSRS&#41;](caching-reports-ssrs.md)  
  
  
