---
title: Implementazione dell'interfaccia IDeliveryExtension per un'estensione per il recapito | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 229d08da8be91a462b243fbb5580395fd03867ed
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "63193647"
---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>Implementazione dell'interfaccia IDeliveryExtension per un'estensione per il recapito
  La classe di estensioni per il recapito viene utilizzata per recapitare le notifiche dei report agli utenti in base al contenuto delle notifiche. La classe di estensioni per il recapito fornisce anche l'infrastruttura per la convalida delle impostazioni utente passate all'estensione per il recapito. Questa classe deve inoltre contenere proprietà specifiche che i client possono utilizzare per ottenere informazioni sul nome dell'estensione, sulle impostazioni supportate dall'estensione e sui formati di rendering disponibili per l'estensione per il recapito.  
  
 ![Processo dell'interfaccia IDeliveryExtension](../../../reporting-services/extensions/delivery-extension/media/bk-ext-02.gif "Processo dell'interfaccia IDeliveryExtension")  
L'interfaccia IDeliveryExtension consente la convalida dei dati utente e fornisce ai client informazioni sulle impostazioni di recapito necessarie  
  
 Per creare un'estensione per il recapito, implementare <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> e <xref:Microsoft.ReportingServices.Interfaces.IExtension>. L'interfaccia **IDeliveryExtension** consente all'estensione per il recapito di recapitare notifiche dei report tramite il metodo <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> e di convalidare le impostazioni dell'estensione in ingresso tramite il metodo <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A>. L'interfaccia **IExtension** consente all'estensione per il recapito di implementare un nome di estensione localizzato e di elaborare le informazioni di configurazione specifiche dell'estensione archiviate nel file di configurazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Grazie all'implementazione di **IExtension**, l'estensione per il recapito contiene la proprietà <xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A>. È consigliabile che le estensioni per il recapito di [!INCLUDE[ssRS](../../../includes/ssrs.md)] supportino la proprietà **LocalizedName**, in modo che gli utenti possano visualizzare un nome familiare per l'estensione in un'interfaccia utente, ad esempio Gestione report.  
  
 L'estensione per il recapito deve implementare anche la proprietà **ExtensionSettings** dell'interfaccia **IDeliveryExtension**. Il server di report utilizza il valore restituito dalla proprietà <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> per valutare le impostazioni necessarie per un'estensione per il recapito. I client che interagiscono con le estensioni per il recapito utilizzano il metodo <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> del servizio Web ReportServer per restituire un elenco di impostazioni per l'estensione per il recapito.  
  
 È inoltre possibile utilizzare la classe di estensioni per il recapito per recuperare ed elaborare i dati di configurazione personalizzati archiviati nel file RSReportServer.config. Per ulteriori informazioni sull'elaborazione dei dati di configurazione personalizzati, vedere il metodo <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 Per un'implementazione di esempio della classe **IDeliveryExtension**, vedere la pagina degli [esempi del prodotto SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di un'estensione per il recapito](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Libreria di estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
