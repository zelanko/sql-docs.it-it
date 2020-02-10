---
title: Configurare regole business per l'invio di notifiche (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], configuring notifications
- e-mail [Master Data Services], configuring business rules
- notifications [Master Data Services], configuring business rules
ms.assetid: b24f7b11-ab53-4642-999c-e17b543b3558
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: b0ea6e215b5192d1b9e84ed252708b188d5c5a59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483948"
---
# <a name="configure-business-rules-to-send-notifications-master-data-services"></a>Configurare regole business per l'invio di notifiche (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]è possibile configurare le regole di business per inviare notifiche agli utenti relative alle modifiche dei valori di attributo.  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere alle aree funzionali **Amministrazione sistema** e **Autorizzazioni utenti e gruppi** . Se non si dispone dell'autorizzazione per l'area funzionale **Autorizzazioni utenti e gruppi** , non è possibile visualizzare l'elenco di utenti e gruppi cui inviare notifiche.  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   È necessario che sia presente una regola business che utilizza un'azione di convalida. Per altre informazioni, vedere [Creare e pubblicare una regola di business &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md).  
  
-   È necessario che l'utente o il gruppo che riceve la notifica disponga almeno dell'autorizzazione **Sola lettura** per l'attributo la cui convalida ha esito negativo. Gli utenti o gruppi a cui è stata negata in modo esplicito o implicito l'autorizzazione all'attributo riceveranno la posta elettronica ma non potranno accedere all'attributo in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
-   Se i messaggi di posta elettronica vengono inviati a un gruppo, verranno ricevuti dai soli membri del gruppo che hanno effettuato l'accesso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
### <a name="to-configure-business-rules-to-send-notifications"></a>Per configurare le regole business per l'invio di notifiche  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Dalla barra dei menu scegliere **Gestisci** e fare clic su **Regole business**.  
  
3.  Nella pagina **Manutenzione regola business** selezionare un modello dall'elenco **Modello** .  
  
4.  Dall'elenco **Entità** selezionare un'entità.  
  
5.  Dall'elenco **tipo di membro** selezionare un tipo di membro.  
  
6.  Dall'elenco **Attributo** selezionare un attributo o lasciare inalterata l'impostazione predefinita **Tutti**.  
  
7.  Nella griglia fare doppio clic sul campo **notifica** nella riga relativa alla regola business.  
  
8.  Dal sottomenu scegliere un utente o un gruppo a cui inviare la notifica tramite posta elettronica.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   Applicare regole business ai dati eseguendo una delle procedure riportate di seguito:  
  
    -   [Convalidare membri specifici rispetto a regole business &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Convalidare una versione rispetto alle regole business &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   Configurare il protocollo della posta elettronica come riportato di seguito:  
  
    -   [Configurare le notifiche di posta elettronica &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Notifiche &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)   
 [Configurare le notifiche di posta elettronica &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
  
