---
title: Rilevato un gruppo di servizi Web ReportServer di SQL Server 2005 Report (Upgrade Advisor) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- deployment [Reporting Services]
ms.assetid: 699d24eb-7756-4b41-9294-ef1a94b2f267
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4f379675a4d7b37b9eab69598f7c04bc57306d46
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092106"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>Rilevato un gruppo di servizi Web ReportServer di SQL Server 2005 (Upgrade Advisor)
  È stato rilevato che il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza è associata una [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] gruppo di servizio Web ReportServer.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non usa il [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] gruppo di servizio Web ReportServer. Quando si esegue l'aggiornamento da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], questo gruppo di servizi viene eliminato e gli elenchi di controllo di accesso (ACL) personalizzati o gli utenti che appartengono al gruppo non vengono mantenuti durante l'aggiornamento.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Prima di eseguire l'aggiornamento, eseguire il backup di tutti gli elenchi di controllo di accesso o utenti che appartengono al gruppo di servizi Web ReportServer di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. A tale scopo, è possibile usare la **Icacls.exe** dello strumento da riga di comando nella [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2 e versioni successive o lo strumento da riga di comando Cacls.exe nei sistemi operativi Windows precedenti a [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2. Per ulteriori informazioni sulla sintassi per questi strumenti, vedere la documentazione di Windows. Dopo che l'installazione è stata completata, applicare gli elenchi di controllo di accesso personalizzati o gli utenti al gruppo Windows del server di report di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per l'istanza del server di report. Il [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] gruppo di Windows Server di Report di assume la forma SQLServerReportServerUser$\<*nome_computer*>$\<*nome_istanza*>.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento di Reporting Services &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
