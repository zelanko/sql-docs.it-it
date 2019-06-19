---
title: Sono state specificate directory virtuali (Upgrade Advisor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 7d32b560-49d6-4558-b5d6-9127067f82d6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f5e0643fad0a9e554c3c89f1d1c546a7ab69534d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091071"
---
# <a name="virtual-directories-are-unspecified-upgrade-advisor"></a>Non sono state specificate directory virtuali (Upgrade Advisor)
  Non sono state rilevate impostazioni di directory virtuali per il servizio Web ReportServer o Gestione report. Dopo che l'aggiornamento è stato completato, è necessario configurare le prenotazioni URL per il server di report tramite Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 L'aggiornamento di un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] richiede di riservare nuovi URL per il servizio Web ReportServer e Gestione report. Per l'istanza da aggiornare, non sono state rilevate directory virtuali per il server di report o Gestione report. Pertanto, le informazioni disponibili non sono sufficienti per creare prenotazioni URL per il server di report aggiornato. L'aggiornamento può continuare, ma la directory virtuale del server di report o di Gestione report non sarà definita dopo che l'installazione è stata aggiornata.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Dopo l'aggiornamento, utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per impostare gli URL per il server di report e Gestione report. Utilizzare Gestione IIS per rimuovere le directory virtuali non più necessarie.  
  
 Per altre informazioni, vedere [configurare un URL &#40;Gestione configurazione SSRS&#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento di Reporting Services &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
