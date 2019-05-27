---
title: 'Procedura: Installare Upgrade Advisor | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0de86b9690f0647803938218ce566508662da20e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094914"
---
# <a name="how-to-install-upgrade-advisor"></a>Procedura: Installare Gestione spazio aggiornamenti
  Preparazione aggiornamento supporta l'analisi remota di tutti i componenti supportati, ad eccezione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se non si prevede di analizzare le istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è possibile installare Preparazione aggiornamento in qualsiasi computer in grado di connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e che soddisfi i prerequisiti di Preparazione aggiornamento. Se si prevede di analizzare le istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è necessario installare Preparazione aggiornamento nel server di report.  
  
 Per altre informazioni, vedere [installazione di preparazione aggiornamento](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
### <a name="to-install-upgrade-advisor"></a>Per installare Preparazione aggiornamento  
  
1.  Avviare l'installazione utilizzando uno dei metodi seguenti:  
  
    -   Se si installa dal [!INCLUDE[msCoName](../../includes/msconame-md.md)] sito Web, fare clic sui **scaricare** collegamento e quindi fare clic sui **eseguire** pulsante per avviare l'installazione.  
  
    -   Se si installa da supporto del prodotto, aprire il **redist** cartella, aprire il **Upgrade Advisor** cartella e quindi fare doppio clic **sqlua. msi**.  
  
    > [!NOTE]  
    >  Preparazione aggiornamento richiede [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4. Se non è installato, o se si dispone di una versione non definitiva, verrà visualizzato un messaggio di errore. Disinstallare qualsiasi versione precedente di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], quindi installare la versione più recente di .NET Framework 4.  
    >   
    >  Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom è un prerequisito per l'installazione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Preparazione aggiornamento e non viene installato dall'installazione di preparazione aggiornamento. Il programma di installazione è necessario scaricare e installare il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom dal [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack.  
  
2.  Nel **iniziale per il [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] installazione di preparazione aggiornamento** pagina, fare clic su **successivo**.  
  
3.  Nel **contratto di licenza** pagina, leggere il contratto di licenza. Se si accetta, selezionare **accettare il contratto di licenza** e quindi fare clic su **successivo**.  
  
4.  Nel **le informazioni di registrazione** pagina, immettere il nome e la società.  
  
5.  Nel **selezione delle caratteristiche** pagina, esaminare le **percorso di installazione** valore. Se necessario, usare il **esplorare** pulsante per modificare il percorso. Scegliere **Avanti**.  
  
6.  Nel **pronto per l'installazione del programma** pagina, fare clic su **installare** per installare Preparazione aggiornamento.  
  
7.  Scegliere **Fine** per uscire dalla procedura guidata.  
  
## <a name="see-also"></a>Vedere anche  
 [Prerequisiti di Preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
