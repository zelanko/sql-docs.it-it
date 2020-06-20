---
title: 'Proprietà avviso: nuovo avviso (pagina Opzioni) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: stevestein
ms.author: sstein
ms.openlocfilehash: b84c2472c56d50fa5c0595ea7046ed3ab9a2b352
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056595"
---
# <a name="alert-properties-new-alert-options-page"></a>Proprietà avviso: Nuovo avviso (pagina Opzioni)
  Utilizzare questa pagina per visualizzare e modificare le opzioni per gli [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avvisi di Agent.  
  
## <a name="options"></a>Opzioni  
 **Posta elettronica**  
 Consente di includere l'eventuale testo dell'errore risultante dall'evento nelle notifiche inviate tramite posta elettronica.  
  
 **Cercapersone**  
 Consente di includere l'eventuale testo dell'errore risultante dall'evento nelle notifiche inviate tramite cercapersone.  
  
 **NET SEND**  
 Consente di includere l'eventuale testo dell'errore risultante dall'evento nelle notifiche Net Send.  
  
 **Messaggio di notifica aggiuntivo da inviare**  
 Consente di digitare un testo aggiuntivo da includere nei messaggi di notifica.  
  
 **Intervallo tra le risposte**  
 Consente di specificare un ritardo per le occorrenze ripetute dell'evento. È possibile che alcuni eventi si verifichino frequentemente durante un breve periodo di tempo. In questo caso, è possibile che si desideri sapere che l'evento si è verificato ma che non si desideri ricevere una risposta per ogni evento. Usare questa opzione per specificare un timeout. Con un ritardo, dopo la risposta dell'avviso a un evento, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent attende il ritardo specificato prima di rispondere di nuovo, indipendentemente dal fatto che l'evento si verifichi durante il ritardo.  
  
 **Minuti**  
 Consente di specificare un ritardo in minuti. Per attivare una risposta ogni volta che si verifica l'evento, specificare 0 minuti e 0 secondi.  
  
 **Secondi**  
 Consente di specificare un ritardo in secondi. Per attivare una risposta ogni volta che si verifica l'evento, specificare 0 minuti e 0 secondi.  
  
## <a name="see-also"></a>Vedere anche  
 [Avvisi](alerts.md)  
  
  
