---
title: 'Lezione 1: Creazione di Windows account per la replica | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
- replication [SQL Server], administering
ms.assetid: 65c3816b-47f0-448c-a4a4-ebd3e2a58820
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: a1457a6d407b2b20c28e93c0ed681ab1dc8109d4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721165"
---
# <a name="lesson-1-creating-windows-accounts-for-replication"></a>Lezione 1: Creazione di Windows account per la replica
  In questa lezione verranno creati account di Windows per l'esecuzione degli agenti di replica. Verrà creato un account di Windows separato nel server locale per gli agenti seguenti:  
  
|Agent|Location|Nome account|  
|-----------|--------------|------------------|  
|agente snapshot|Server di pubblicazione|\<*nome_computer*>\repl_snapshot|  
|Agente di lettura log|Server di pubblicazione|\<*nome_computer*>\repl_logreader|  
|Agente di distribuzione|Server di pubblicazione e Sottoscrittore|\<*nome_computer*>\repl_distribution|  
|Agente di merge|Server di pubblicazione e Sottoscrittore|\<*nome_computer*>\repl_merge|  
  
> [!NOTE]  
>  Nelle esercitazioni sulla replica i server di pubblicazione e il server di distribuzione condividono la stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il server di pubblicazione e il Sottoscrittore possono utilizzare la stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ma ciò non è un requisito. Se il server di pubblicazione e il Sottoscrittore condividono la stessa istanza, i passaggi utilizzati per creare gli account del Sottoscrittore non sono obbligatori.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>Per creare account di Windows locali per gli agenti di replica nel server di pubblicazione  
  
1.  Nel server di pubblicazione fare clic su **Gestione computer** in **Strumenti di amministrazione** nel Pannello di controllo.  
  
2.  In **Utilità di sistema**espandere **Utenti e gruppi locali**.  
  
3.  Fare clic con il pulsante destro del mouse su **Utenti** e scegliere **Nuovo utente**.  
  
4.  Immettere `repl_snapshot` nella **nome utente** casella, specificare la password e altre informazioni rilevanti e quindi fare clic su **Create** per creare l'account repl_snapshot.  
  
5.  Ripetere il passaggio precedente per creare gli account repl_logreader, repl_distribution e repl_merge.  
  
6.  Scegliere **Chiudi**.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>Per creare account di Windows locali per gli agenti di replica nel Sottoscrittore  
  
1.  Nel Sottoscrittore fare clic su **Gestione computer** in **Strumenti di amministrazione** nel Pannello di controllo.  
  
2.  In **Utilità di sistema**espandere **Utenti e gruppi locali**.  
  
3.  Fare clic con il pulsante destro del mouse su **Utenti** e scegliere **Nuovo utente**.  
  
4.  Immettere `repl_distribution` nella **nome utente** casella, specificare la password e altre informazioni rilevanti e quindi fare clic su **Create** per creare l'account repl_distribution.  
  
5.  Ripetere il passaggio precedente per creare l'account repl_merge.  
  
6.  Scegliere **Chiudi**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 In questo modo sono stati creati gli account di Windows per gli agenti di replica. Il passaggio successivo consiste nella configurazione della cartella snapshot. Vedere [Lezione 2: Preparazione della cartella Snapshot](lesson-2-preparing-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica degli agenti di replica](agents/replication-agents-overview.md)  
  
  
