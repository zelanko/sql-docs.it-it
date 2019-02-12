---
title: 'Nuova pianificazione: Modifica pianificazione pagina (gestione Report) | Microsoft Docs'
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 52a4d250-e185-4116-a29c-d809940a00fb
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 97af25216bd0f1e30531fcb43e182672cd299ac6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034548"
---
# <a name="new-schedule-edit-schedule-page-report-manager"></a>Nuova pianificazione: Modifica pianificazione (gestione Report)
  Utilizzare la pagina Nuova pianificazione/Modifica pianificazione per creare una pianificazione per un report. Le pianificazioni vengono utilizzate con le sottoscrizioni, per aggiornare i report memorizzati nella cache e per creare snapshot autonomi o nella cronologia dei report.  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 È possibile creare pianificazioni solo per i report eseguibili in modo automatico. Per l'esecuzione automatica di un report è necessario archiviare le credenziali per l'origine dati del report nel database del server di report. Per altre informazioni, vedere [pagina delle proprietà origini dati &#40;gestione Report&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md).  
  
 Non è possibile supportare tutte le combinazioni di frequenze in una singola pianificazione. Ad esempio, se si desidera eseguire un report alle 12.00 e alle 16.00 ogni venerdì è necessario creare due pianificazioni giornaliere, una con giorno di esecuzione venerdì e inizio alle ore 12.00 e l'altra con inizio alle ore 16.00  
  
 L'elaborazione delle pianificazioni si basa sull'orario locale del server di report che ospita ed elabora la pianificazione.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare le procedure riportate di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-execution-properties-page-of-a-report"></a>Per aprire la pagina Nuova pianificazione o Modifica pianificazione dalla pagina delle proprietà Esecuzione di un report  
  
1.  Aprire Gestione report e individuare il report per il quale si desidera configurare una pianificazione.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà Generale per il modello.  
  
4.  Selezionare la scheda **Esecuzione** .  
  
5.  Selezionare l'opzione **Esegui il rendering del report da uno snapshot dell'esecuzione del report**. Successivamente selezionare **Usa la pianificazione seguente per aggiungere snapshot alla cronologia del report**, quindi **Pianificazione in base al report**. Fare clic su **Configura**.  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-history-properties-page-of-a-report"></a>Per aprire la pagina Nuova pianificazione o Modifica pianificazione dalla pagina delle proprietà Cronologia di un report  
  
1.  Aprire Gestione report e individuare il report per il quale si desidera configurare una pianificazione.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà Generale per il modello.  
  
4.  Selezionare la scheda **Cronologia** .  
  
5.  Selezionare **Usa la pianificazione seguente per aggiungere snapshot alla cronologia del report**, quindi **Pianificazione in base al report**. Fare clic su **Configura**.  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-subscriptions-page"></a>Per aprire la pagina Nuova pianificazione o Modifica pianificazione dalla pagina Sottoscrizioni  
  
1.  Aprire Gestione report e individuare il report per il quale si desidera configurare una pianificazione.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Nel menu a discesa  
  
    -   fare clic su **Gestisci**. Verrà visualizzata la pagina delle proprietà Generale per il report. Selezionare la scheda **Sottoscrizioni** .  
  
    -   Fare clic su **Sottoscrivi**. Verrà visualizzata la pagina delle proprietà **Sottoscrizioni** per il report.  
  
4.  Nella barra degli strumenti fare clic su **Nuova sottoscrizione** o selezionare una sottoscrizione esistente da modificare.  
  
5.  In **Opzioni di elaborazione sottoscrizione**, fare clic su **Nuova pianificazione**.  
  
## <a name="options"></a>Opzioni  
 **Dettagli pianificazione**  
 Selezionare le opzioni per stabilire quando eseguire il report e con quale frequenza. Le opzioni relative alla frequenza sono suddivise in due gruppi. Il primo set di opzioni consente di specificare la frequenza (oraria, giornaliera, settimanale e così via). Il secondo set di opzioni varia a seconda dell'opzione selezionata nel primo gruppo.  
  
-   **Ora** definisce una pianificazione eseguita a intervalli di ore. Utilizzare le opzioni nella sezione **Date di inizio e fine** per specificare il giorno di esecuzione della pianificazione.  
  
-   **Giorno** definisce una pianificazione eseguita nei giorni selezionati a un'ora specifica. È possibile specificare i giorni nei modi seguenti: Ogni \< *giorno*>, ogni giorno feriale e ogni \< *numero*> giorni. La selezione di un'opzione determina la disattivazione delle altre anche se può sembrare che siano selezionati altri giorni.  
  
-   **Settimana** definisce una pianificazione eseguita settimanalmente a un'ora specifica. È possibile impostare un intervallo di una o più settimane intere (ad esempio, ogni due settimane) oppure di alcuni giorni della settimana.  
  
-   **Mese** definisce una pianificazione eseguita su base mensile. Per una pianificazione mensile è possibile scegliere un giorno in base a uno schema (ad esempio l'ultima domenica di ogni mese) oppure date specifiche (ad esempio 1 e 15 per indicare il primo e il quindicesimo giorno di ogni mese). Per specificare più giorni e intervalli è possibile utilizzare virgole e trattini, ad esempio, 1, 5, 7-12, 21.  
  
-   **Singola occorrenza** definisce una pianificazione eseguita una sola volta. Utilizzare le opzioni nella sezione **Date di inizio e fine** per specificare il giorno di esecuzione della pianificazione. La pianificazione scade subito dopo l'elaborazione.  
  
 **Date di inizio e fine**  
 Consente di specificare le date di inizio e fine, ovvero la data di attivazione e la data di scadenza della pianificazione.  
  
 La scadenza delle pianificazioni non viene notificata. Dopo la data di scadenza, le pianificazioni non vengono più eseguite. Le pianificazioni scadute non vengono comunque eliminate. È possibile eliminare le pianificazioni solo manualmente in modo che sia possibile estendere la data di fine nel caso si scelga di mantenere attiva la pianificazione dopo la scadenza iniziale.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Create, Modify, and Delete Schedules](subscriptions/create-modify-and-delete-schedules.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
