---
title: Rimozione di un'estensione per il rendering | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 77a8a9ac44b35f338f978913985617e4f264ddb7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62988056"
---
# <a name="removing-a-rendering-extension"></a>Rimozione di un'estensione per il rendering
  Per rimuovere un [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] estensione per il rendering, rimuovere semplicemente il `Extension` (elemento) per l'estensione per il rendering dal file RSReportServer. config, situato nella **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\< Nome istanza > Services\ReportServer.** cartella. Se sono state create voci per una finestra di progettazione di Report, nonché un server di report, rimuovere il `Extension` elemento il [RSReportDesigner Configuration File](../../report-server/rsreportdesigner-configuration-file.md) anche. Dopo la rimozione delle informazioni di configurazione, l'estensione per il rendering non è più disponibile per il componente.  
  
## <a name="see-also"></a>Vedere anche  
 [File di configurazione di Reporting Services](../../report-server/reporting-services-configuration-files.md)   
 [Implementazione di un'estensione per il rendering](implementing-a-rendering-extension.md)   
 [Panoramica delle estensioni per il rendering](rendering-extensions-overview.md)   
 [Implementazione dell'interfaccia IRenderingExtension](implementing-the-irenderingextension-interface.md)   
 [Considerazioni sulla sicurezza per le estensioni](../security-considerations-for-extensions.md)   
 [Distribuzione di un'estensione per il rendering](deploying-a-rendering-extension.md)  
  
  
