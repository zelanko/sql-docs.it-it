---
title: Filtri ISAPI rilevati nel sito del server di report (preparazione aggiornamento) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- ISAPI filters
- report servers [Reporting Services], upgrade issues
ms.assetid: dd30560d-9e16-47c7-ba68-a9743a657e4e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a2b811955839eb22e3325d64c55454b92a6b1b8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952438"
---
# <a name="isapi-filters-detected-on-the-report-server-site-upgrade-advisor"></a>Filtri ISAPI rilevati sul sito del server di report (Upgrade Advisor)
  Sono stati rilevati uno o più filtri ISAPI per il sito Web che ospita le directory virtuali del server di report e di Gestione report. I filtri ISAPI non sono supportati [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]in.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Native.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 Prima di eseguire l'aggiornamento, verificare se i filtri ISAPI per il sito Web sono utilizzati da applicazioni [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se il filtro ISAPI non è necessario, è possibile aggiornare il server di report. Verranno creati gli URL predefiniti, senza il supporto per il filtro ISAPI in esecuzione in IIS. Se il filtro ISAPI è necessario, non eseguire l'aggiornamento finché non sarà stata trovata un'alternativa per l'hosting del filtro ISAPI, ad esempio utilizzando ISA Server o continuando a ospitare il filtro ISAPI in IIS. Il server di report supporta ASP.NET HTTPModules come sostituzione per i filtri ISAPI in scenari specifici. Per ulteriori informazioni, vedere la documentazione di ASP.NET in MSDN.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Valutare e utilizzare una soluzione distinta per ospitare i filtri ISAPI richiesti per l'attività di sviluppo.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento Reporting Services &#40;preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
