---
title: Server di pubblicazione non SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, non-SQL Server Publishers
- non-SQL Server Publishers
- heterogeneous data sources, non-SQL Server Publishers
- Publishers [SQL Server replication], Oracle
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 19db106c43007259754bace7f0e9d2938ad9cf1e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63022092"
---
# <a name="non-sql-server-publishers"></a>server di pubblicazione non SQL Server
  La pubblicazione di dati da[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] origini diverse consente di consolidare i dati [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]in. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente la sottoscrizione di dati snapshot o transazionali pubblicati da un database Oracle. Per altre informazioni sulla pubblicazione da sistemi Oracle, vedere [Panoramica della pubblicazione Oracle](oracle-publishing-overview.md).  
  
 La replica eterogenea a Sottoscrittori non SQL Server è deprecata. La pubblicazione Oracle è deprecata. Per spostare dati, creare soluzioni utilizzando Change Data Capture e [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 La pubblicazione da database non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è ideale nei seguenti scenari:  
  
|Scenario|Descrizione|  
|--------------|-----------------|  
|Distribuzioni di applicazioni[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Sviluppo con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , operando al contempo su dati replicati da un database non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Server di gestione temporanea di data warehousing|Mantenimento dei database di gestione temporanea di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sincronizzati con un database non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Migrazione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Verifica dell'applicazione in tempo reale a fronte di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] replicando al contempo le modifiche del sistema di origine. Quando il risultato della migrazione è soddisfacente, passare a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
  
## <a name="see-also"></a>Vedi anche  
 [Replica di database eterogenei](heterogeneous-database-replication.md)  
  
  
