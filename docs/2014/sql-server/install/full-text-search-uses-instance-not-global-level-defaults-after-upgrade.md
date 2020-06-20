---
title: Con l'aggiornamento, la ricerca full-text utilizzerà i Word breaker e i filtri a livello di istanza, non globali, per impostazione predefinita | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 93ee8fcb-d11c-49fa-8fac-51ed31a8f008
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0b6cea7ab63351fad25f0205a614e364328171a9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036816"
---
# <a name="upgrading-will-cause-full-text-search-to-use-instance-level-not-global-word-breakers-and-filters-by-default"></a>A seguito dell'aggiornamento, per la ricerca full-text verranno utilizzati per impostazione predefinita word breaker e filtri a livello di istanza, non globali
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente la registrazione a livello di istanza per i nuovi word breaker e i nuovi filtri.  
  
## <a name="component"></a>Componente  
 Ricerca full-text  
  
## <a name="description"></a>Descrizione  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente la registrazione a livello di istanza per i nuovi word breaker e i nuovi filtri. La registrazione a livello di istanza garantisce un isolamento funzionale e la sicurezza delle istanze.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Dopo l'aggiornamento, utilizzare `sp_fulltext_service` per impostare la proprietà del servizio e `load_os_resources` che consente il caricamento dei componenti. È necessario eseguire quanto segue:  
  
 `sp_fulltext_service 'load_os_resources', 1`  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
