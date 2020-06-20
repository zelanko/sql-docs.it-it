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
ms.openlocfilehash: 70be2b9c4e7abd55daaa752830a73cbe6e222659
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054670"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>Rilevato un gruppo di servizi Web ReportServer di SQL Server 2005 (Upgrade Advisor)
  È stato rilevato che l' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza è associata a un [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] gruppo di servizi Web ReportServer.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità nativa.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]non [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Usa il [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Gruppo di servizi Web ReportServer. Quando si esegue l'aggiornamento da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], questo gruppo di servizi viene eliminato e gli elenchi di controllo di accesso (ACL) personalizzati o gli utenti che appartengono al gruppo non vengono mantenuti durante l'aggiornamento.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Prima di eseguire l'aggiornamento, eseguire il backup di tutti gli elenchi di controllo di accesso o utenti che appartengono al gruppo di servizi Web ReportServer di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. A tale scopo, è possibile usare lo strumento da riga di comando **Icacls.exe** in [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2 e versioni successive o lo strumento da riga di comando Cacls.exe nei sistemi operativi Windows precedenti a [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2. Per ulteriori informazioni sulla sintassi per questi strumenti, vedere la documentazione di Windows. Dopo che l'installazione è stata completata, applicare gli elenchi di controllo di accesso personalizzati o gli utenti al gruppo Windows del server di report di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per l'istanza del server di report. Il [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] gruppo di Windows del server di report assume il formato SQLServerReportServerUser $ \<*computer_name*> $ \<*instance_name*> .  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento Reporting Services &#40;preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
