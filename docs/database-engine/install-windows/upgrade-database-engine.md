---
title: Aggiornare il motore di database | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 029643d80f98f22e49e567bde8a2fb6e85073e50
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794751"
---
# <a name="upgrade-database-engine"></a>Aggiornare il motore di database

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  Gli articoli di questa sezione descrivono come eseguire l'aggiornamento del motore di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
1.  [Scegliere un metodo di aggiornamento del motore di database](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md) Prima di iniziare a eseguire un aggiornamento, è necessario comprendere i vari metodi di aggiornamento. Questo articolo descrive i metodi di aggiornamento e i passaggi previsti per ognuno.  
  
2.  [Pianificare e testare il piano di aggiornamento del motore di database](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md) Dopo aver esaminato i metodi di aggiornamento, si è pronti per sviluppare il metodo di aggiornamento appropriato per l'ambiente e per testarlo prima di aggiornare l'ambiente esistente. Questo articolo illustra lo sviluppo di un piano di aggiornamento e il relativo test.  
  
3.  [Completare l'aggiornamento al motore di database](../../database-engine/install-windows/complete-the-database-engine-upgrade.md) Dopo aver aggiornato i database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è necessario eseguire passaggi aggiuntivi, tra cui un nuovo backup, l'abilitazione di nuove funzionalità e il ripopolamento di cataloghi full-text. Questo articolo tratta tali passaggi.  
  
4.  [Modificare la modalità di compatibilità del database e usare l'archivio query](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md) Uno dei passaggi da eseguire dopo aver aggiornato [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] prevede l'abilitazione di nuove funzionalità modificando la modalità di compatibilità del database e usando quindi l'archivio query per monitorare le prestazioni. Questo articolo descrive il processo e propone un flusso di lavoro consigliato.  
  
5.  [Vantaggi delle nuove funzionalità di SQL Server](https://www.microsoft.com/sql-server/sql-server-2017) Infine, dopo aver completato i passaggi precedenti, si è pronti per sfruttare i vantaggi offerti dai nuovi miglioramenti specifici del motore di database. Questo articolo suggerisce alcuni di questi miglioramenti e fornisce collegamenti ad altre informazioni.  
  
  
