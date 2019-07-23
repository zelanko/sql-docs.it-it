---
title: Archiviazione di gestione basata su criteri | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2f2be2bae147355557925bba1bd475ee9583447d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086919"
---
# <a name="policy-based-management-storage"></a>Archiviazione di gestione basata su criteri
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  I criteri vengono archiviati nel database msdb. In seguito alla modifica di criteri o di una condizione, è consigliabile eseguire il backup del database msdb. Per altre informazioni, vedere [Backup e ripristino di Database di sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="storing-policies"></a>Archiviazione di criteri  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] include criteri che consentono di monitorare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per impostazione predefinita, tali criteri non vengono installati in [!INCLUDE[ssDE](../../includes/ssde-md.md)], ma possono essere importati dal percorso di installazione predefinito C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Policies\DatabaseEngine\1033.  
  
 È possibile creare direttamente criteri utilizzando il menu **File/Nuovo** , quindi salvando i criteri in un file. In questo modo è possibile creare criteri quando non si è connessi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Una cronologia dei criteri valutati nell'istanza corrente del [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene gestita nelle tabelle di sistema msdb. Non viene mantenuta alcuna cronologia dei criteri applicati ad altre istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] o a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
  
