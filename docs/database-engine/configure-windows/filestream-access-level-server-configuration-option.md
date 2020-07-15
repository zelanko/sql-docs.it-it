---
title: Opzione di configurazione del server filestream access level | Microsoft Docs
description: Acquisire familiarità con l'opzione "filestream_access_level". Scoprire come viene modificato il livello di accesso di FILESTREAM per un'istanza di SQL Server.
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b891ba283acb1176a60bcc64105e126192aa8225
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772459"
---
# <a name="filestream-access-level-server-configuration-option"></a>Opzione di configurazione del server filestream access level
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
  
  
