---
title: Convalidare un'installazione di SQL Server | Microsoft Docs
description: Per verificare la versione e le funzionalità di SQL Server installate nel computer, è possibile usare il report di individuazione di SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: fde701b41060b59d08be9ced38687385a6b3a995
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130801"
---
# <a name="validate-a-sql-server-installation"></a>Convalidare un'installazione di SQL Server

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
  Il report sull'individuazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere utilizzato per verificare la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installate nel computer. Nel **Report sull'individuazione delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installate** viene visualizzato un report di tutte le funzionalità e di tutti i prodotti di [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e [!INCLUDE[ssSQL15](../../includes/sssqlv14-md.md)] installati nel server locale. Il report sull'individuazione delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile nella pagina **Strumenti** del Centro installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 ## <a name="run-ssnoversion-features-discovery-report"></a>Per eseguire il report sull'individuazione delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Avviare Centro installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] facendo clic sul pulsante **Start**, scegliendo **Tutti i programmi**, quindi **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<Version Name>** , **Strumenti di configurazione** e infine **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Centro installazione**. Per eseguire il report sull'individuazione delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], fare clic su **Strumenti** nell'area di navigazione a sinistra di **Centro installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** , quindi fare clic su **Report sull'individuazione delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installate**.  
  
 Il report sull'individuazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene salvato in %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<ultima sessione di installazione\>.  
  
 Tale report può essere generato anche tramite la riga di comando. Eseguire "Setup.exe /Action=RunDiscovery" al prompt dei comandi. Se si aggiunge "/q" alla riga di comando qui sopra, non viene visualizzata alcuna interfaccia utente, ma il report viene comunque creato in %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<ultima sessione di installazione\>.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
