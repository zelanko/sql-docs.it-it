---
title: Certificati client sul sito Web del server di report (preparazione aggiornamento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 5ecce26b-99df-4109-8e51-d150d369dff7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 563a64e695ef552a712a5678f56d38fdfbff619f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059361"
---
# <a name="client-certificates-on-the-report-server-web-site-upgrade-advisor"></a>Certificati client sul sito Web del server di report (Upgrade Advisor)
  Sono stati rilevati uno o più certificati client sul sito Web IIS che ospita le directory virtuali del server di report o di Gestione report.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità nativa.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]non [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supporta l'utilizzo di certificati client per autenticare gli utenti. L'aggiornamento può continuare, ma i certificati client non verranno utilizzati dal server di report aggiornato.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Sarà necessario utilizzare una soluzione distinta, ad esempio ISA Server, per assicurarsi di rispettare i requisiti di autenticazione dei certificati client.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento Reporting Services &#40;preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
