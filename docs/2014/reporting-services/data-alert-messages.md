---
title: Messaggi di avviso dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6819720c-d848-4b90-9b51-89501b4f4645
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93991a067fdb547232471b48f391d057469aa751
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78173880"
---
# <a name="data-alert-messages"></a>Messaggi di avviso dati
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Gli avvisi dati di Reporting Services consentono di recapitare due tipi di messaggi di avviso dati tramite posta elettronica: messaggi con risultati degli avvisi dati e messaggi con descrizioni degli errori. I messaggi con i risultati consentono di tenere informati tutti i destinatari sulle modifiche ai dati dei report di interesse comune e importanti per le decisioni aziendali. Se per qualche motivo si verifica un errore e i risultati non sono disponibili, viene inviato il messaggio di errore.

 Il proprietario della definizione di avviso dati può inoltre visualizzare le informazioni sull'istanza di avviso dati in Gestione avvisi dati. Per altre informazioni, vedere [Gestione avvisi dati per utenti di SharePoint](../../2014/reporting-services/data-alert-manager-for-sharepoint-users.md).

##  <a name="data-alert-messages"></a><a name="DataAlertMessages"></a>Messaggi di avviso dati
 Nelle figure seguenti sono illustrati un messaggio di avviso dati con risultati e un messaggio di avviso con una descrizione di un errore.

 **Messaggio dei risultati**

 ![Messaggio di posta elettronica di avviso dati con risultati](media/rs-alertmessageresults.gif "Messaggio di posta elettronica di avviso dati con risultati")

 **Messaggio di errore**

 ![Messaggio di avviso dati con messaggio di errore](media/rs-alertmessageerrror.gif "Messaggio di avviso dati con messaggio di errore")

 I messaggi includono gli stessi tipi di informazioni.

1.  **Per conto di** contiene il nome dell'utente che ha creato la definizione di avviso dati.

2.  Se nella definizione di avviso è stata fornita una descrizione, viene visualizzata al di sotto di **Per conto di**.

3.  **Risultati degli avvisi** indica le righe nel feed di dati del report che soddisfano le regole specificate nella definizione di avviso in formato tabulare, in alternativa contiene una descrizione dell'errore. Non vi sono limiti al numero di righe visualizzate.

4.  **Vai a report** è un collegamento al report in base al quale viene compilata la definizione di avviso. Se il collegamento non è valido perché il report è stato spostato o eliminato, viene visualizzato un messaggio di errore.

5.  **Regole** indica le regole e le clausole nella definizione di avviso. Queste informazioni consentono di verificare e comprendere i risultati degli avvisi e di identificare le regole nella definizione di avviso dati che potrebbe essere necessario modificare per restringere o ampliare i risultati.

6.  **Parametri report** indica i parametri e i valori dei parametri usati per l'esecuzione del report. I parametri e i valori dei parametri aiutano a comprendere i risultati degli avvisi.

7.  **Contextual values** (Valori contestuali) indica i nomi e i valori degli elementi del report esterni alle aree dati del report. Tali elementi sono in genere costituiti da caselle di testo. Ad esempio, una casella di testo con un valore costante come l'oggetto o la descrizione di un report.

 L'unica differenza tra i due tipi di messaggi è l'elemento 5, **Risultati degli avvisi**. Se si verifica un errore quando viene creato un messaggio di avviso o un'istanza di avviso dati, in **Risultati degli avvisi** viene visualizzato un messaggio di errore che descrive il problema. Il messaggio di errore, inviato a tutti i destinatari, serve per comunicare che i risultati degli avvisi attesi e che potrebbero essere necessari per prendere decisioni aziendali non sono disponibili.

 

##  <a name="related-tasks"></a><a name="HowTo"></a> Attività correlate
 In questa sezione vengono elencate le procedure in cui viene illustrato come creare e modificare le definizioni di avviso dati che forniscono molte delle informazioni incluse nei messaggi di avviso dati.

-   [Creare un avviso dati nella finestra di progettazione Avviso dati](create-a-data-alert-in-data-alert-designer.md)

-   [Modificare un avviso dati nella finestra di progettazione di avvisi](edit-a-data-alert-in-alert-designer.md)



## <a name="see-also"></a>Vedere anche
 [Finestra di progettazione Avviso dati](../../2014/reporting-services/data-alert-designer.md) [Reporting Services avvisi dati](../ssms/agent/alerts.md)


