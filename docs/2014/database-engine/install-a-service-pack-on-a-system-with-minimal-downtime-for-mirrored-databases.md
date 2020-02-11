---
title: Installare un Service Pack in un sistema con tempi di inattività minimi per i database con mirroring | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- hotfixes [SQL Server]
- database mirroring [SQL Server], upgrading system
- rolling upgrades [SQL Server]
- service packs [SQL Server]
- upgrading mirrored database systems
- upgrading SQL Server, mirrored databases
ms.assetid: bdc63142-027d-4ead-9d3e-147331387ef5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 821fd05e94ac820dff50bd08c70c75e7e9cc653d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779595"
---
# <a name="install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases"></a>Installare un Service Pack in un sistema con tempi di inattività minimi per database con mirroring
  In questo argomento viene descritta la procedura per ridurre al minimo il tempo di inattività per i database con mirroring quando vengono installati Service Pack e hotfix. Questo processo comprende l'aggiornamento sequenziale delle istanze di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] che partecipano al mirroring del database. Questa forma di aggiornamento, nota come *aggiornamento in sequenza*, riduce il tempo di inattività a un singolo failover. Per le sessioni in modalità a prestazioni elevate nelle quali il server mirror è geograficamente distante dal server principale, un aggiornamento in sequenza potrebbe non essere appropriato.  
  
 Un aggiornamento in sequenza è un processo a più stadi articolato nelle fasi seguenti:  
  
-   Protezione dei dati.  
  
-   Se la sessione include un server di controllo del mirroring, si consiglia di rimuoverlo. In caso contrario, quando l'istanza del server mirror viene aggiornata, la disponibilità del database dipende dal server di controllo del mirroring che rimane connesso all'istanza del server principale. Dopo avere rimosso un server di controllo del mirroring, è possibile aggiornarlo in qualsiasi momento durante il processo di aggiornamento in sequenza senza rischiare alcun tempo di inattività del database.  
  
    > [!NOTE]  
    >  Per altre informazioni, vedere [Quorum: Impatto di un server di controllo del mirroring sulla disponibilità del database &#40;mirroring del database&#41;](database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
-   Se una sessione è in esecuzione in modalità a prestazioni elevate, impostare la modalità operativa su modalità a protezione elevata.  
  
-   Aggiornare ciascuna istanza del server interessata dal mirroring del database. Un aggiornamento in sequenza prevede l'aggiornamento dell'istanza del server che è attualmente il server mirror, l'esecuzione manuale del failover di ciascuno dei database con mirroring e l'aggiornamento dell'istanza che era il primo server principale (e che ora è il nuovo server mirror). A questo punto, è necessario riprendere il mirroring.  
  
    > [!NOTE]  
    >  Prima di avviare un aggiornamento in sequenza, è consigliabile eseguire un failover manuale di prova su almeno una delle sessioni di mirroring.  
  
-   Ripristinare la modalità a elevate prestazioni, se richiesto.  
  
-   Fare tornare il server di controllo del mirroring nella sessione di mirroring, se richiesto.  
  
 Le procedure per queste fasi sono descritte di seguito.  
  
> [!IMPORTANT]  
>  Un'istanza del server potrebbe ricoprire ruoli di mirroring diversi (server principale, server mirror o server di controllo del mirroring) in sessioni di mirroring simultanee. In questo caso, è necessario adattare di conseguenza il processo di aggiornamento in sequenza di base.  
  
### <a name="to-protect-your-data-before-an-update-a-best-practice"></a>Per proteggere i dati prima di un aggiornamento (procedura consigliata)  
  
1.  Eseguire un backup completo di ciascun database principale.  
  
     **Per eseguire il backup di un database**  
  
    -   [Creare un backup completo del Database &#40;SQL Server&#41;](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
2.  Eseguire il comando [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) in ogni database principale.  
  
### <a name="to-remove-a-witness-from-a-session"></a>Per rimuovere un server di controllo del mirroring da una sessione  
  
1.  Se una sessione di mirroring prevede un server di controllo del mirroring, si consiglia di rimuoverlo prima di eseguire un aggiornamento in sequenza.  
  
     **Per rimuovere il server di controllo del mirroring**  
  
    -   [Rimuovere il server di controllo del mirroring da una sessione di mirroring del database &#40;SQL Server&#41;](database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
### <a name="to-change-a-session-from-high-performance-mode-to-high-safety-mode"></a>Per modificare la modalità di una sessione dalla modalità a elevate prestazioni alla modalità a protezione elevata  
  
1.  Se una sessione di mirroring viene eseguita in modalità a elevate prestazioni, prima di eseguire un aggiornamento in sequenza impostare la modalità operativa su protezione elevata senza failover automatico. Utilizzare uno dei seguenti metodi:  
  
    -   In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]: modificare l'opzione **Modalità operativa** e impostarla su **Protezione elevata senza failover automatico (sincrona)** usando la [pagina Mirroring](../relational-databases/databases/database-properties-mirroring-page.md) della finestra di dialogo **Proprietà database**. Per informazioni su come accedere a questa pagina, vedere [Avvio della Configurazione guidata sicurezza mirroring del database &#40;SQL Server Management Studio&#41;](database-mirroring/start-the-configuring-database-mirroring-security-wizard.md).  
  
    -   In [!INCLUDE[tsql](../includes/tsql-md.md)]: impostare la sicurezza della transazione su FULL. Per altre informazioni, vedere [Modifica della protezione delle transazioni in una sessione di mirroring del database &#40;SQL Server&#41;](database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md).  
  
### <a name="to-perform-the-rolling-update"></a>Per eseguire l'aggiornamento in sequenza  
  
1.  Per ridurre al minimo i tempi di inattività, è consigliabile attenersi alla seguente procedura: avviare l'aggiornamento in sequenza aggiornando qualsiasi server partner di mirroring che è attualmente il server mirror in tutte le relative sessioni di mirroring. In questa fase potrebbe essere necessario aggiornare più istanze del server.  
  
    > [!NOTE]  
    >  Un server di controllo del mirroring può essere aggiornato in qualsiasi punto del processo di aggiornamento in sequenza. Ad esempio, se un'istanza del server è un server mirror nella sessione 1 e un server di controllo del mirroring nella sessione 2, è possibile aggiornare l'istanza del server.  
  
     L'istanza del server da aggiornare per prima dipende dalla configurazione corrente delle sessioni di mirroring, ovvero:  
  
    -   Se un'istanza del server si trova già nel server mirror in tutte le sue sessioni di mirroring, installare il Service Pack o l'hotfix in quell'istanza del server.  
  
    -   Se tutte le istanze del server sono attualmente il server principale in tutte le sessioni di mirroring, selezionare un'istanza del server da aggiornare per prima. Eseguire il failover manuale di ciascun database principale e aggiornare l'istanza del server installando il Service Pack o l'hotfix.  
  
     Dopo aver eseguito l'aggiornamento, un'istanza del server torna automaticamente a partecipare a tutte le sue sessioni di mirroring.  
  
     **Per eseguire un failover manuale**  
  
    -   [Failover manuale di una sessione di mirroring del database &#40;SQL Server Management Studio&#41;](database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   Eseguire [il failover manuale di una sessione di mirroring del Database &#40;&#41;Transact-SQL ](database-mirroring/manually-fail-over-a-database-mirroring-session-transact-sql.md).  
  
     Per informazioni sul funzionamento del failover manuale, vedere [Cambio di ruolo durante una sessione di mirroring del database &#40;SQL Server&#41;](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).  
  
2.  Attendere la sincronizzazione di ciascuna sessione di mirroring la cui istanza del server mirror è stata appena aggiornata. Quindi, connettersi all'istanza del server principale ed eseguire manualmente il failover della sessione. Con il failover, l'istanza del server aggiornata diventa il server principale per la sessione e il server principale precedente diventa il server mirror.  
  
     L'obiettivo di questo passaggio è consentire a un'altra istanza del server di diventare il server mirror in tutte le sessione di mirroring in cui è un server partner.  
  
3.  Dopo aver eseguito il failover, è consigliabile eseguire il comando [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) sul database principale.  
  
4.  Installare il Service Pack o l'hotfix in ciascuna istanza del server mirror in tutte le sessioni di mirroring in cui è un server partner. In questa fase potrebbe essere necessario aggiornare più server.  
  
    > [!IMPORTANT]  
    >  In una configurazione di mirroring complessa, alcune istanze del server potrebbero essere ancora il server principale originale in una o più sessioni di mirroring. Ripetere i passaggi 2-4 per le istanze del server finché non vengono aggiornate tutte le istanze di in questione.  
  
5.  Riprendere la sessione di mirroring.  
  
    > [!NOTE]  
    >  Il failover automatico non funzionerà finché il server di controllo del mirroring non verrà aggiornato.  
  
6.  Installare i Service Pack o gli hotfix su tutte le istanze del server rimanenti che sono server di controllo in tutte le sessioni di mirroring. Dopo che un server di controllo del mirroring aggiornato torna a partecipare a una sessione di mirroring, il failover automatico diventa nuovamente possibile. In questa fase potrebbe essere necessario aggiornare più server.  
  
### <a name="to-return-a-session-to-high-performance-mode"></a>Per ripristinare una sessione alla modalità a elevate prestazioni  
  
1.  Facoltativamente, tornare alla modalità a elevate prestazioni utilizzando uno dei metodi seguenti:  
  
    -   In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]: modificare l'opzione **Modalità operativa** e impostarla su **Prestazioni elevate (asincrona)** usando la [pagina Mirroring](../relational-databases/databases/database-properties-mirroring-page.md) della finestra di dialogo **Proprietà database** .  
  
    -   In [!INCLUDE[tsql](../includes/tsql-md.md)]: utilizzare [ALTER database](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring) per impostare la protezione delle transazioni su off.  
  
### <a name="to-return-a-witness-to-a-mirroring-session"></a>Per restituire un server di controllo del mirroring a una sessione di mirroring  
  
1.  Facoltativamente, nella modalità a protezione elevata, ristabilire il server di controllo del mirroring su ciascuna sessione di mirroring.  
  
     **Per ristabilire il server di controllo del mirroring**  
  
    -   [Aggiunta o sostituzione di un server di controllo del mirroring del database &#40;SQL Server Management Studio&#41;](database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
    -   [Aggiungere un server di controllo del mirroring del database utilizzando l'autenticazione di Windows &#40;Transact-SQL&#41;](database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Mirroring del database di ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Mirroring del database &#40;SQL Server&#41;](database-mirroring/database-mirroring-sql-server.md)   
 [Modalità di funzionamento del mirroring del database](database-mirroring/database-mirroring-operating-modes.md)   
 [Cambio di ruolo durante una sessione di mirroring del database &#40;SQL Server&#41;](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Avvia Monitoraggio mirroring del database &#40;SQL Server Management Studio&#41;](database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Visualizzazione dello stato di un database con mirroring &#40;SQL Server Management Studio&#41;](database-mirroring/view-the-state-of-a-mirrored-database-sql-server-management-studio.md)  
  
  
