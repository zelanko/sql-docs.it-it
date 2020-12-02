---
description: Autorizzazioni server per il ruolo public
title: Autorizzazioni server per il ruolo public | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4abf2fd4068f19befd2896a27b9b214fee95dec0
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2020
ms.locfileid: "88482557"
---
# <a name="server-public-permissions"></a>Autorizzazioni server per il ruolo public
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Questa regola consente di determinare se il ruolo del server public dispone di autorizzazioni server. Ogni account di accesso creato nel server è un membro del ruolo del server public. Se questa condizione viene soddisfatta, ogni account di accesso nel server disporrà di autorizzazioni server.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Non concedere autorizzazioni server al ruolo del server public.  
  
> [!IMPORTANT]  
>  Una volta completata l'installazione, nel ruolo **PUBLIC** è disponibile l'autorizzazione **CONNECT** per tutti gli endpoint ad eccezione di **Connessione amministrativa dedicata**. Questa situazione è normale e, generalmente, non deve essere modificata (l'accesso viene controllato con l'autorizzazione **CONNECT SQL** che viene concessa automaticamente in caso di creazione di nuovi account di accesso).  
  
### <a name="for-more-information"></a>Per ulteriori informazioni  
 [Sicurezza di SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
  
