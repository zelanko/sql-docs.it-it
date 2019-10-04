---
title: Rilevato gruppo di servizi Web ReportServer SQL Server 2005 (preparazione aggiornamento) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- deployment [Reporting Services]
ms.assetid: 699d24eb-7756-4b41-9294-ef1a94b2f267
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bfeff5eae569b481edfcc1cacc89c26e44edaece
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952370"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>Rilevato un gruppo di servizi Web ReportServer di SQL Server 2005 (Upgrade Advisor)
  È stato rilevato che l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è associata a un gruppo di servizi Web ReportServer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non utilizza il gruppo di servizi Web ReportServer di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Quando si esegue l'aggiornamento da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], questo gruppo di servizi viene eliminato e gli elenchi di controllo di accesso (ACL) personalizzati o gli utenti che appartengono al gruppo non vengono mantenuti durante l'aggiornamento.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Prima di eseguire l'aggiornamento, eseguire il backup di tutti gli elenchi di controllo di accesso o utenti che appartengono al gruppo di servizi Web ReportServer di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. A tale scopo, è possibile utilizzare lo strumento da riga di comando **Icacls. exe** in [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2 e versioni successive o lo strumento da riga di comando cacls. exe nei sistemi operativi Windows prima di [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2. Per ulteriori informazioni sulla sintassi per questi strumenti, vedere la documentazione di Windows. Dopo che l'installazione è stata completata, applicare gli elenchi di controllo di accesso personalizzati o gli utenti al gruppo Windows del server di report di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per l'istanza del server di report. Il gruppo di Windows del server di report [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] assume il formato SQLServerReportServerUser $ \<*computer_name*>$ @ no__t-4*instance_name*>.  
  
## <a name="see-also"></a>Vedere anche  
 [Preparazione aggiornamento Reporting Services &#40;problemi di aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
