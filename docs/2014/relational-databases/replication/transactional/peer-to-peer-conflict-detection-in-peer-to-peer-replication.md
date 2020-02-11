---
title: Peer-to-peer - Rilevamento dei conflitti nella replica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, peer-to-peer replication
- peer-to-peer transactional replication, conflict detection
ms.assetid: 754a1070-59bc-438d-998b-97fdd77d45ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9db326ac27a7137f03f34e242c3c5c3931637f36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68198988"
---
# <a name="conflict-detection-in-peer-to-peer-replication"></a>Rilevamento dei conflitti nella replica peer-to-peer
  La replica transazionale peer-to-peer consente di inserire, aggiornare o eliminare dati in qualsiasi nodo di una topologia e di propagare le modifiche agli altri nodi. Poiché è possibile modificare i dati in qualsiasi nodo, si potrebbe verificare un conflitto tra le modifiche apportate ai dati in nodi diversi. Se una riga viene modificata in più nodi, può causare un conflitto o persino la perdita di un aggiornamento quando viene propagata in altri nodi.  
  
 Con la replica peer-to-peer in [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e versioni successive, viene introdotta l'opzione che consente di abilitare il rilevamento dei conflitti in una topologia peer-to-peer. Questa opzione consente di evitare problemi causati da conflitti non rilevati, tra cui il comportamento incoerente dell'applicazione e la perdita di aggiornamenti. Se questa opzione è abilitata, per impostazione predefinita una modifica in conflitto viene considerata come un errore critico che impedisce il corretto funzionamento dell'agente di distribuzione. In caso di conflitto, la topologia rimane in uno stato incoerente finché il conflitto non viene risolto e i dati non vengono resi coerenti nell'intera topologia.  
  
> [!NOTE]  
>  Per prevenire potenziali incoerenze dei dati, evitare che si verifichino conflitti in una topologia peer-to-peer, anche quando il rilevamento dei conflitti è abilitato. Per garantire che le operazioni di scrittura relative a una determinata riga vengano eseguite in un unico nodo, le applicazioni che accedono e modificano i dati devono partizionare le operazioni di inserimento, aggiornamento ed eliminazione. Tale partizionamento assicura che le modifiche apportate a una determinata riga in un singolo nodo vengano sincronizzate con tutti gli altri nodi della topologia prima che la riga venga modificata da un nodo diverso. Se un'applicazione richiede funzionalità avanzate di rilevamento e risoluzione dei conflitti, utilizzare la replica di tipo merge. Per altre informazioni, vedere [Replica di tipo merge](../merge/merge-replication.md) e [Rilevare e risolvere i conflitti tra repliche di tipo merge](../merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
## <a name="understanding-conflicts-and-conflict-detection"></a>Informazioni sui conflitti e sul relativo rilevamento  
 In un singolo database le modifiche apportate alla stessa riga da applicazioni diverse non generano un conflitto, in quanto le transazioni sono serializzate e vengono utilizzati blocchi per gestire le modifiche simultanee. In un sistema distribuito asincrono, ad esempio la replica peer-to-peer, le transazioni agiscono in modo indipendente su ogni nodo e non sono presenti meccanismi per serializzarle tra più nodi. È possibile utilizzare un protocollo come il commit 2PC, che tuttavia influisce in modo significativo sulle prestazioni.  
  
 Nei sistemi come la replica peer-to-peer i conflitti non vengono rilevati quando viene eseguito il commit delle modifiche nei singoli peer. Vengono invece rilevati quando queste modifiche vengono replicate e applicate in altri peer. Nella replica peer-to-peer i conflitti vengono rilevati dalle stored procedure che applicano le modifiche a ogni nodo, in base a una colonna nascosta in ogni tabella pubblicata. Questa colonna nascosta archivia un ID costituito dalla combinazione tra un *ID origine* specificato per ogni nodo e la versione della riga. Durante la sincronizzazione, l'agente di distribuzione esegue le procedure per ogni tabella. Queste procedure applicano le operazioni di inserimento, aggiornamento ed eliminazione da altri peer. Se una delle procedure rileva un conflitto quando legge il valore della colonna nascosta, genera l'errore 22815 con un livello di gravità 16:  
  
 `A conflict of type '%s' was detected at peer %d between peer %d (incoming), transaction id %s  and peer %d (on disk), transaction id %s`  
  
 Per impostazione predefinita, a causa di questo errore l'agente di distribuzione arresta l'applicazione di modifiche a tale nodo. Per informazioni su come gestire i conflitti rilevati, vedere "Gestione dei conflitti" più avanti in questo argomento.  
  
> [!NOTE]  
>  Alla colonna nascosta può accedere solo un utente connesso tramite la connessione amministrativa dedicata (DAC, Dedicated Administrator Connection). Per informazioni sulle connessioni DAC, vedere [Connessione di diagnostica per gli amministratori di database](../../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).  
  
 La replica peer-to-peer rileva i tipi seguenti di conflitti:  
  
-   Inserimento-inserimento  
  
     Tutte le righe di ogni tabella che partecipa alla replica peer-to-peer sono identificate in modo univoco tramite valori di chiave primaria. Un conflitto di tipo inserimento-inserimento si verifica quando viene inserita una riga con lo stesso valore di chiave in più di un nodo.  
  
-   Aggiornamento-aggiornamento  
  
     Si verifica quando la stessa riga viene aggiornata in più di un nodo.  
  
-   Inserimento-aggiornamento  
  
     Si verifica se una riga viene aggiornata in un nodo ma viene anche eliminata e quindi reinserita in un altro nodo.  
  
-   Inserimento-eliminazione  
  
     Si verifica se una riga viene eliminata in un nodo ma viene anche eliminata e quindi reinserita in un altro nodo.  
  
-   Aggiornamento-eliminazione  
  
     Si verifica se una riga viene aggiornata in un nodo ma viene anche eliminata in un altro nodo.  
  
-   Eliminazione-eliminazione  
  
     Si verifica quando una riga viene eliminata in più di un nodo.  
  
## <a name="enabling-conflict-detection"></a>Abilitazione del rilevamento dei conflitti  
 Per usare il rilevamento dei conflitti, tutti i nodi devono eseguire [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] o versioni successive e il rilevamento deve essere abilitato per tutti i nodi. In [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e versioni successive il rilevamento dei conflitti è abilitato per impostazione predefinita in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Si consiglia di lasciare abilitato il rilevamento, anche negli scenari in cui non si prevedono conflitti. Per abilitare e disabilitare il rilevamento dei conflitti, è possibile utilizzare le stored procedure [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)] :  
  
-   Per abilitare e disabilitare il rilevamento in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] , è possibile utilizzare la pagina **Opzioni della sottoscrizione** della finestra di dialogo **Proprietà pubblicazione** o la pagina **Configura topologia** della Configurazione guidata topologia peer-to-peer.  
  
     Se si configura il rilevamento dei conflitti utilizzando [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], l'agente di distribuzione viene configurato per arrestare l'applicazione di modifiche quando viene rilevato un conflitto.  
  
-   Per abilitare e disabilitare il rilevamento, è anche possibile utilizzare le stored procedure seguenti: [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) o [sp_configure_peerconflictdetection](/sql/relational-databases/system-stored-procedures/sp-configure-peerconflictdetection-transact-sql).  
  
     Se si configura il rilevamento dei conflitti utilizzando le stored procedure, è possibile specificare se l'agente di distribuzione deve arrestare l'applicazione di modifiche quando viene rilevato un conflitto. Per impostazione predefinita, l'agente si arresta. È consigliabile utilizzare l'impostazione predefinita.  
  
## <a name="handling-conflicts"></a>Gestione dei conflitti  
 Quando si verifica un conflitto nella replica peer-to-peer, viene generato l'avviso di rilevamento dei conflitti peer-to-peer. Si consiglia di configurare questo avviso in modo da ricevere una notifica quando si verifica un conflitto. Per altre informazioni sugli avvisi, vedere [Usare gli avvisi per gli eventi degli agenti di replica](../agents/use-alerts-for-replication-agent-events.md).  
  
 Dopo l'arresto dell'agente di distribuzione e la generazione dell'avviso, utilizzare uno degli approcci seguenti per gestire i conflitti che si sono verificati:  
  
-   Reinizializzare il nodo in cui è stato rilevato il conflitto dal backup di un nodo contenente i dati necessari (approccio consigliato). Questo metodo assicura che i dati siano in uno stato coerente.  
  
-   Tentare di sincronizzare nuovamente il nodo consentendo all'agente di distribuzione di continuare ad applicare le modifiche:  
  
    1.  Execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql): specificare ' p2p_continue_onconflict ' per il @property parametro e `true` per il @value parametro.  
  
    2.  Riavviare l'agente di distribuzione.  
  
    3.  Verificare i conflitti rilevati utilizzando il Visualizzatore conflitti e determinare le righe coinvolte, il tipo di conflitto e la riga in conflitto confermata. Il conflitto viene risolto in base al valore di ID origine specificato durante la configurazione: la riga che ha origine nel nodo con l'ID più alto è la riga in conflitto confermata. Per altre informazioni, vedere [Visualizzare i conflitti di dati per le pubblicazioni transazionali &#40;SQL Server Management Studio&#41;](../view-data-conflicts-for-transactional-publications-sql-server-management-studio.md).  
  
    4.  Eseguire la convalida per assicurare la corretta convergenza delle righe in conflitto. Per altre informazioni, vedere [Convalidare i dati replicati](../validate-data-at-the-subscriber.md).  
  
        > [!NOTE]  
        >  Se i dati sono incoerenti dopo questo passaggio, è necessario aggiornare manualmente le righe sul nodo con la massima priorità, quindi consentire la propagazione delle modifiche da questo nodo. Se non sono presenti ulteriori modifiche in conflitto nella topologia, tutti i nodi verranno portati in uno stato coerente.  
  
    5.  Execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql): specificare ' p2p_continue_onconflict ' per il @property parametro e `false` per il @value parametro.  
  
## <a name="see-also"></a>Vedere anche  
 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)  
  
  
