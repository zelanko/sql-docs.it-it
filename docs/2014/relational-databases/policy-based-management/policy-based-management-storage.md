---
title: Archiviazione di gestione basata su criteri | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0e775d038c5bb4f7a467f2691e374296f1389d84
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066766"
---
# <a name="policy-based-management-storage"></a>Archiviazione di gestione basata su criteri
  I criteri vengono archiviati nel database msdb. In seguito alla modifica di criteri o di una condizione, è consigliabile eseguire il backup del database msdb. Per altre informazioni, vedere [Backup e ripristino di Database di sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="storing-policies"></a>Archiviazione di criteri  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] include criteri che consentono di monitorare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per impostazione predefinita, questi criteri non vengono installati nel, ma [!INCLUDE[ssDE](../../includes/ssde-md.md)] possono essere importati dal percorso di installazione predefinito C:\Program Files (x86) \Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033.  
  
 È possibile creare direttamente criteri utilizzando il menu **File/Nuovo** , quindi salvando i criteri in un file. In questo modo è possibile creare criteri quando non si è connessi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Una cronologia dei criteri valutati nell'istanza corrente del [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene gestita nelle tabelle di sistema msdb. Non viene mantenuta alcuna cronologia dei criteri applicati ad altre istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] o a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
  
