---
title: Autorizzazioni server per il ruolo public | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6f240973def97dea739c21381f38dc366deb8920
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691477"
---
# <a name="server-public-permissions"></a>Autorizzazioni server per il ruolo public
  Questa regola consente di determinare se il ruolo del server public dispone di autorizzazioni server. Ogni account di accesso creato nel server è un membro del ruolo del server public. Se questa condizione viene soddisfatta, ogni account di accesso nel server disporrà di autorizzazioni server.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Non concedere autorizzazioni server al ruolo del server public.  
  
> [!IMPORTANT]  
>  Al termine dell'installazione il **pubblici** ruolo ha `CONNECT` l'autorizzazione per tutti gli endpoint ad eccezione di **Dedicated Admin Connection**. Questa situazione è normale e, generalmente, non deve essere modificata (l'accesso viene controllato tramite l'autorizzazione `CONNECT SQL` che viene concessa automaticamente in caso di creazione di nuovi account di accesso).  
  
### <a name="for-more-information"></a>Per ulteriori informazioni  
 [Sicurezza di SQL Server](../security/securing-sql-server.md)  
  
  
