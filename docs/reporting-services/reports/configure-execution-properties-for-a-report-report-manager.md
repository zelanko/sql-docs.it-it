---
title: Configurare le proprietà di esecuzione per un report (Gestione report) | Microsoft Docs
ms.date: 03/01/2017
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
ms.openlocfilehash: 27508400b63e1fe0cc95b290130d9c122399be32
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570855"
---
# <a name="configure-execution-properties-for-a-report--report-manager"></a>Configurare le proprietà di esecuzione per un report (Gestione report)
  È possibile impostare le opzioni di elaborazione di un report per specificare il momento in cui i dati vengono recuperati per un report specifico. Questa operazione risulta utile per pianificare l'elaborazione dei dati per un report se l'origine dati esterna viene aggiornata a intervalli stabiliti (ad esempio se un data warehouse viene aggiornato su base giornaliera o settimanale) e si desidera evitare l'overhead dovuto al recupero degli stessi dati ogni volta che un report viene richiesto. La pianificazione dell'elaborazione dei dati è utile anche se si desidera controllare il carico di elaborazione nel server di database esterno o quando si desidera fornire risultati coerenti per più utenti che devono utilizzare set di dati identici. Con dati volatili, un report su richiesta può generare risultati diversi anche a differenza di pochi minuti. Uno snapshot del report, invece, consente di eseguire confronti validi con altri report o strumenti analitici contenenti dati riferiti allo stesso momento nel tempo.  
  
 Il termine snapshot del report indica un report che include informazioni sul layout e i risultati di query recuperati in un momento specifico. Diversamente dai report su richiesta, per i quali vengono recuperati risultati di query aggiornati quando si seleziona il report, gli snapshot dei report vengono elaborati in base a una pianificazione e quindi salvati nel server di report. Quando si seleziona uno snapshot per la visualizzazione, il server di report recupera il report archiviato dal database del server di report e visualizza i dati e il layout del report aggiornati al momento della creazione dello snapshot.  
  
 Gli snapshot dei report non vengono salvati in un formato di rendering specifico, ma ne viene eseguito il rendering nel formato di visualizzazione finale, ad esempio HTML, solo quando vengono richiesti da un utente o un'applicazione. Il rendering posticipato rende uno snapshot portabile. È possibile eseguire il rendering del report nel formato corretto per il dispositivo o il browser da cui proviene la richiesta.  
  
### <a name="to-configure-report-processing-options"></a>Per configurare le opzioni relative all'elaborazione dei report  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Selezionare e aprire il report per il quale si desidera impostare le opzioni di elaborazione.  
  
 Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
1.  Scegliere **Gestisci** dal menu a discesa, quindi selezionare la scheda **Opzioni di elaborazione** .  
  
2.  Fare clic su **Esegui il rendering del report da uno snapshot dell'esecuzione del report**, quindi selezionare una delle opzioni seguenti:  
  
    -   Se si desidera creare uno snapshot, selezionare **Usa la pianificazione seguente per creare snapshot dell'esecuzione del report**, quindi definire una pianificazione in base al report oppure selezionare un'opzione dall'elenco **Pianificazione condivisa** .  
  
    -   Se si desidera creare immediatamente uno snapshot, selezionare **Crea uno snapshot del report quando viene scelto il pulsante Applica in questa pagina**.  
  
3.  Fare clic su **Applica**.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare proprietà di elaborazione dei report](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Aprire e chiudere un report &#40;Gestione report&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [Pagina Contenuto &#40;Gestione report&#41;](https://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [Gestione contenuto del server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Pagina delle proprietà Opzioni di elaborazione &#40;Gestione report&#41;](https://msdn.microsoft.com/library/28f07c70-7132-4d15-9505-4fdf31dc9cc0)  
  
  
