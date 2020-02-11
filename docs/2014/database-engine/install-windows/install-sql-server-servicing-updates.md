---
title: Installare gli aggiornamenti di manutenzione di SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07f438f86a22b866351a0b83ee7634338f3ad2cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62775344"
---
# <a name="install-sql-server-2014-servicing-updates"></a>Installare gli aggiornamenti dei servizi di SQL Server 2014
  In questo argomento vengono fornite informazioni sull'installazione degli aggiornamenti per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. In questa sezione vengono fornite informazioni sui seguenti argomenti:  
  
-   Installazione di aggiornamenti per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante una nuova installazione  
  
-   Installazione di aggiornamenti per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dopo che è stato installato.  
  
 Si consiglia agli clienti di valutare e installare tempestivamente gli ultimi aggiornamenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per assicurarsi che i sistemi dispongano degli aggiornamenti di sicurezza più recenti.  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-during-a-new-installation"></a>Installazione di aggiornamenti per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante una nuova installazione  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Il programma di installazione integra gli aggiornamenti più recenti del pacchetto con l'installazione del prodotto principale in modo che quest'ultimo e i relativi aggiornamenti applicabili vengano installati contemporaneamente. Aggiornamento prodotto consente la ricerca degli aggiornamenti applicabili da:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
-   Windows Server Update Services (WSUS)  
  
-   Cartella locale  
  
-   Condivisione di rete  
  
 Dopo avere individuato le versioni più recenti degli aggiornamenti applicabili, questi vengono scaricati e integrati dal programma di installazione con il processo di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrente. Tramite l'aggiornamento del prodotto è possibile includere un aggiornamento cumulativo, un Service Pack o un Service Pack con aggiornamento cumulativo. La funzionalità di aggiornamento del prodotto è un'estensione della [funzionalità](https://go.microsoft.com/fwlink/?LinkId=219945) di integrazione disponibile [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] in PCU1.  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-after-it-has-already-been-installed"></a>Installazione di aggiornamenti per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dopo che è stato installato  
 In un'istanza installata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]si consiglia di applicare tutti gli aggiornamenti disponibili, ovvero le versioni di distribuzione generale (GDR-Security/Critical Update), i Service Pack (SP) e l'ultimo aggiornamento cumulativo disponibile (Cu).  
  
 A seconda del tipo di versione del servizio, SQL Server aggiornamenti sono disponibili tramite Microsoft Update (MU), l'area download Microsoft e/o il server hotfix del servizio supporto tecnico clienti. Gli aggiornamenti della sicurezza e critici per SQL Server vengono forniti automaticamente da Microsoft Update (per poter visualizzare questi aggiornamenti, è necessario acconsentire esplicitamente a MU tramite Windows Update nel pannello di controllo). I Service Pack sono disponibili in MU come download facoltativi/importanti, oltre che nell'area download. Gli aggiornamenti cumulativi sono disponibili nel server di download degli hotfix Microsoft fornito negli articoli della Knowledge base.  
  
## <a name="see-also"></a>Vedere anche  
 [Installare SQL Server 2014 dall'installazione guidata &#40;&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 L' [installazione di aggiornamenti dal prompt dei comandi](installing-updates-from-the-command-prompt.md) [consente di aggiungere funzionalità a un'istanza di SQL Server 2014 &#40;di installazione&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [Rimuovere un'installazione di SQL Server 2014](repair-a-failed-sql-server-installation.md)  
  
  
