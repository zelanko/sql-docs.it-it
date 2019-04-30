---
title: 'Proprietà avviso: Nuovo avviso (pagina Opzioni) | Microsoft Docs'
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
manager: craigg
ms.openlocfilehash: 69f467af1c797b9bf1cfa55c7def8456ad4a32bd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061272"
---
# <a name="alert-properties-new-alert-options-page"></a>Proprietà avviso: Nuovo avviso (pagina Opzioni)
  Usare questa pagina per visualizzare e modificare opzioni per gli avvisi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
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
 [Avvisi](alerts.md)  
  
  
