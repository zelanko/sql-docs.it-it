---
title: Proprietà pianificazione (pagina Generale) | Microsoft Docs
description: Informazioni sulle opzioni per la visualizzazione o la modifica di una pianificazione condivisa nella pagina Reporting Services di SQL Server Management Studio.
ms.date: 06/11/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.scheduleproperties.general.f1
ms.assetid: 20e43966-6caf-4972-a2e2-0d9131ac8f51
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dd34cc584049eb363f6119e1131eaaaa853b3ce4
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920937"
---
# <a name="schedule-properties-general-page"></a>Proprietà pianificazione (pagina Generale)
  Usare la pagina [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] per visualizzare o modificare una pianificazione condivisa. È possibile utilizzare le pianificazioni condivise al posto di di pianificazioni specifiche di report o sottoscrizioni. Le modifiche alla pianificazione vengono applicate dopo aver salvato la pianificazione stessa. La modifica di una pianificazione non ha effetto sui processi attualmente in corso. Se si modifica una pianificazione mentre è in uso, tutte le sottoscrizioni e i report in esecuzione attivati da tale pianificazione verranno portati a termine.  
  
 Non è possibile supportare tutte le combinazioni di frequenze in una singola pianificazione. Ad esempio, se si desidera eseguire un report alle 12.00 e alle 16.00 ogni venerdì è necessario creare due pianificazioni giornaliere, una con giorno di esecuzione venerdì e inizio alle ore 12.00 e l'altra con inizio alle ore 16.00  
  
 L'elaborazione delle pianificazioni si basa sull'orario locale del server di report che ospita ed elabora la pianificazione.  
  
 Per aprire la pagina:
 1) Avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Connettersi a un'istanza di un server di report.
 3) Espandere la cartella **Pianificazioni condivise** .
 4) Fare clic con il pulsante destro del mouse su una pianificazione condivisa e selezionare **Proprietà**.  
  
> [!NOTE]  
>Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e questa pagina non è visualizzata quando si esegue un'edizione che non dispone di questa funzionalità. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Edizioni e funzionalità supportate di SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Consente di specificare il nome della pianificazione condivisa.  
  
 **Inizia l'esecuzione della pianificazione il**  
 Consente di specificare la data di inizio della pianificazione.  
  
 **Arresta l'esecuzione della pianificazione il**  
 Consente di impostare la data di scadenza della pianificazione.  
  
 **Tipo**  
 Specifica se il criterio di occorrenza è basato principalmente su ore, giorni, settimane o mesi oppure se l'esecuzione è prevista una sola volta.  
  
 **Ora (criterio di occorrenza)**  
 Consente di specificare le opzioni per l'esecuzione di un'operazione pianificata a intervalli di un'ora, ad esempio per eseguire un report ogni 6 ore. È possibile specificare l'intervallo in ore e minuti.  
  
 **Giorno (criterio di occorrenza)**  
 Consente di specificare le opzioni per l'esecuzione di un'operazione pianificata a intervalli di giorni, ad esempio per eseguire un report ogni 2 giorni. È possibile specificare l'intervallo in giorni e impostare l'ora e i minuti in cui si desidera eseguire la pianificazione.  
  
 **Settimana (criterio di occorrenza)**  
 Consente di specificare le opzioni per l'esecuzione di un'operazione pianificata a intervalli di una settimana oppure quando lo schema che si desidera ripetere si basa su settimane, ad esempio per eseguire un report ogni due settimane. È possibile specificare una pianificazione settimanale relativa al giorno, all'ora e ai minuti in cui si desidera eseguire la pianificazione.  
  
 **Mese (criterio di occorrenza)**  
 Consente di specificare le opzioni per l'esecuzione di un'operazione pianificata a intervalli di un mese oppure quando lo schema che si desidera ripetere si basa su mesi. È possibile specificare una pianificazione mensile relativa al giorno, all'ora e ai minuti in cui si desidera eseguire la pianificazione. Dalla pianificazione è possibile omettere mesi specifici.  
  
 **Una volta**  
 Consente di specificare una pianificazione che viene eseguita una sola volta nella data e all'ora specifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto del server di report in Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Eseguire la connessione a un server di report in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [Pianificazioni](../../reporting-services/subscriptions/schedules.md)  
  
  

