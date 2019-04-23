---
title: Pagina memorizzazione nella cache, condivisi (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: eac372e9-d2a1-48a8-bbe5-09d101df16ea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6b816af806e419cab0f6eb0997c6ec7f08bc7b93
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59968747"
---
# <a name="caching-page-shared-datasets-report-manager"></a>Pagina Memorizzazione nella cache, set di dati condivisi (Gestione report)
  La pagina delle proprietà di memorizzazione nella cache consente di impostare le opzioni di cache per un set di dati condiviso.  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per spostarsi in questo percorso nell'interfaccia utente.  
  
### <a name="to-open-the-caching-properties-page-for-a-shared-dataset"></a>Per aprire la pagina delle proprietà per la memorizzazione nella cache per un set di dati condiviso  
  
1.  Aprire Gestione report, quindi individuare il report per il quale si desidera configurare le proprietà del set di dati condiviso.  
  
2.  Posizionare il puntatore del mouse sul set di dati condiviso, quindi fare clic sulla freccia a discesa.  
  
3.  Nell'elenco a discesa fare clic su **Gestisci**. Viene visualizzata la pagina delle proprietà Generale per il report.  
  
4.  Fare clic sulla scheda **Memorizzazione nella cache** .  
  
## <a name="options"></a>Opzioni  
 **Memorizzare nella cache set di dati condiviso**  
 Consente di posizionare nella cache una copia temporanea dei dati alla prima apertura da parte di un utente di un report che utilizza questo set di dati. Gli utenti che eseguono successivamente il report durante il periodo di memorizzazione nella cache riceveranno la copia dei dati memorizzata nella cache. La memorizzazione nella cache consente in genere di migliorare le prestazioni in quanto i dati vengono restituiti dalla cache anziché tramite una nuova query del set di dati.  
  
 **Scadenza cache dopo un numero di minuti**  
 Specificare il numero di minuti per il salvataggio della copia memorizzata nella cache dei dati. Dopo la scadenza della copia temporanea i dati non vengono più restituiti dalla cache. Alla successiva apertura di un report che utilizza questo set di dati condiviso da parte di un utente, viene eseguita la query del set di dati e il server di report memorizza nella cache una copia dei dati aggiornati.  
  
 **Scadenza cache basata sulla pianificazione seguente**  
 Consente di pianificare l'ora in cui i dati memorizzati nella cache non sono più validi e vengono rimossi dalla stessa. La pianificazione può essere una pianificazione condivisa o specifica del set di dati condiviso corrente.  
  
 **Pianificazione in base al set di dati**  
 Consente di specificare una pianificazione utilizzata solo per questo set di dati.  
  
 **pianificazione condivisa**  
 Consente di specificare una pianificazione condivisa fra report, sottoscrizioni e altri set di dati condivisi.  
  
 **Applica**  
 Salvare le modifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Guida F1 di gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Memorizzare nella cache set di dati condivisi &#40;SSRS&#41;](report-server/cache-shared-datasets-ssrs.md)   
 [Pianificazioni](subscriptions/schedules.md)  
  
  
