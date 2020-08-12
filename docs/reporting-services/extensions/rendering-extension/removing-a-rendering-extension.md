---
title: Rimozione di un'estensione per il rendering | Microsoft Docs
description: Informazioni su come rimuovere un'estensione per il rendering da Reporting Services in modo che non sia più disponibile per il server di report e per Progettazione report.
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f71fceddd59141516453f9f392f8f913ba20cfad
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529437"
---
# <a name="removing-a-rendering-extension"></a>Rimozione di un'estensione per il rendering
  Per rimuovere un'estensione per il rendering di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], è sufficiente rimuovere l'elemento **Extension** per l'estensione dal file rsreportserver.config, che si trova nella cartella **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<Instance Name>\Reporting Services\ReportServer**. Se sono state create voci per Progettazione report e per un server di report, rimuovere l'elemento **Extension** anche dal [file di configurazione RSReportDesigner](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md). Dopo la rimozione delle informazioni di configurazione, l'estensione per il rendering non è più disponibile per il componente.  
  
## <a name="see-also"></a>Vedere anche  
 [File di configurazione di Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Implementazione di un'estensione per il rendering](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Panoramica delle estensioni per il rendering](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [Implementazione dell'interfaccia IRenderingExtension](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [Considerazioni sulla sicurezza per le estensioni](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [Distribuzione di un'estensione per il rendering](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  
