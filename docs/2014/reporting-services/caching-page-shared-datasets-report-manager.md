---
title: Pagina memorizzazione nella cache, set di impostazioni condivisi (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eac372e9-d2a1-48a8-bbe5-09d101df16ea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ae18d021465a7d14ea22b56534ea48ac316154c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109904"
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
 **Memorizza nella cache set di dati condiviso**  
 Consente di posizionare nella cache una copia temporanea dei dati alla prima apertura da parte di un utente di un report che utilizza questo set di dati. Gli utenti che eseguono successivamente il report durante il periodo di memorizzazione nella cache riceveranno la copia dei dati memorizzata nella cache. La memorizzazione nella cache consente in genere di migliorare le prestazioni in quanto i dati vengono restituiti dalla cache anziché tramite una nuova query del set di dati.  
  
 **Memorizza nella cache una copia temporanea del report. La copia del report scadrà dopo il numero di minuti seguente**  
 Specificare il numero di minuti per il salvataggio della copia memorizzata nella cache dei dati. Dopo la scadenza della copia temporanea i dati non vengono più restituiti dalla cache. Alla successiva apertura di un report che utilizza questo set di dati condiviso da parte di un utente, viene eseguita la query del set di dati e il server di report memorizza nella cache una copia dei dati aggiornati.  
  
 **Scadenza cache basata sulla pianificazione seguente**  
 Consente di pianificare l'ora in cui i dati memorizzati nella cache non sono più validi e vengono rimossi dalla stessa. La pianificazione può essere una pianificazione condivisa o specifica del set di dati condiviso corrente.  
  
 **Pianificazione specifica del set di dati**  
 Consente di specificare una pianificazione utilizzata solo per questo set di dati.  
  
 **Pianificazione condivisa**  
 Consente di specificare una pianificazione condivisa fra report, sottoscrizioni e altri set di dati condivisi.  
  
 **Applica**  
 Salvare le modifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Guida sensibile al contesto Gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Memorizzare nella cache i set di impostazioni &#40;SSRS&#41;](report-server/cache-shared-datasets-ssrs.md)   
 [Pianificazioni](subscriptions/schedules.md)  
  
  
