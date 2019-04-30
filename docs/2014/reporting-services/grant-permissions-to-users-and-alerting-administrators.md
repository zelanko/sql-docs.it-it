---
title: Concedere autorizzazioni a utenti e amministratori di avvisi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 166808e1-ada7-48d2-bda8-8f7c017fb3aa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 44b0a20461df3214f605e68bbebb861cadf01849
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225305"
---
# <a name="grant-permissions-to-users-and-alerting-administrators"></a>Concedere autorizzazione a utenti e amministratori di avvisi
  Per poter creare, modificare, eliminare e visualizzare avvisi dati, è necessario che agli utenti e agli amministratori di avvisi vengano concesse le autorizzazioni di SharePoint. Non esistono autorizzazioni speciali da usare con la funzionalità relativa agli avvisi dati di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . È possibile usare le autorizzazioni predefinite di SharePoint.  
  
 **Information worker**: le autorizzazioni devono includere le autorizzazioni di SharePoint per la creazione di avvisi e la visualizzazione di elementi. I livelli di autorizzazione predefiniti di SharePoint denominati Progettazione, Collaborazione, Lettura e Solo visualizzazione includono le autorizzazioni di SharePoint relative alla creazione di avvisi e alla visualizzazione di elementi. È inoltre possibile creare un livello di autorizzazione personalizzato con le autorizzazioni necessarie per gli utenti che creano, modificano, eseguono e visualizzano avvisi dati.  
  
 **Amministratori di avvisi**: le autorizzazioni devono includere l'autorizzazione di SharePoint per la gestione degli avvisi. Per impostazione predefinita solamente il livello di autorizzazione Controllo completo include questa autorizzazione per i siti creati con il modello di sito del team. Se si utilizzano altri modelli di sito, vengono visualizzati elenchi diversi di gruppi di SharePoint predefiniti. È possibile aggiungere l'autorizzazione Gestione avvisi a uno dei livelli di autorizzazione predefiniti oppure creare un livello di autorizzazione personalizzato con l'autorizzazione necessaria per supportare gli amministratori di avvisi che visualizzano ed eliminano gli avvisi dati.  
  
 Per altre informazioni sulle autorizzazioni di SharePoint, vedere la pagina relativa alle [autorizzazioni utente e ai livelli di autorizzazione (SharePoint Server 2010)](https://technet.microsoft.com/library/cc721640.aspx).  
  
### <a name="to-grant-permissions"></a>Per concedere autorizzazioni  
  
1.  Accedere al sito di SharePoint in cui si desidera concedere autorizzazioni.  
  
2.  Nella barra degli strumenti, fare clic su **Azioni sito** , quindi su **Autorizzazioni sito**.  
  
     Se questa opzione non viene visualizzata, non si dispone del livello di autorizzazione sufficiente per concedere autorizzazioni ad altri.  
  
3.  Fare clic su **Concedi autorizzazioni**.  
  
4.  In **Utenti/Gruppi**digitare i nomi degli utenti, i nomi dei gruppi e gli indirizzi di posta elettronica a cui si vuole concedere autorizzazioni.  
  
5.  Selezionare l'opzione **Aggiungi utenti a un gruppo di SharePoint** o **Concedi direttamente le autorizzazioni agli utenti** . A seconda del fatto che sia stata selezionata l'opzione **Aggiungi utenti a un gruppo di SharePoint** o **Concedi direttamente le autorizzazioni agli utenti** , effettuare una delle operazioni seguenti:  
  
    -   Se è stata selezionata l'opzione **Aggiungi utenti a un gruppo di SharePoint**, selezionare un livello di autorizzazione nell'elenco a discesa.  
  
    -   Se è stato selezionato **Concedi direttamente le autorizzazioni agli utenti**, selezionare un livello di autorizzazione.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare autorizzazioni per gli elementi del server di report in un sito di SharePoint &#40;Reporting Services in modalità integrata SharePoint&#41;](security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Avvisi dati di Reporting Services](../ssms/agent/alerts.md)  
  
  
