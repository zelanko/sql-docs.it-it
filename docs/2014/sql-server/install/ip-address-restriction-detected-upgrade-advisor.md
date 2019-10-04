---
title: Restrizione indirizzi IP rilevata (preparazione aggiornamento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 9a154455-c68f-4403-a3a7-b90f4d35eecb
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 487ced9f103fd10a581841595111f01a5710bd15
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952077"
---
# <a name="ip-address-restriction-detected-upgrade-advisor"></a>Rilevata restrizione degli indirizzi IP (Upgrade Advisor)
  Sono state rilevate una o più restrizioni degli indirizzi IP sul sito Web di IIS che ospita le directory virtuali del server di report o di Gestione report. In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è disponibile il supporto nativo per le restrizioni degli indirizzi IP.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] native.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 Non è possibile definire le restrizioni degli indirizzi IP sugli URL creati per un server di report aggiornato. L'aggiornamento può continuare, ma le restrizioni degli indirizzi IP non saranno definite sugli URL di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="corrective-action"></a>Azione correttiva  
 Dopo l'aggiornamento, utilizzare ISA Server, il software del firewall o un'altra soluzione per consentire o escludere richieste dagli indirizzi IP specifici al server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Preparazione aggiornamento Reporting Services &#40;problemi di aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
