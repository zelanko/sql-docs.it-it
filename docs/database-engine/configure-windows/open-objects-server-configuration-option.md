---
title: Opzione di configurazione del server open objects | Microsoft Docs
description: Informazioni sull'opzione di configurazione disabilitata "open objects." Scoprire come SQL Server gestisce ora il numero di oggetti di database aperti.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- open objects option
ms.assetid: c8424d3c-86ba-4cc5-bf0c-be4ce44bdd04
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0bbcb11a80f06eae10e5481c965e9216cc84695e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773621"
---
# <a name="open-objects-server-configuration-option"></a>Opzione di configurazione del server open objects
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Questa opzione è ancora presente in **sp_configure**, anche se in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la relativa funzionalità è stata disabilitata. L'impostazione non ha alcun effetto. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il numero degli oggetti di database aperti viene gestito in modo dinamico ed è limitato soltanto dalla memoria disponibile. L'opzione **open objects** è stata mantenuta in **sp_configure** per garantire la compatibilità con le versioni precedenti per gli script esistenti.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
