---
title: Programma di rilevata restrizione degli indirizzi IP (Upgrade Advisor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 9a154455-c68f-4403-a3a7-b90f4d35eecb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ec72f58aaa0a10d0fa13860bc39e81b717d0ff89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094182"
---
# <a name="ip-address-restriction-detected-upgrade-advisor"></a>Rilevata restrizione degli indirizzi IP (Upgrade Advisor)
  Sono state rilevate una o più restrizioni degli indirizzi IP sul sito Web di IIS che ospita le directory virtuali del server di report o di Gestione report. In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è disponibile il supporto nativo per le restrizioni degli indirizzi IP.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Nativo.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 Non è possibile definire le restrizioni degli indirizzi IP sugli URL creati per un server di report aggiornato. L'aggiornamento può continuare, ma le restrizioni degli indirizzi IP non saranno definite sugli URL di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="corrective-action"></a>Azione correttiva  
 Dopo l'aggiornamento, utilizzare ISA Server, il software del firewall o un'altra soluzione per consentire o escludere richieste dagli indirizzi IP specifici al server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento di Reporting Services &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
