---
title: Replica su Internet | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Web publishing [SQL Server replication], about Web publishing
- Web publishing [SQL Server replication]
- Internet [SQL Server replication]
- Internet [SQL Server replication], publishing
ms.assetid: 04e7f4ed-e244-4bbe-ba12-09c33abea09e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: d7dd25b2b1cd2aa0cc8560072702bc8188191d09
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287388"
---
# <a name="replication-over-the-internet"></a>Replica su Internet
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  La replica dei dati su Internet consente a utenti remoti e non connessi di accedere ai dati nel momento desiderato tramite una connessione a Internet. È possibile replicare i dati su Internet utilizzando:  
  
-   Una rete privata virtuale (VPN). Per altre informazioni, vedere [Pubblicare i dati su Internet tramite VPN](../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md).  
  
-   L'opzione di sincronizzazione Web per la replica di tipo merge. Per altre informazioni, vedere [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Tutti i tipi di replica di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono replicare i dati in una VPN, ma è consigliabile considerare la sincronizzazione Web se si usa la replica di tipo merge.  
  
  
