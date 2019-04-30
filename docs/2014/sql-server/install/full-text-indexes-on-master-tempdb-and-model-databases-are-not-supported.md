---
title: Non sono supportati gli indici full-text nei database master, tempdb e model | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f055640dbdbf4ece491b2d8552c1581b122faed3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240632"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>Gli indici full-text nei database master, tempdb e model non sono supportati
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente indici full-text in un database di sistema.  
  
## <a name="description"></a>Descrizione  
 In [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] gli indici full-text sono supportati nei database master, tempdb e model.  
  
 Cataloghi full-text nel master, tempdb e modello di database vengono rimossi durante l'aggiornamento.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
