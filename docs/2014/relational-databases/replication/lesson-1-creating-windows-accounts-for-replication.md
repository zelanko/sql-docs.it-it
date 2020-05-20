---
title: 'Lezione 1: Creazione di account di Windows per la replica | Microsoft Docs'
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f11321b20c4238fdf9b3376d79edcb12c0e9204b
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000471"
---
# <a name="lesson-1-creating-windows-accounts-for-replication"></a>Lezione 1: Creazione di account di Windows per la replica
  In questa lezione verranno creati account di Windows per l'esecuzione degli agenti di replica. Verrà creato un account di Windows separato nel server locale per gli agenti seguenti:  
  
|Agente|Location|Nome account|  
|-----------|--------------|------------------|  
|agente snapshot|Publisher|\<*nome_computer*>\repl_snapshot|  
|Agente di lettura log|Publisher|\<*nome_computer*>\repl_logreader|  
|Agente di distribuzione|Server di pubblicazione e Sottoscrittore|\<*nome_computer*>\repl_distribution|  
|Agente di merge|Server di pubblicazione e Sottoscrittore|\<*nome_computer*>\repl_merge|  
  
> [!NOTE]  
>  Nelle esercitazioni sulla replica i server di pubblicazione e il server di distribuzione condividono la stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il server di pubblicazione e il Sottoscrittore possono utilizzare la stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ma ciò non è un requisito. Se il server di pubblicazione e il Sottoscrittore condividono la stessa istanza, i passaggi utilizzati per creare gli account del Sottoscrittore non sono obbligatori.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>Per creare account di Windows locali per gli agenti di replica nel server di pubblicazione  
  
1.  Nel server di pubblicazione aprire **Gestione computer** da **strumenti di amministrazione** nel pannello di controllo.  
  
2.  In **Utilità di sistema**espandere **Utenti e gruppi locali**.  
  
3.  Fare clic con il pulsante destro del mouse su **utenti** e quindi scegliere **nuovo utente**.  
  
4.  Immettere `repl_snapshot` nella casella **nome utente** , specificare la password e altre informazioni rilevanti, quindi fare clic su **Crea** per creare l'account repl_snapshot.  
  
5.  Ripetere il passaggio precedente per creare gli account repl_logreader, repl_distribution e repl_merge.  
  
6.  Fare clic su **Chiudi**.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>Per creare account di Windows locali per gli agenti di replica nel Sottoscrittore  
  
1.  Nel Sottoscrittore aprire **Gestione computer** da **strumenti di amministrazione** nel pannello di controllo.  
  
2.  In **Utilità di sistema**espandere **Utenti e gruppi locali**.  
  
3.  Fare clic con il pulsante destro del mouse su **utenti** e quindi scegliere **nuovo utente**.  
  
4.  Immettere `repl_distribution` nella casella **nome utente** , specificare la password e altre informazioni rilevanti, quindi fare clic su **Crea** per creare l'account repl_distribution.  
  
5.  Ripetere il passaggio precedente per creare l'account repl_merge.  
  
6.  Fare clic su **Chiudi**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 In questo modo sono stati creati gli account di Windows per gli agenti di replica. Il passaggio successivo consiste nella configurazione della cartella snapshot. Vedere [Lezione 2: Preparazione della cartella snapshot](lesson-2-preparing-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica degli agenti di replica](agents/replication-agents-overview.md)  
  
  
