---
title: Sospendere l'elaborazione di sottoscrizioni e Report | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1607637630c507588602dd7e566917ce1eeb6080
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100919"
---
# <a name="pause-report-and-subscription-processing"></a>Sospendere l'elaborazione del report e della sottoscrizione
  Non è possibile sospendere direttamente un report o una sottoscrizione, tuttavia è possibile interromperne l'elaborazione prima dell'avvio del processo o quando viene stabilita una connessione all'origine dei dati. È inoltre possibile impedire l'elaborazione di una sottoscrizione o di un report rendendolo inaccessibile agli utenti.  
  
 Per impedire temporaneamente un'elaborazione, utilizzare le strategie seguenti.  
  
## <a name="modify-role-assignments-to-prevent-access"></a>Modifica delle assegnazioni di ruolo per impedire l'accesso  
 Il modo migliore per rendere non disponibile un report consiste nel rimuovere temporaneamente l'assegnazione di ruolo che consente l'accesso al report. Questa strategia può essere utilizzata con tutti i report, indipendentemente dalla modalità di connessione all'origine dei dati. L'operazione ha effetto solo sul report in questione, non su altri report o elementi.  
  
 Per rimuovere l'assegnazione di ruolo, aprire la pagina delle proprietà sicurezza del report in Gestione report. Se il report eredita la sicurezza da un elemento padre, è possibile fare clic su **Modifica sicurezza elemento** per creare criteri di sicurezza restrittivi privi di assegnazioni di ruolo che consentono l'accesso a numerosi utenti. È possibile, ad esempio, rimuovere un'assegnazione di ruolo che consente l'accesso al gruppo Everyone e mantenere l'assegnazione di ruolo che consente l'accesso a un gruppo ristretto di utenti, ad esempio Administrators.  
  
## <a name="disable-a-shared-data-source"></a>Disabilitazione di un'origine dei dati condivisa  
 Uno dei vantaggi dell'utilizzo di origini dei dati condivise è rappresentato dalla possibilità di disabilitarle per impedire l'esecuzione di un report o di una sottoscrizione guidata dai dati. Quando si disabilita un'origine dei dati condivisa, il report viene disconnesso dalla relativa origine dei dati esterna. Dopo la disabilitazione l'origine dei dati non sarà più disponibile per tutti i report e le sottoscrizioni che la utilizzano. Per disabilitare un'origine dati condivisa, aprire l'origine dati in Gestione Report e deselezionare il **abilita questa origine dati** casella di controllo.  
  
 Si noti che il report viene caricato anche se la relativa origine dei dati non è disponibile. Il report non conterrà dati, ma gli utenti con le autorizzazioni appropriate potranno accedere alle pagine delle proprietà, alle impostazioni di sicurezza, alla cronologia e alle informazioni di sottoscrizione associate al report.  
  
## <a name="pause-a-shared-schedule"></a>Sospensione di una pianificazione condivisa  
 Se una sottoscrizione o un report viene eseguito in base a una pianificazione condivisa, è possibile sospendere la pianificazione per impedire l'elaborazione del report o della sottoscrizione. Tutte le operazioni di elaborazione del report o della sottoscrizione eseguite in base alla pianificazione verranno posticipate fino a quando verrà ripresa la pianificazione. Per altre informazioni, vedere [sospendere e riprendere le pianificazioni condivise](schedules.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Server di report di Reporting Services &#40;modalità nativa&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Pagina delle proprietà sicurezza, Elementi&#40;Gestione report&#41;](../security-properties-page-items-report-manager.md)  
  
  
