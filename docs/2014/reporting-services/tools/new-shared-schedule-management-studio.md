---
title: Nuova pianificazione condivisa (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.newschedule.f1
ms.assetid: b2c69586-d98e-4933-827d-f5e6c15c5203
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 083fa7998e347b3aa3abe7aacbf9585a18047b20
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66100233"
---
# <a name="new-shared-schedule-management-studio"></a>Nuova pianificazione condivisa (Management Studio)
  Questa pagina consente di creare una pianificazione condivisa per l'esecuzione di sottoscrizioni e report pubblicati. È possibile utilizzare le pianificazioni condivise al posto di di pianificazioni specifiche di report o sottoscrizioni. Le informazioni centralizzate sulla pianificazione e la possibilità di sospendere e riprendere le operazioni pianificate costituiscono due funzionalità fondamentali che distinguono le pianificazioni condivise da quelle specifiche degli elementi.  
  
 Non è possibile supportare tutte le combinazioni di frequenze in una singola pianificazione. Ad esempio, se si desidera eseguire un report alle 12.00 e alle 16.00 ogni venerdì è necessario creare due pianificazioni giornaliere, una con giorno di esecuzione venerdì e inizio alle ore 12.00 e l'altra con inizio alle ore 16.00  
  
 L'elaborazione delle pianificazioni si basa sull'orario locale del server di report che ospita ed elabora la pianificazione.  
  
 Per aprire questa pagina, avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], connettersi a un server di report, fare clic con il pulsante destro del mouse su **Pianificazione condivisa**quindi scegliere **Nuova pianificazione**. Per salvare la pianificazione, è necessario che il servizio SQL Server Agent sia in esecuzione.  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473).  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Consente di digitare un nome per la pianificazione condivisa. Questo nome viene visualizzato negli elenchi a discesa quando gli utenti selezionano una pianificazione condivisa per report e sottoscrizioni. Assicurarsi di fornire un nome descrittivo che possa essere inserito facilmente in un elenco e che consenta di distinguere in modo immediato le pianificazioni condivise. Il nome deve includere almeno un carattere alfanumerico. È inoltre possibile utilizzare spazi e alcuni simboli. Il nome non può contenere i caratteri seguenti:  
  
 ; ? : \@ & = + , $ / * \< >  
  
 " /  
  
 **Inizia l'esecuzione della pianificazione il**  
 Consente di specificare la data di inizio della pianificazione.  
  
 **Arresta l'esecuzione della pianificazione il**  
 Consente di impostare la data di scadenza della pianificazione.  
  
 **Tipo**  
 Specifica se il criterio di occorrenza è basato principalmente su ore, giorni, settimane o mesi.  
  
 **Ora (criterio di occorrenza)**  
 Consente di specificare le opzioni per l'esecuzione di un'operazione pianificata a intervalli di ore, ad esempio per eseguire un report ogni 6 ore. È possibile specificare l'intervallo in ore e minuti.  
  
 **Giorno (criterio di occorrenza)**  
 Consente di specificare le opzioni per l'esecuzione di un'operazione pianificata a intervalli di giorni, ad esempio per eseguire un report ogni 2 giorni. È possibile specificare l'intervallo in giorni e impostare l'ora e i minuti in cui si desidera eseguire la pianificazione.  
  
 **Settimana (criterio di occorrenza)**  
 Consente di specificare le opzioni per l'esecuzione di un'operazione pianificata a intervalli settimanali oppure quando lo schema che si desidera ripetere si basa su settimane, ad esempio per eseguire un report ogni due settimane. È possibile specificare una pianificazione settimanale relativa al giorno, all'ora e ai minuti in cui si desidera eseguire la pianificazione.  
  
 **Mese (criterio di occorrenza)**  
 Consente di specificare le opzioni per l'esecuzione di un'operazione pianificata a intervalli mensili oppure quando lo schema che si desidera ripetere si basa su mesi. È possibile specificare una pianificazione mensile relativa al giorno, all'ora e ai minuti in cui si desidera eseguire la pianificazione. Dalla pianificazione è possibile omettere mesi specifici.  
  
 **Una volta**  
 Selezionare questa opzione per creare una pianificazione che viene eseguita una sola volta nella data e all'ora specificate.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto del server di report in Management Studio](report-server-in-management-studio-f1-help.md)   
 [Eseguire la connessione a un server di report in Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Create, Modify, and Delete Schedules](../subscriptions/create-modify-and-delete-schedules.md)   
 [Pianificazioni](../subscriptions/schedules.md)   
 [Guida sensibile al contesto del server di report in Management Studio](report-server-in-management-studio-f1-help.md)  
  
  
