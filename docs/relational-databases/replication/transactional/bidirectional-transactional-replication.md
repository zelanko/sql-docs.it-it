---
title: Replica transazionale bidirezionale | Microsoft Docs
description: La replica transazionale bidirezionale consente lo scambio di modifiche tra due server. Ogni server pubblica i dati e sottoscrive una pubblicazione dall'altro server.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: f8a22b04834cc80b3b64cf7384bc6fe97d2f0571
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97406278"
---
# <a name="bidirectional-transactional-replication"></a>replica transazionale bidirezionale
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  La replica transazionale bidirezionale è una topologia di replica transazionale specifica che consente lo scambio reciproco di modifiche tra due server: ogni server pubblica i dati e successivamente esegue la sottoscrizione di una pubblicazione con gli stessi dati dell'altro server. Il parametro `@loopback_detection` di [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) è impostato su TRUE per garantire che le modifiche vengano inviate solo al Sottoscrittore e non restituite al server di pubblicazione.  
  
 In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive questa topologia è supportata inoltre dalla replica transazionale peer-to-peer, ma la replica bidirezionale consente di migliorare le prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
