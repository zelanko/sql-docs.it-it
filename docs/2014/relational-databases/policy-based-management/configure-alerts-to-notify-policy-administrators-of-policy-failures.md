---
title: Configurare avvisi per notificare agli amministratori eventuali errori dei criteri| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, configure alerts
ms.assetid: e8e60159-d5b0-49d5-91f3-af8e9cb994c1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 57eb4f021a25fa2fa559fa7ff21d12bb621cc53a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63126906"
---
# <a name="configure-alerts-to-notify-policy-administrators-of-policy-failures"></a>Configurare avvisi per notificare agli amministratori eventuali errori dei criteri
  Se si verifica una violazione quando i criteri di gestione basata su criteri vengono eseguiti in una delle tre modalità di valutazione automatiche, viene scritto un messaggio nel registro eventi. Per ricevere una notifica relativa all'avvenuta scrittura del messaggio nel registro eventi, è possibile creare un avviso per rilevare il messaggio ed eseguire un'azione. L'avviso dovrà rilevare i messaggi come indicato nella tabella seguente.  
  
|Modalità di esecuzione|Numero di messaggio|  
|--------------------|--------------------|  
|Su modifica: impedisci esecuzione<br /><br /> (se automatica)|34050|  
|Su modifica: impedisci esecuzione<br /><br /> (se Su richiesta)|34051|  
|Su pianificazione|34052|  
|Su modifica|34053|  
  
 Per configurare un avviso per rispondere ai messaggi di errore relativi alla gestione basata su criteri, vedere gli argomenti seguenti:  
  
-   [Create an Operator](../../ssms/agent/create-an-operator.md)  
  
-   [Creazione di un avviso utilizzando un numero di errore](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Assegnazione di avvisi a un operatore](../../ssms/agent/assign-alerts-to-an-operator.md)  
  
## <a name="permissions"></a>Autorizzazioni  
 Quando i criteri vengono valutati su richiesta, vengono eseguiti nel contesto di sicurezza dell'utente. Per poter scrivere nel log degli errori, l'utente deve disporre di autorizzazioni ALTER TRACE o deve essere un membro del ruolo predefinito del server sysadmin. I criteri valutati da un utente che dispone di privilegi di livello inferiore non verranno scritti nel registro eventi e non genereranno un avviso.  
  
 Le modalità di esecuzione automatiche possono essere eseguite solo da membri del ruolo sysadmin. Tale ruolo consente la scrittura dei criteri nel log degli errori e la generazione di un avviso.  
  
## <a name="additional-considerations-about-alerts"></a>Considerazioni aggiuntive sugli avvisi  
 Tenere presente le considerazioni aggiuntive seguenti relative agli avvisi:  
  
-   Gli avvisi vengono generati solo per i criteri abilitati. Poiché i criteri **Su richiesta** non possono essere abilitati, non vengono generati avvisi per i criteri eseguiti su richiesta.  
  
-   Se l'azione che si desidera eseguire include l'invio di un messaggio di posta elettronica, è necessario configurare un account di posta elettronica. È consigliabile utilizzare Posta elettronica database. Per altre informazioni su come configurare Posta elettronica database, vedere [Creare un account di Posta elettronica database](../database-mail/create-a-database-mail-account.md).  
  
  
