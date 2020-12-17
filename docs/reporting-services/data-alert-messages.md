---
title: Messaggi di avviso dati | Microsoft Docs
description: 'Informazioni su come avvisi dati di SQL Server Reporting Services consentano di recapitare tramite posta elettronica due tipi di messaggi di avviso dati: messaggi con risultati degli avvisi dati e messaggi con descrizioni degli errori.'
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 6819720c-d848-4b90-9b51-89501b4f4645
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016'
ms.openlocfilehash: 7c7f28e92a29dd355d4b74de2121e1c386816116
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97425337"
---
# <a name="data-alert-messages"></a>Messaggi di avviso dati

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

Gli avvisi dati di SQL Server Reporting Services consentono di recapitare tramite posta elettronica due tipi di messaggi di avviso dati: messaggi con risultati degli avvisi dati e messaggi con descrizioni degli errori. I messaggi con i risultati consentono di tenere informati tutti i destinatari sulle modifiche ai dati dei report di interesse comune e importanti per le decisioni aziendali. Se per qualche motivo si verifica un errore e i risultati non sono disponibili, viene inviato il messaggio di errore.

Il proprietario della definizione di avviso dati può inoltre visualizzare le informazioni sull'istanza di avviso dati in Gestione avvisi dati. Per altre informazioni, vedere [Gestione avvisi dati per utenti di SharePoint](../reporting-services/data-alert-manager-for-sharepoint-users.md).  

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.
  
##  <a name="data-alert-messages"></a><a name="DataAlertMessages"></a> Messaggi di avviso dati  
 Nelle figure seguenti sono illustrati un messaggio di avviso dati con risultati e un messaggio di avviso con una descrizione di un errore.  
  
 **Messaggio dei risultati**  
  
 ![Messaggio di posta elettronica di avviso dati con risultati](../reporting-services/media/rs-alertmessageresults.gif "Messaggio di posta elettronica di avviso dati con risultati")  
  
 **Messaggio di errore**  
  
 ![Messaggio di avviso dati con messaggio di errore](../reporting-services/media/rs-alertmessageerrror.gif "Messaggio di avviso dati con messaggio di errore")  
  
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
  
-   [Creare un avviso dati nella finestra di progettazione Avviso dati](../reporting-services/create-a-data-alert-in-data-alert-designer.md)  
  
-   [Modificare un avviso dati nella finestra di progettazione di avvisi](../reporting-services/edit-a-data-alert-in-alert-designer.md)  

## <a name="see-also"></a>Vedere anche

[Finestra di progettazione Avviso dati](../reporting-services/data-alert-designer.md)   
[Avvisi dati di Reporting Services](../reporting-services/reporting-services-data-alerts.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
