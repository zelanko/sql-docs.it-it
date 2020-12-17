---
title: Configurare le proprietà di esecuzione per un report - Reporting Services | Microsoft Docs
description: Informazioni su come impostare le opzioni di elaborazione del report per specificare quando recuperare i dati del report per evitare il sovraccarico del recupero degli stessi dati ogni volta che viene richiesto un report.
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- reports [Reporting Services], properties
- reports [Reporting Services], execution options
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9b1cecda6c4ec085efe7b18392eb06f06866352b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466562"
---
# <a name="configure-execution-properties-for-a-report"></a>Configurare le proprietà di esecuzione per un report
  È possibile impostare le opzioni di elaborazione di un report per specificare il momento in cui i dati vengono recuperati per un report specifico. Questa operazione risulta utile per pianificare l'elaborazione dei dati per un report se l'origine dati esterna viene aggiornata a intervalli stabiliti (ad esempio se un data warehouse viene aggiornato su base giornaliera o settimanale) e si desidera evitare l'overhead dovuto al recupero degli stessi dati ogni volta che un report viene richiesto. La pianificazione dell'elaborazione dei dati è utile anche se si desidera controllare il carico di elaborazione nel server di database esterno o quando si desidera fornire risultati coerenti per più utenti che devono utilizzare set di dati identici. Con dati volatili, un report su richiesta può generare risultati diversi anche a differenza di pochi minuti. Uno snapshot del report, invece, consente di eseguire confronti validi con altri report o strumenti analitici contenenti dati riferiti allo stesso momento nel tempo.  
  
 Il termine snapshot del report indica un report che include informazioni sul layout e i risultati di query recuperati in un momento specifico. Diversamente dai report su richiesta, per i quali vengono recuperati risultati di query aggiornati quando si seleziona il report, gli snapshot dei report vengono elaborati in base a una pianificazione e quindi salvati nel server di report. Quando si seleziona uno snapshot per la visualizzazione, il server di report recupera il report archiviato dal database del server di report e visualizza i dati e il layout del report aggiornati al momento della creazione dello snapshot.  
  
 Gli snapshot dei report non vengono salvati in un formato di rendering specifico, ma ne viene eseguito il rendering nel formato di visualizzazione finale, ad esempio HTML, solo quando vengono richiesti da un utente o un'applicazione. Il rendering posticipato rende uno snapshot portabile. È possibile eseguire il rendering del report nel formato corretto per il dispositivo o il browser da cui proviene la richiesta.  

::: moniker range="=sql-server-2016"
  
## <a name="to-configure-report-processing-options"></a>Per configurare le opzioni relative all'elaborazione dei report  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../web-portal-ssrs-native-mode.md).  
  
2.  Selezionare e aprire il report per il quale si desidera impostare le opzioni di elaborazione.  
  
 Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
1.  Scegliere **Gestisci** dal menu a discesa, quindi selezionare la scheda **Opzioni di elaborazione** .  
  
2.  Fare clic su **Esegui il rendering del report da uno snapshot dell'esecuzione del report**, quindi selezionare una delle opzioni seguenti:  
  
    -   Se si desidera creare uno snapshot, selezionare **Usa la pianificazione seguente per creare snapshot dell'esecuzione del report**, quindi definire una pianificazione in base al report oppure selezionare un'opzione dall'elenco **Pianificazione condivisa** .  
  
    -   Se si desidera creare immediatamente uno snapshot, selezionare **Crea uno snapshot del report quando viene scelto il pulsante Applica in questa pagina**.  
  
3.  Fare clic su **Applica**.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare proprietà di elaborazione dei report](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Pagina Contenuto &#40;Gestione report&#41;](/previous-versions/sql/sql-server-2016/ms186470(v=sql.130))   
 [Gestione contenuto del server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Pagina delle proprietà Opzioni di elaborazione &#40;Gestione report&#41;](/previous-versions/sql/sql-server-2016/ms178821(v=sql.130))  
  
::: moniker-end

::: moniker range=">=sql-server-2017"
  
## <a name="to-configure-report-execution-properties"></a>Per configurare le proprietà di esecuzione dei report  
  
Dal [portale Web di un server di report (modalità nativa SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md):  
  
1. Passare al report per il quale si vogliono configurare le proprietà di esecuzione.  
  
2. Fare clic con il pulsante destro del mouse sul report e scegliere **Gestisci** dal menu a discesa.

3. Selezionare la scheda **Snapshot della cronologia** per visualizzare la pagina **Snapshot della cronologia**.  
  
4. Selezionare il pulsante **Schedules and settings** (Pianificazioni e impostazioni) e selezionare **Creare gli snapshot della cronologia in base a una pianificazione** se non è già selezionato.
  
5. Selezionare una **pianificazione condivisa** o una **pianificazione in base al report** in base alle esigenze.  
  
6. Nella sezione **Avanzate** selezionare il criterio **Conservazione** desiderato per gli snapshot della cronologia.  
  
7. Selezionare **Applica**.  
  
   >[!NOTE]
   >Per creare immediatamente uno snapshot, selezionare il pulsante **Nuovo snapshot della cronologia** invece del pulsante **Schedules and settings** (Pianificazioni e impostazioni). Verrà immediatamente creato uno snapshot del report.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare proprietà di elaborazione dei report](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Gestione del contenuto del server di report (modalità nativa SSRS)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Impostare le proprietà di elaborazione dei report](../../reporting-services/report-server/set-report-processing-properties.md)   

::: moniker-end