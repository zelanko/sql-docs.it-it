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
manager: jroth
ms.openlocfilehash: 81d5627c46f12a033de5dab881f2c6de7f99e2f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66785329"
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
  
  
