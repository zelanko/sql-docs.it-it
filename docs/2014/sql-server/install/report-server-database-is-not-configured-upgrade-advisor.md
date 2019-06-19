---
title: Database del server di report non è configurato (Upgrade Advisor) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: b964300c-b220-4244-9fa6-c0c6a57760f6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 813319309e489943cfdd94e13f300990b72e94be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092718"
---
# <a name="report-server-database-is-not-configured-upgrade-advisor"></a>Il database del server di report non è configurato (Upgrade Advisor)
  L'aggiornamento è bloccato a causa di una configurazione del server di report incompleta. Il database del server di report non è configurato.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  Modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 L'installazione può aggiornare solo un'istanza del server di report completamente configurata. Per continuare, è necessario configurare il database del server di report, oppure usare Microsoft Windows **Pannello di controllo** per rimuovere funzionalità server di report dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installazione. Dopo la rimozione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è possibile aggiornare gli altri componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Azione correttiva  
 Se il database del server di report non è stato configurato, il server di report non è operativo e deve essere rimosso prima dell'aggiornamento.  
  
 Per ulteriori informazioni sulla disinstallazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vedere [disinstallare Reporting Services 2012](https://technet.microsoft.com/library/hh479745.aspx\(v=sql.11\)). Nell'argomento viene descritto come disinstallare una versione specifica e le procedure sono simili a quelle delle versioni precedenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento di Reporting Services &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
