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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62988056"
---
# <a name="removing-a-rendering-extension"></a>Rimozione di un'estensione per il rendering
  Per rimuovere un' [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] estensione per il rendering, è `Extension` sufficiente rimuovere l'elemento per l'estensione per il rendering dal file RSReportServer. config, che si trova in **%Programmi%\Microsoft SQL Server \ MSRS10_50.\< Nome istanza> cartella Services\ReportServer \Reporting** . Se sono state apportate voci per un Progettazione report e un server di report, `Extension` rimuovere anche l'elemento dal [file di configurazione RSReportDesigner](../../report-server/rsreportdesigner-configuration-file.md) . Dopo la rimozione delle informazioni di configurazione, l'estensione per il rendering non è più disponibile per il componente.  
  
## <a name="see-also"></a>Vedere anche  
 [File di configurazione di Reporting Services](../../report-server/reporting-services-configuration-files.md)   
 [Implementazione di un'estensione per il rendering](implementing-a-rendering-extension.md)   
 [Panoramica delle estensioni per il rendering](rendering-extensions-overview.md)   
 [Implementazione dell'interfaccia IRenderingExtension](implementing-the-irenderingextension-interface.md)   
 [Considerazioni sulla sicurezza per le estensioni](../security-considerations-for-extensions.md)   
 [Distribuzione di un'estensione per il rendering](deploying-a-rendering-extension.md)  
  
  
