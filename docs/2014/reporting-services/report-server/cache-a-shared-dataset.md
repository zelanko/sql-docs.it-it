---
title: Memorizzare nella cache un set di dati condiviso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c2d8c81a-da1e-4a8a-9845-fff9a0903d24
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9c4b124ca7d8595962535cded369670430a4adff
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026462"
---
# <a name="cache-a-shared-dataset"></a>Memorizzare nella cache un set di dati condiviso
  Per ottimizzare le prestazioni, è possibile configurare le proprietà relative alla memorizzazione nella cache per un set di dati condiviso. Quando un set di dati condiviso viene memorizzato nella cache, una copia dei risultati di query viene salvata per un determinato periodo di tempo. Il primo utente che richiede un report che utilizza il set di dati condiviso deve attendere il completamento dei risultati di query e di tutte le elaborazioni prima di visualizzare il report. Gli utenti successivi che richiedono il report all'interno del periodo di memorizzazione nella cache otterranno prestazioni migliori perché la query e l'elaborazione sono già state eseguite. È inoltre possibile specificare un piano di aggiornamento della cache per eseguire la query e memorizzare nella cache i risultati fino alla scadenza della cache specificata.  
  
 Gli utenti che eseguono report in base a un set di dati condiviso o a piani di aggiornamento della cache creano la cache delle query e in entrambi i casi, la disponibilità della cache dipende dalle opzioni di scadenza della stessa.  
  
 Sono presenti restrizioni sui tipi di set di dati condivisi che è possibile memorizzare nella cache. I risultati di query, ad esempio, non possono essere memorizzati nella cache quando i dati variano in base all'identità utente o vengono recuperati utilizzando il token di sicurezza dell'utente che richiede il report. Per altre informazioni, vedere [Memorizzare nella cache set di dati condivisi &#40;SSRS&#41;](cache-shared-datasets-ssrs.md) e [Memorizzazione dei report nella cache &#40;SSRS&#41;](caching-reports-ssrs.md).  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>Per pianificare la scadenza di un report memorizzato nella cache  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  In Gestione report passare al set di dati condiviso per cui si desidera impostare le proprietà relative alla memorizzazione nella cache, posizionare il puntatore del mouse sull'elemento, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa.  
  
4.  Nel riquadro a sinistra, fare clic su **Memorizzazione nella cache**.  
  
    > [!NOTE]  
    >  Se viene visualizzato l'errore **Le credenziali utilizzate per eseguire il set di dati condiviso non sono associate**, l'opzione relativa alla memorizzazione nella cache del set di dati condiviso verrà disabilitata. È necessario modificare l'origine dati per archiviare le credenziali o modificare il set di dati condiviso per utilizzare un'origine dati diversa che consenta di archiviare le credenziali.  
  
5.  Selezionare **Memorizza nella cache set di dati condiviso**.  
  
6.  Selezionare l'opzione che determina la scadenza della cache dopo 30 minuti. È inoltre possibile scegliere che la cache scada in base a una determinata pianificazione.  
  
7.  Fare clic su **Applica**.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire set di dati condivisi](../report-data/manage-shared-datasets.md)  
  
  
