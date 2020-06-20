---
title: Convalidare un'installazione di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8dd4e6ce7800c3a0a9db51f6c1a4bddfe7a188c3
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84931692"
---
# <a name="validate-a-sql-server-installation"></a>Convalidare un'installazione di SQL Server
  Il report sull'individuazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere utilizzato per verificare la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installate nel computer. Il ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] report sull'individuazione delle funzionalità installate** Visualizza un report di tutti i prodotti e le funzionalità di,,,, [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] installati nel server locale. Il report sull'individuazione delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile nella pagina **Strumenti** del Centro installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Per eseguire il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] report sull'individuazione delle funzionalità:**  
  
 Avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Centro installazione, facendo clic sul **pulsante Start** , scegliere tutti i **programmi** ** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<Version Name> **,, **strumenti di configurazione**e quindi fare clic su ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Centro installazione**. Per eseguire il report sull'individuazione delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], fare clic su **Strumenti** nell'area di navigazione a sinistra di **Centro installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** , quindi fare clic su **Report sull'individuazione delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installate**.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] report di individuazione viene salvato in% ProgramFiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\LOG \\<Ultima sessione di installazione \> .  
  
 Tale report può essere generato anche tramite la riga di comando. Eseguire "Setup.exe/Action = RunDiscovery" da un prompt dei comandi. Se si aggiunge "/q" alla riga di comando riportata in precedenza, non viene visualizzata alcuna interfaccia utente, ma il report verrà comunque creato in% programmi% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\LOG \\<Ultima sessione di installazione \> .  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e leggere i file di log del programma di installazione di SQL Server](view-and-read-sql-server-setup-log-files.md)  
  
  
