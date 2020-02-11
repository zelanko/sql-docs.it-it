---
title: 'Procedura: installazione di preparazione aggiornamento | Microsoft Docs'
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66094914"
---
# <a name="how-to-install-upgrade-advisor"></a>Procedura: Installazione di Preparazione aggiornamento
  Preparazione aggiornamento supporta l'analisi remota di tutti i componenti supportati, ad eccezione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se non si prevede di analizzare le istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è possibile installare Preparazione aggiornamento in qualsiasi computer in grado di connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e che soddisfi i prerequisiti di Preparazione aggiornamento. Se si prevede di analizzare le istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è necessario installare Preparazione aggiornamento nel server di report.  
  
 Per ulteriori informazioni, vedere [installazione di preparazione aggiornamento](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
### <a name="to-install-upgrade-advisor"></a>Per installare Preparazione aggiornamento  
  
1.  Avviare l'installazione utilizzando uno dei metodi seguenti:  
  
    -   Se si sta eseguendo l'installazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] dal sito Web, fare clic sul collegamento **download** , quindi fare clic sul pulsante **Esegui** per avviare l'installazione.  
  
    -   Se si sta eseguendo l'installazione dal supporto del prodotto, aprire la cartella **Redist** , aprire la cartella **Preparazione aggiornamento** , quindi fare doppio clic su **SQLUA. msi**.  
  
    > [!NOTE]  
    >  Preparazione aggiornamento richiede [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4. Se non è installato, o se si dispone di una versione non definitiva, verrà visualizzato un messaggio di errore. Disinstallare qualsiasi versione precedente di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], quindi installare la versione più recente di .NET Framework 4.  
    >   
    >  ScriptDom [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] è un prerequisito per l' [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] installazione di preparazione aggiornamento e non viene installato tramite l'installazione di preparazione aggiornamento. Per il programma di installazione è necessario scaricare e [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] installare ScriptDom dal [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack.  
  
2.  Nella pagina **installazione di preparazione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] aggiornamento** , fare clic su **Avanti**.  
  
3.  Nella pagina **contratto di licenza** leggere il contratto di licenza. Se si accettano le condizioni, selezionare Accetto **il contratto di licenza** e quindi fare clic su **Avanti**.  
  
4.  Nella pagina **informazioni di registrazione** immettere il nome e la società.  
  
5.  Nella pagina **Selezione funzionalità** esaminare il valore del **percorso di installazione** . Se necessario, utilizzare il pulsante **Sfoglia** per modificare il percorso. Fare clic su **Avanti**.  
  
6.  Nella pagina **pronto per l'installazione del programma** fare clic su **Installa** per installare Upgrade Advisor.  
  
7.  Fare clic su **Fine** per uscire dalla procedura guidata.  
  
## <a name="see-also"></a>Vedere anche  
 [Prerequisiti di Preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
