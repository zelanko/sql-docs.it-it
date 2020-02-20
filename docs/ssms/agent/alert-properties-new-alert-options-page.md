---
title: Proprietà avviso - Nuovo avviso (pagina Opzioni)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 89404b754b51edfbe5a1bd36b7f4e5999f50fb39
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75254516"
---
# <a name="alert-properties---new-alert-options-page"></a>Proprietà avviso - Nuovo avviso (pagina Opzioni)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa pagina per visualizzare e modificare le opzioni per gli avvisi di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  

## <a name="options"></a>Opzioni  
**Posta elettronica**  
Consente di includere l'eventuale testo dell'errore risultante dall'evento nelle notifiche inviate tramite posta elettronica.  
  
**Cercapersone**  
Consente di includere l'eventuale testo dell'errore risultante dall'evento nelle notifiche inviate tramite cercapersone.  
  
**Net Send**  
Consente di includere l'eventuale testo dell'errore risultante dall'evento nelle notifiche Net Send.  
  
**Messaggio di notifica aggiuntivo da inviare**  
Consente di digitare un testo aggiuntivo da includere nei messaggi di notifica.  
  
**Intervallo tra le risposte**  
Consente di specificare un ritardo per le occorrenze ripetute dell'evento. È possibile che alcuni eventi si verifichino frequentemente durante un breve periodo di tempo. In questo caso, è possibile che si desideri sapere che l'evento si è verificato ma che non si desideri ricevere una risposta per ogni evento. Utilizzare questa opzione per specificare un valore di timeout. Se si specifica un ritardo, dopo la risposta dell'avviso a un evento, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent rimarrà in attesa per il periodo di tempo specificato prima di rispondere di nuovo, indipendentemente dal fatto che l'evento si verifichi o meno durante il ritardo.  
  
**Minutes**  
Consente di specificare un ritardo in minuti. Per attivare una risposta ogni volta che si verifica l'evento, specificare 0 minuti e 0 secondi.  
  
**Secondi**  
Consente di specificare un ritardo in secondi. Per attivare una risposta ogni volta che si verifica l'evento, specificare 0 minuti e 0 secondi.  
  
## <a name="see-also"></a>Vedere anche  
[Avvisi](../../ssms/agent/alerts.md)  
  
