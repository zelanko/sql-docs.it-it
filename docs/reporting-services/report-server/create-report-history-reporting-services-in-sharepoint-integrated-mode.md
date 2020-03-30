---
title: Creare la cronologia dei report (Reporting Services in modalità integrata SharePoint) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report history [Reporting Services], SharePoint
ms.assetid: e57ec746-05ae-4ff6-8e39-6cde87310daa
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4034d7a2892ede43f364d0ebdd105314b6107ff2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "65580361"
---
# <a name="create-report-history-reporting-services-in-sharepoint-integrated-mode"></a>Creare la cronologia dei report (Reporting Services in modalità integrata SharePoint)
  La cronologia di un report è una raccolta di snapshot del report creati nel tempo. Ogni snapshot è una copia del report nello stato in cui si trovava al momento della creazione. e include il layout e i dati del report aggiornati al momento della creazione dello snapshot. Le informazioni sul rendering non vengono archiviate con lo snapshot. Gli snapshot della cronologia del report vengono aperti in una pagina HTML nella web part Visualizzatore report. Dopo il rendering, lo snapshot può essere esportato in altri formati di applicazione.  
  
 Per creare la cronologia del report, è necessario che il report possa essere eseguito automaticamente, ovvero che il server di report sia in grado di eseguire il report senza l'interazione dell'utente. È necessario disporre dell'autorizzazione Modifica elementi sulla raccolta che contiene il report. Per visualizzare o eliminare la cronologia del report, è necessario disporre dell'autorizzazione Visualizzazione versioni o Eliminazione versioni.  
  
### <a name="to-create-a-snapshot-or-report-history-on-demand"></a>Per creare uno snapshot o una cronologia del report su richiesta  
  
1.  Selezionare il report.  
  
2.  Fare clic per visualizzare la freccia in giù e quindi selezionare **Visualizza cronologia report**.  
  
3.  Fare clic su **Nuovo snapshot**. Se tale pulsante non è visualizzato, significa che non si dispone delle autorizzazioni necessarie per la creazione di snapshot nella cronologia del report.  
  
4.  Per visualizzare lo snapshot appena creato, selezionarlo dall'elenco. Ogni snapshot è identificato da un timestamp che ne indica la data e l'ora di creazione. Non è possibile rinominare lo snapshot, spostarlo in un altro percorso o modificarlo.  
  
### <a name="to-schedule-report-history"></a>Per pianificare la cronologia di un report  
  
1.  Selezionare il report.  
  
2.  Fare clic per visualizzare la freccia in giù e quindi selezionare **Gestisci opzioni di elaborazione**.  
  
3.  In **Opzioni snapshot cronologia**fare clic su **Crea snapshot della cronologia del report in base a una pianificazione**.  
  
4.  Se si dispone di una pianificazione condivisa che contiene le informazioni di pianificazione che si desidera usare, fare clic su **In base a una pianificazione condivisa** e selezionare la pianificazione da usare. In caso contrario fare clic su **In base a una pianificazione personalizzata**, quindi su **Configura** per specificare le opzioni relative alla creazione della cronologia del report in base a una pianificazione ricorrente.  
  
### <a name="to-create-report-history-when-data-is-refreshed-in-a-report"></a>Per creare la cronologia del report quando i dati del report vengono aggiornati  
  
1.  Selezionare il report.  
  
2.  Fare clic per visualizzare la freccia in giù e quindi selezionare **Gestisci opzioni di elaborazione**.  
  
3.  In **Opzioni snapshot cronologia**fare clic su **Archivia tutti gli snapshot di dati del report nella cronologia del report**.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare le opzioni di elaborazione &#40;Reporting Services in modalità integrata SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
  
