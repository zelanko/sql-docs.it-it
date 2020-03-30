---
title: Opzione di configurazione del server filestream access level | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8335f821e2bd4026c17b0054e047125a0afd0177
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68011699"
---
# <a name="filestream-access-level-server-configuration-option"></a>Opzione di configurazione del server filestream access level
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Utilizzare l'opzione filestream_access_level per modificare il livello di accesso di FILESTREAM per l'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Prima che questa opzione abbia effetto, è necessario abilitare le impostazioni dell'amministrazione di Windows per FILESTREAM. È possibile abilitare queste impostazioni durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|valore|Definizione|  
|-----------|----------------|  
|0|Disabilita il supporto di FILESTREAM per l'istanza corrente.|  
|1|Abilita FILESTREAM per l'accesso [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|2|Abilita l'accesso tramite flusso [!INCLUDE[tsql](../../includes/tsql-md.md)] e Win32 per FILESTREAM.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione del Motore di database - Filestream](https://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)   
 [Abilitare e configurare FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
