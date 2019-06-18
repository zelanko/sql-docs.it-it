---
title: Using a Notification Class for a Delivery Extension (Uso della classe Notification per un'estensione per il recapito) | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], notifications
- notifications [Reporting Services]
- retry queues
- Nofication class
ms.assetid: 549c40c4-d33d-46c2-9d6a-7bbb671ac67a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ad2792a390597223a98b8606af4cb361d17b9e8d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193675"
---
# <a name="using-a-notification-class-for-a-delivery-extension"></a>Utilizzo della classe Notification per un'estensione per il recapito
  La classe <xref:Microsoft.ReportingServices.Interfaces.Notification> si trova nello spazio dei nomi <xref:Microsoft.ReportingServices.Interfaces> e rappresenta le informazioni sulla sottoscrizione utilizzate dalle estensioni per il recapito per recapitare i report. La classe <xref:Microsoft.ReportingServices.Interfaces.Notification> fornisce numerose proprietà che possono essere utilizzate per eseguire il rendering dei report per il recapito, determinare lo stato della notifica e impostare i dati degli utenti.  
  
 ![Processo di notifica del report](../../../reporting-services/extensions/delivery-extension/media/bk-ext-03.gif "Processo di notifica del Report")  
La notifica rappresenta l'oggetto centrale di qualsiasi tipo di recapito  
  
 Quando viene generato un evento associato a una sottoscrizione che utilizza l'estensione per il recapito personalizzata, viene creata una notifica contenente un oggetto <xref:Microsoft.ReportingServices.Interfaces.Report>. L'oggetto <xref:Microsoft.ReportingServices.Interfaces.Report> incapsula le funzionalità necessarie per eseguire il rendering di un determinato report in un formato di rendering supportato e contiene proprietà specifiche del report, ad esempio il nome del report e il suo URL nel server. Per altre informazioni sulla classe<xref:Microsoft.ReportingServices.Interfaces.Report>, vedere [Uso della classe di Report per l'estensione per il recapito](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md).  
  
 L'oggetto <xref:Microsoft.ReportingServices.Interfaces.Notification> viene passato al metodo <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> dell'estensione per il recapito. Il metodo <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> deve contenere codice specifico per l'elaborazione della notifica e il recapito del report.  
  
 Per un esempio su come usare la classe <xref:Microsoft.ReportingServices.Interfaces.Notification>, vedere [ Esempi del prodotto Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="retry-functionality"></a>Funzionalità di ripetizione dei tentativi  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] consente di creare una coda di tentativi per le notifiche che non possono essere recapitate immediatamente. Dopo che il server di report richiama il metodo <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> di un'estensione per il recapito, l'estensione può richiedere che il server di report esegua un nuovo tentativo di recapito in un momento successivo. Se questo si verifica, il server di report inserisce la notifica in una coda interna ed esegue un nuovo tentativo di recapito dopo che è trascorso un determinato intervallo di tempo. Gli amministratori possono configurare il numero massimo di tentativi eseguiti dal server di report e l'intervallo tra i tentativi nella sezione dell'estensione per il recapito del file RSReportServer.config usando l'elemento XML **MaxNumberOfRetries** e l'elemento XML **PeriodBetweenRetries**. Le notifiche vengono rimosse dalla coda di tentativi se in un secondo momento il recapito ha esito positivo o se viene raggiunto il numero massimo di tentativi. Se non è possibile effettuare il recapito dopo il numero massimo di tentativi, la notifica viene eliminata.  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di un'estensione per il recapito](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Libreria di estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
