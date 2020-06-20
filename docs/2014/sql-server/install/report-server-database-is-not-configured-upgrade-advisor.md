---
title: Il database del server di report non è configurato (preparazione aggiornamento) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: b964300c-b220-4244-9fa6-c0c6a57760f6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8800951a2edfa3a71643ba3af65bae2b7cfdc29f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011843"
---
# <a name="report-server-database-is-not-configured-upgrade-advisor"></a>Il database del server di report non è configurato (Upgrade Advisor)
  L'aggiornamento è bloccato a causa di una configurazione del server di report incompleta. Il database del server di report non è configurato.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  Modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 L'installazione può aggiornare solo un'istanza del server di report completamente configurata. Per continuare, è necessario configurare il database del server di report oppure utilizzare il **Pannello di controllo** di Microsoft Windows per rimuovere la funzionalità del server di report dall' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installazione di. Dopo la rimozione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è possibile aggiornare gli altri componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Azione correttiva  
 Se il database del server di report non è stato configurato, il server di report non è operativo e deve essere rimosso prima dell'aggiornamento.  
  
 Per ulteriori informazioni sulla disinstallazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vedere [Uninstall Reporting Services 2012](https://technet.microsoft.com/library/hh479745.aspx\(v=sql.11\)). Nell'argomento viene descritto come disinstallare una versione specifica e le procedure sono simili a quelle delle versioni precedenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento Reporting Services &#40;preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
