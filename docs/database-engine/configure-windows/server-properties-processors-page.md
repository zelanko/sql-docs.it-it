---
title: Proprietà server (pagina Processori) | Microsoft Docs
description: Acquisire familiarità con le impostazioni del processore in SQL Server. Informazioni sulle opzioni che controllano il numero di thread di lavoro, l'assegnazione del processore e altre proprietà.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.processor.f1
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a3652ee3b01383d8d029bb0eb7aeefaa4f8cc045
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726603"
---
# <a name="server-properties---processors-page"></a>Proprietà server (pagina Processori)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Utilizzare questa pagina per visualizzare o modificare le opzioni del processore. Le impostazioni Affinità processori sono abilitate solo se sono installati più processori.  
  
## <a name="options"></a>Opzioni  
 **Affinità processori**  
 Consente di assegnare i processori a thread specifici, in modo da eliminare i ricaricamenti dei processori e ridurre la migrazione dei thread tra i processori. Per altre informazioni, vedere [Opzione di configurazione del server affinity mask](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md).  
  
 **Affinità I/O**  
 Associa l'I/O su disco di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un determinato subset di CPU. Per altre informazioni, vedere [Opzione di configurazione del server affinity I/O mask](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md).  
  
 **Imposta automaticamente maschera di affinità processori per tutti i processori**  
 Consente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di impostare l'affinità processori.  
  
 **Imposta automaticamente maschera di affinità di I/O per tutti i processori**  
 Consente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di impostare l'affinità di I/O.  
  
 **Numero massimo thread di lavoro**  
 Il valore 0 consente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di impostare dinamicamente il numero di thread di lavoro. Si tratta dell'impostazione ottimale per la maggior parte dei sistemi. A seconda della configurazione di sistema, è tuttavia possibile che l'impostazione di questa opzione su un valore specifico migliori le prestazioni. Per altre informazioni, vedere [Configurare l'opzione di configurazione del server max worker threads](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md).  
  
 **Aumenta priorità di SQL Server**  
 Consente di specificare se eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una priorità di pianificazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows maggiore rispetto agli altri processi in esecuzione nello stesso computer. Per altre informazioni, vedere [Configurare l'opzione di configurazione del server priority boost](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md).  
  
 **Usa fiber Windows (lightweight pooling)**  
 Consente di utilizzare i fiber Windows anziché i thread per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si noti che l'opzione è disponibile solo in Windows 2003 Server Edition. Per altre informazioni, vedere [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
 **Valori configurati**  
 Consente di visualizzare i valori configurati per le opzioni nel riquadro. Se si modificano i valori, fare clic su **Valori correnti** per verificare se le modifiche sono diventate effettive. In caso contrario, l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere prima riavviata.  
  
 **Valori correnti**  
 Consente di visualizzare i valori correnti per le opzioni contenute nel riquadro. I valori sono di sola lettura.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
