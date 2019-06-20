---
title: Gestire tutti gli avvisi dati in un sito di SharePoint con Gestione avvisi dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: 9c70b0f4-2db8-4c2e-acbf-96e2a55ddc48
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: debf7415a6364a358bb92066d53b840bcecd5930
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108336"
---
# <a name="manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager"></a>Gestire tutti gli avvisi dati in un sito di SharePoint
  Gli amministratori di avvisi di SharePoint possono visualizzare un elenco degli avvisi dati creati da qualsiasi utente del sito e le informazioni sugli avvisi. Gli amministratori di avvisi possono inoltre eliminare avvisi. Nella figura seguente sono illustrate le funzionalità disponibili per gli amministratori di avvisi in Gestione avvisi dati.  
  
 ![Gestione avvisi per gli amministratori del sito di SharePoint](media/rs-alertmanagersite.gif "Gestione avvisi per gli amministratori del sito di SharePoint")  
  
### <a name="to-view-a-list-of-alerts-created-by-a-site-user"></a>Per visualizzare un elenco di avvisi creati da un utente del sito  
  
1.  Passare al sito di SharePoint in cui sono state salvate le definizioni di avviso dati.  
  
2.  Nella home page fare clic su **Azioni sito**.  
  
3.  Scorrere verso la parte inferiore dell'elenco e fare clic su **Impostazioni sito**.  
  
4.  In **Reporting Services**fare clic su **Gestisci avvisi dati**.  
  
5.  Fare clic sulla freccia a discesa dall'elenco **Visualizza avvisi per l'utente** e selezionare l'utente di cui visualizzare gli avvisi.  
  
6.  Fare clic sulla freccia a discesa dell'elenco **Visualizza avvisi per il report** e selezionare un avviso specifico da visualizzare o fare clic su **Mostra tutto** per elencare tutti gli avvisi creati dall'utente selezionato.  
  
     In una tabella sono elencati il nome, il nome del report, il nome dell'utente che ha creato l'avviso dati, il numero di volte che l'avviso dati è stato inviato, l'ultima modifica della definizione di avviso dati e lo stato dell'avviso dati. Se l'avviso dati non può essere generato o inviato, nella colonna relativa allo stato sono incluse informazioni sull'errore che consentono di risolvere il problema.  
  
### <a name="to-delete-an-alert-definition"></a>Per eliminare una definizione di avviso  
  
-   Fare clic con il pulsante destro del mouse sull'avviso dati da eliminare e quindi fare clic su **Elimina**.  
  
    > [!NOTE]  
    >  Dopo avere eliminato l'avviso, non verranno inviati ulteriori messaggi di avviso. Se tuttavia si esegue una query sul database di avvisi, è possibile trovare ancora la definizione di avviso. Il servizio avvisi consente di eseguire la pulizia in base a una pianificazione e la definizione di avviso verrà eliminata definitivamente alla successiva operazione di pulizia. L'intervallo di pulizia predefinito è impostato su 20 minuti. Questo e altri intervalli di pulizia sono configurabili. Per altre informazioni, vedere [Avvisi dati di Reporting Services](../ssms/agent/alerts.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione avvisi dati per gli amministratori di avvisi](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md)   
 [Avvisi dati di Reporting Services](../ssms/agent/alerts.md)  
  
  
