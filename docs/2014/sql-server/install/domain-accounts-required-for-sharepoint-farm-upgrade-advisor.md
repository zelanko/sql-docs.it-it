---
title: Gli account di dominio richiesti per la farm di SharePoint (Upgrade Advisor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 90cd6d3e-a271-4cb8-81f2-fc555b2d3cab
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 983e01046fd90fbaf8d9ff680492f1b385435f61
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253581"
---
# <a name="domain-accounts-required-for-sharepoint-farm-upgrade-advisor"></a>Account di dominio richiesti per la farm di SharePoint (Upgrade Advisor)
  I prodotti SharePoint configurati per un ambiente della farm richiedono l'utilizzo di account di dominio.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRS](../../includes/ssrs.md)]  
  
### <a name="description"></a>Descrizione  
 I prodotti SharePoint configurati per un ambiente della farm richiedono l'utilizzo di account di dominio per i servizi e le connessioni ai database. È incluso l'account specificato per l'account del servizio Reporting Services.  
  
 Le pagine Amministrazione centrale SharePoint 2010, ad esempio, restituiscono problemi se non si utilizza un account utente di dominio per Reporting Services. Quando si tenta di configurare l'integrazione di Reporting Services, verrà visualizzato un messaggio di errore simile al seguente:  
  
 "Il server di report è in esecuzione con l'account NT AUTHORITY\NETWORK SERVICE predefinito, condizione non supportata dall'installazione di una farm di SharePoint. Riconfigurare il server di report affinché venga eseguito con un account di dominio".  
  
## <a name="corrective-action"></a>Azione correttiva  
 Per la [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versioni precedenti, utilizzare Gestione configurazione Reporting Services per modificare l'account assegnato come account di servizio del server di report.  
  
#### <a name="to-change-the-service-account-from-configuration-manager"></a>Per modificare l'account del servizio da Gestione configurazione  
  
1.  Dal **avviare** dal menu **tutti i programmi**, quindi fare clic su **Microsoft SQL Server 2008 R2**.  
  
2.  Selezionare **strumenti di configurazione**, quindi fare clic su **Gestione configurazione Reporting Services**.  
  
3.  In Configuration Manager, selezionare la **Account del servizio** scheda.  
  
4.  Selezionare **Usa un altro account** e immettere le credenziali per un account di dominio.  
  
5.  Fare clic su **Applica**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
  
  
