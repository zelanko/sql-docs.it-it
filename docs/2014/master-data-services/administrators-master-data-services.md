---
title: Amministratori (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], about administrators
- administrators [Master Data Services]
- models [Master Data Services], administrators
ms.assetid: d330aa4e-6ade-4b09-b376-1b15d6c78f7d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: aeedc1f735fd296169f704b794d1bb0e69adab22
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972271"
---
# <a name="administrators-master-data-services"></a>Amministratori (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] sono presenti due tipi di amministratore: gli amministratori di modelli e l'amministratore di sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## <a name="model-administrators"></a>Amministratori di modelli  
 In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , un amministratore di modelli è un utente che dispone dell'autorizzazione **aggiornamento** assegnata all'oggetto modello di livello superiore nella scheda **oggetti modello** e senza altre autorizzazioni assegnate.  
  
-   Se l'utente dispone dell'accesso all'area funzionale **Esplora risorse** , l'utente può aggiungere, eliminare e aggiornare tutti i dati master in questa area.  
  
-   Se l'utente dispone di accesso ad altre aree funzionali, questo utente può eseguire tutte le attività amministrative disponibili nell'area funzionale.  
  
 Ogni modello può avere più amministratori. Ogni utente può essere un amministratore di uno, alcuni o tutti i modelli della distribuzione [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 Un utente può essere configurato come amministratore di modelli in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] o a livello di codice. Per altre informazioni, vedere [Creare un amministratore di modelli &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md).  
  
## <a name="master-data-services-system-administrator"></a>Amministratore del sistema Master Data Services  
 Esiste un solo amministratore del sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. L'amministratore di sistema è l'utente specificato per l' **account Administrator** quando si crea il [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database.  
  
 L'amministratore del sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]:  
  
-   Dispone automaticamente dell'accesso a tutte le aree funzionali.  
  
-   Consente di aggiungere, eliminare e aggiornare tutti i dati master per tutti i modelli nell'area funzionale **Esplora** .  
  
 È possibile modificare l'utente assegnato come amministratore del sistema. Per ulteriori informazioni, vedere [modificare l'account amministratore di sistema &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
## <a name="comparing-administrator-types"></a>Confronto tra tipi di amministratore  
  
|Tipo di amministratore|Description|  
|------------------------|-----------------|  
|Amministratore del sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|Le autorizzazioni assegnate in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] non influiscono sull'accesso dell'amministratore.<br /><br /> Dispone automaticamente dell'autorizzazione **aggiornamento** per tutti i modelli.<br /><br /> Dispone automaticamente dell'accesso a tutte le aree funzionali.<br /><br /> In MDM. tblUser il valore nella colonna **ID** è **1**.|  
|Amministratore di modelli|Le autorizzazioni assegnate in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] determinano se l'utente è o meno un amministratore di modelli.<br /><br /> Può essere un amministratore di modelli in base alle autorizzazioni assegnate in modo esplicito o in base alle autorizzazioni ereditate da un gruppo.<br /><br /> È un amministratore solo per i modelli che dispongono dell'autorizzazione **aggiornamento** assegnata all'oggetto modello di livello superiore e non altre autorizzazioni.<br /><br /> Dispone dell'accesso solo alle aree funzionali per le quali è stato concesso l'accesso.<br /><br /> In MDM. tblUser il valore della colonna **ID** non è **1**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un amministratore di modelli &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md)   
 [Modificare l'account amministratore di sistema &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md)   
 [Creazione di un database di Master Data Services](install-windows/create-a-master-data-services-database.md)   
 [Notifiche &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)  
  
  
