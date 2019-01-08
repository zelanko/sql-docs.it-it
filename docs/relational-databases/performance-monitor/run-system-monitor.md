---
title: Eseguire Monitoraggio di sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], running
- Windows System Monitor [SQL Server], running
- remote procedure calls [SQL Server]
- starting Windows NT System Monitor
- RPC
ms.assetid: 05297984-bc8d-43df-829c-032387f7ea61
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 67652dd6931f1961bbfc9f19b19a5044816edcc3
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53379732"
---
# <a name="run-system-monitor"></a>Eseguire Monitoraggio di sistema
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Monitoraggio di sistema utilizza chiamate di procedura remota (RPC, Remote Procedure Call) per raccogliere informazioni da Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Qualunque utente che dispone di autorizzazioni di Microsoft Windows per l'esecuzione di Monitoraggio di sistema può utilizzare tale programma per monitorare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se si utilizza Monitoraggio di sistema o Performance Monitor, non sarà possibile connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguita in Microsoft Windows 98.  
  
 Analogamente a tutti gli strumenti di monitoraggio delle prestazioni, Monitoraggio di sistema determina un peggioramento delle prestazioni del sistema durante il monitoraggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'overhead effettivo di un'istanza specifica varia a seconda della piattaforma hardware, del numero di contatori e dell'intervallo di aggiornamento selezionato. L'integrazione di Monitoraggio di sistema con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stata tuttavia progettata in modo da ridurre al minimo eventuali peggioramenti delle prestazioni.  
  
> [!NOTE]  
>  Se sono stati selezionati contatori delle prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da monitorare nello snap-in di Monitoraggio di sistema, tali contatori verranno visualizzati anche se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in esecuzione.  
  
 Per informazioni sull'avvio di Monitoraggio di sistema, vedere [Avvio di Monitoraggio di sistema &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md).  
  
  
