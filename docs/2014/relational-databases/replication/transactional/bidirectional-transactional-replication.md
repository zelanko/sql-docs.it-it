---
title: Replica transazionale bidirezionale | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2cf5fbf215338b273be0924e6930906c8698aff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63188601"
---
# <a name="bidirectional-transactional-replication"></a>replica transazionale bidirezionale
  La replica transazionale bidirezionale è una topologia di replica transazionale specifica che consente lo scambio reciproco di modifiche tra due server: ogni server pubblica i dati e successivamente esegue la sottoscrizione di una pubblicazione con gli stessi dati dell'altro server. Il **@loopback_detection** parametro di [Sp_addsubscription &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) è impostato su true per garantire che le modifiche vengano inviate solo al Sottoscrittore e che non comportino l'invio della modifica al server di pubblicazione.  
  
 In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive questa topologia è supportata inoltre dalla replica transazionale peer-to-peer, ma la replica bidirezionale consente di migliorare le prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)  
  
  
