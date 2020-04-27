---
title: Gli indici full-text nei database master, tempdb e modello non sono supportati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 743c7153b034cf5e1267c6a0da1e585845800980
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66095194"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>Gli indici full-text nei database master, tempdb e model non sono supportati
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente indici full-text in un database di sistema.  
  
## <a name="description"></a>Descrizione  
 In [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] gli indici full-text sono supportati nei database master, tempdb e model.  
  
 Eventuali cataloghi full-text nei database master, tempdb e modello vengono rimossi durante l'aggiornamento.  
  
## <a name="see-also"></a>Vedi anche  
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
