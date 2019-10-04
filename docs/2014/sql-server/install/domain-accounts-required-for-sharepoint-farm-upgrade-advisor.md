---
title: Account di dominio necessari per la farm di SharePoint (preparazione aggiornamento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 90cd6d3e-a271-4cb8-81f2-fc555b2d3cab
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c4079ea4213d7ecbec0165c32c82b3449bbb5aee
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952514"
---
# <a name="domain-accounts-required-for-sharepoint-farm-upgrade-advisor"></a>Account di dominio richiesti per la farm di SharePoint (Upgrade Advisor)
  I prodotti SharePoint configurati per un ambiente della farm richiedono l'utilizzo di account di dominio.  
  
||  
|-|  
|modalità SharePoint **[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRS](../../includes/ssrs.md)]  
  
### <a name="description"></a>Descrizione  
 I prodotti SharePoint configurati per un ambiente della farm richiedono l'utilizzo di account di dominio per i servizi e le connessioni ai database. È incluso l'account specificato per l'account del servizio Reporting Services.  
  
 Le pagine Amministrazione centrale SharePoint 2010, ad esempio, restituiscono problemi se non si utilizza un account utente di dominio per Reporting Services. Quando si tenta di configurare l'integrazione di Reporting Services, verrà visualizzato un messaggio di errore simile al seguente:  
  
 "Il server di report è in esecuzione con l'account NT AUTHORITY\NETWORK SERVICE predefinito, condizione non supportata dall'installazione di una farm di SharePoint. Riconfigurare il server di report affinché venga eseguito con un account di dominio".  
  
## <a name="corrective-action"></a>Azione correttiva  
 Per [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versioni precedenti, utilizzare il Configuration Manager Reporting Services per modificare l'account assegnato come account del servizio del server di report.  
  
#### <a name="to-change-the-service-account-from-configuration-manager"></a>Per modificare l'account del servizio da Gestione configurazione  
  
1.  Dal menu **Start** selezionare **tutti i programmi**, quindi fare clic su **Microsoft SQL Server 2008 R2**.  
  
2.  Selezionare **strumenti di configurazione**, quindi fare clic su **Reporting Services Configuration Manager**.  
  
3.  In Configuration Manager selezionare la scheda **account del servizio** .  
  
4.  Selezionare **Usa un altro account** e immettere le credenziali per un account di dominio.  
  
5.  Fare clic su **Applica**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
  
  
