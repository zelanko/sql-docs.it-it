---
title: Implementazione di un'estensione per il rendering | Microsoft Docs
description: Informazioni su come trasformare le informazioni sul layout e i dati dei report di Reporting Services in formati specifici dei dispositivi implementando le estensioni per il rendering.
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- rendering extensions [Reporting Services]
- custom rendering extensions [Reporting Services]
- transformations [Reporting Services]
- extensions [Reporting Services], rendering
- rendering extensions [Reporting Services], implementing
ms.assetid: 4a5c64f5-2391-4597-ba3f-81d265b23703
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d61af9bd987256a2ad293f7f9566fd1a2bcd041e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529087"
---
# <a name="implementing-a-rendering-extension"></a>Implementazione di un'estensione per il rendering
  Un'estensione per il rendering è un componente o un modulo di un server di report che consente di trasformare le informazioni sul layout e i dati del report in un formato specifico del dispositivo. SQL Server Reporting Services include sei estensioni per il rendering: HTML, Excel, Word, CSV o testo, XML, immagine e PDF. È possibile creare estensioni per il rendering aggiuntive per generare report in altri formati.  
  
> [!NOTE]  
>  Per determinare quali sono le estensioni per il rendering disponibili, è possibile visualizzare l'elenco delle estensioni installate nel file RSReportServer.config.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Panoramica delle estensioni per il rendering](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
 Vengono fornite informazioni introduttive per la scrittura di un'estensione per il rendering personalizzata per [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Implementazione dell'interfaccia IRenderingExtension](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)  
 Vengono descritti gli attributi di un'estensione per il rendering.  
  
 [Distribuzione di un'estensione per il rendering](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
 Viene descritto come distribuire un'estensione per il rendering in un server di report.  
  
 [Rimozione di un'estensione per il rendering](../../../reporting-services/extensions/rendering-extension/removing-a-rendering-extension.md)  
 Viene descritto come rimuovere un'estensione per il rendering da un server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Libreria di estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
