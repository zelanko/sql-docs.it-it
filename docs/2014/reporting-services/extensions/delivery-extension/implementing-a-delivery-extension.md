---
title: Implementazione di un'estensione per il recapito | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery [Reporting Services]
- custom delivery extensions [Reporting Services]
- extensions [Reporting Services], delivery
- delivery extensions [Reporting Services]
ms.assetid: 600cd229-efcd-480e-8c95-3c3c39ff4e7a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cae33496e4dddcaf2d14ba2d87f0d4013795e58f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63165138"
---
# <a name="implementing-a-delivery-extension"></a>Implementazione di un'estensione per il recapito
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] consente agli utenti di creare e pubblicare report che, una volta creati e pubblicati, possono essere recapitati a diverse posizioni. 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] include inoltre diverse estensioni per il recapito e un'API di recapito tramite cui gli sviluppatori possono creare estensioni per il recapito aggiuntive per estendere ulteriormente le funzionalità di recapito in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 Per un'implementazione di esempio di un'estensione per il recapito, vedere la pagina degli [esempi del prodotto SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Panoramica sulle estensioni per il recapito] recapito-estensioni-overview.md)  
 Vengono fornite informazioni introduttive per la scrittura di un'estensione per il recapito personalizzata per [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Preparazione all'implementazione di un'estensione per il recapito](preparing-to-implement-a-delivery-extension.md)  
 Vengono descritte le interfacce e le classi disponibili per l'implementazione di un'estensione per il recapito di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], nonché i problemi da considerare prima dell'implementazione.  
  
 [Creazione di una libreria di estensioni per il recapito](creating-a-delivery-extension-library.md)  
 Vengono descritte le operazioni di assegnazione di uno spazio dei nomi per l'estensione per il recapito di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e di compilazione dell'estensione per il recapito nella DLL di una libreria.  
  
 [Implementazione dell'interfaccia IDeliveryExtension per un'estensione per il recapito](implementing-the-ideliveryextension-interface-for-a-delivery-extension.md)  
 Vengono descritti gli attributi di un'estensione per il recapito e come implementare una classe personalizzata dell'estensione per il recapito.  
  
 [Utilizzo della classe Notification per un'estensione per il recapito](using-a-notification-class-for-a-delivery-extension.md)  
 Vengono descritti gli attributi di una classe **Notification** e come usarla nell'implementazione dell'estensione per il recapito.  
  
 [Utilizzo della classe Setting per un'estensione per il recapito](using-the-setting-class-for-a-delivery-extension.md)  
 Vengono descritti gli attributi di una classe **Setting** e come usarla nell'implementazione dell'estensione per il recapito.  
  
 [Utilizzo dell'interfaccia IDeliveryReportServerInformation per un'estensione per il recapito](using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)  
 Vengono descritti gli attributi di una classe **IDeliveryReportServerInformation** e come usarla nell'implementazione dell'estensione per il recapito.  
  
 [Utilizzo della classe Report per un'estensione per il recapito](using-the-report-class-for-a-delivery-extension.md)  
 Vengono descritti gli attributi di una classe **Report** e come usarla nell'implementazione dell'estensione per il recapito.  
  
 [Utilizzo della classe RenderedOutputFile per un'estensione per il recapito](using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
 Vengono descritti gli attributi di una classe **RenderedOutputFile** e come usarla nell'implementazione dell'estensione per il recapito.  
  
 [Implementazione dell'interfaccia ISubscriptionBaseUIUserControl per un'estensione per il recapito](implementing-the-isubscriptionbaseuiusercontrol-interface.md)  
 Vengono descritti gli attributi di un controllo utente di un'estensione per il recapito e come implementare un'interfaccia utente personalizzata per una sottoscrizione.  
  
 [Distribuzione di un'estensione per il recapito](deploying-a-delivery-extension.md)  
 Viene descritto come distribuire un'estensione per il recapito.  
  
 [Esecuzione del debug del codice dell'estensione per il recapito](debugging-delivery-extension-code.md)  
 Viene descritto come eseguire il debug del codice in un'estensione per il recapito.  
  
 [Rimozione di un'estensione per il recapito](removing-a-delivery-extension.md)  
 Viene descritto come rimuovere un'estensione per il recapito da un server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Estensioni di Reporting Services](../reporting-services-extensions.md)   
 [Libreria di estensioni di Reporting Services](../reporting-services-extension-library.md)  
  
  
