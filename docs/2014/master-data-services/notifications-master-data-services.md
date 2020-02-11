---
title: Notifiche (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- notifications [Master Data Services]
- notifications [Master Data Services], about notifications
- e-mail [Master Data Services]
- e-mail [Master Data Services], about e-mail notifications
ms.assetid: d7ad32d5-9fe5-48fd-8c61-0b00c0aff082
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 54f8cdc55322144414be11dd837bd723b4ed3c10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65478975"
---
# <a name="notifications-master-data-services"></a>Notifiche (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]può essere configurato per inviare una notifica tramite posta elettronica quando la convalida delle regole business ha esito negativo o se lo stato di una versione del modello viene modificato.  
  
## <a name="how-notifications-are-sent"></a>Modalità di invio delle notifiche  
 È possibile configurare notifiche in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Le notifiche inviano messaggi di posta elettronica utilizzando posta elettronica database nell' [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] istanza di che [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ospita il database. Per altre informazioni su Posta elettronica database, vedere la sezione [Oggetti di configurazione di Posta elettronica database](../relational-databases/database-mail/database-mail-configuration-objects.md) nella documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="when-notifications-are-sent"></a>Quando vengono inviate le notifiche  
 Dopo la configurazione delle notifiche, è possibile inviare notifiche automatiche tramite posta elettronica nelle due istanze seguenti.  
  
|Istanza|Descrizione|  
|--------------|-----------------|  
|La convalida dei dati tramite regole business ha esito negativo|È necessario configurare singole regole business per l'invio di posta elettronica quando la convalida tramite regole business di un valore di attributo ha esito negativo. Per altre informazioni, vedere [Configurare le regole di business per l'invio di notifiche &#40;Master Data Services&#41;](configure-business-rules-to-send-notifications-master-data-services.md).|  
|Lo stato della versione di un modello viene modificato|Ogni volta che lo stato della versione di un modello viene modificato, vengono inviate automaticamente notifiche agli utenti configurati come amministratori del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).|  
  
## <a name="system-settings"></a>Impostazioni sistema  
 Alcune impostazioni di [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] hanno effetto sulle notifiche. È possibile regolare tali impostazioni in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] o direttamente nella tabella Impostazioni sistema del database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Per altre informazioni, vedere [Impostazioni di sistema &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Configurare [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] per inviare notifiche di posta elettronica.|[Configurare le notifiche di posta elettronica &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)|  
|Configurare [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] per inviare notifiche quando i valori dell'attributo vengono modificati.|[Configurare regole business per l'invio di notifiche &#40;Master Data Services&#41;](configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Regole business &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [Versioni &#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
-   [Risoluzione dei problemi relativi alle notifiche tramite posta elettronica (Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  
