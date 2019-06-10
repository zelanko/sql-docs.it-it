---
title: Configurare criteri flessibili per il failover automatico di un gruppo di disponibilità
description: 'Descrizione delle varie opzioni disponibili per decidere il livello di flessibilità dei criteri di failover per un gruppo di disponibilità Always On. '
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- flexible failover policy
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 8c504c7f-5c1d-4124-b697-f735ef0084f0
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: a28e7f6a105d26d1dc68d295798e04c3d32edfd8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66772602"
---
# <a name="configure-a-flexible-automatic-failover-policy-for-an-always-on-availability-group"></a>Configurare criteri flessibili per il failover automatico di un gruppo di disponibilità Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Con i criteri di failover flessibili viene garantito un controllo granulare delle condizioni che causano un [failover automatico](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) per un gruppo di disponibilità. Modificando le condizioni di errore che attivano un failover automatico e la frequenza di controlli di integrità, è possibile aumentare o diminuire la probabilità di un failover automatico per supportare il Contratto di servizio per la disponibilità elevata.  
  
 I criteri di failover flessibili di un gruppo di disponibilità vengono definiti in base al relativo livello delle condizioni di errore e alla soglia di Timeout controllo integrità. Quando viene rilevato che un gruppo di disponibilità ha superato il livello di condizione di errore o la soglia di Timeout controllo integrità, la DLL risorse del gruppo di disponibilità risponde al cluster WSFC (Windows Server Failover Clustering). Tramite il cluster WSFC viene quindi iniziato un failover automatico alla replica secondaria.  
  
> [!IMPORTANT]  
>  Se un gruppo di disponibilità supera la relativa soglia di errore WSFC, non verrà effettuato il tentativo di failover automatico per il gruppo di disponibilità da parte del cluster WSFC. Inoltre, il gruppo di risorse WSFC del gruppo di disponibilità rimarrà in uno stato di errore finché l'amministratore del cluster non porterà manualmente online il gruppo di risorse con errori o l'amministratore del database non eseguirà un failover manuale del gruppo di disponibilità. La *soglia di errore WSFC* è definita come il numero massimo di errori supportati per il gruppo di disponibilità durante un determinato periodo di tempo. Il periodo di tempo predefinito è sei ore e il valore predefinito per il numero massimo di errori durante questo periodo è *n*-1, dove *n* è il numero di nodi WSFC. Per modificare i valori soglia dell'errore per un determinato gruppo di disponibilità, utilizzare la console di Gestione cluster di failover WSFC.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
-   [Soglia di Timeout controllo integrità](#HCtimeout)  
  
-   [Livello delle condizioni di errore](#FClevel)  
  
-   [Attività correlate](#RelatedTasks)  
  
-   [Contenuto correlato](#RelatedContent)  
  
##  <a name="HCtimeout"></a> Soglia di Timeout controllo integrità  
 La DLL risorse di WSFC del gruppo di disponibilità esegue un *controllo di integrità* della replica primaria chiamando la stored procedure [sp_server_diagnostics](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) sull'istanza di SQL Server che ospita la replica primaria. **sp_server_diagnostics** restituisce i risultati in un intervallo uguale a 1/3 della soglia di timeout controllo integrità per il gruppo di disponibilità. La soglia di timeout controllo integrità predefinita è 30 secondi, in base alla quale i risultati di **sp_server_diagnostics** vengono restituiti a intervalli di 10 secondi. Se la stored procedure **sp_server_diagnostics** risulta lenta o non restituisce informazioni, la DLL risorse attenderà per l'intero intervallo della soglia di timeout controllo integrità prima di determinare che la replica primaria non risponde. Se la replica primaria non risponde, viene avviato un failover automatico, se è attualmente supportato.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** non esegue controlli di integrità a livello di database.  
  
##  <a name="FClevel"></a> Livello delle condizioni di errore  
 La possibilità che i dati di diagnostica e le informazioni sull'integrità restituiti da **sp_server_diagnostics** assicurino un failover automatico dipende dal livello di condizione di errore del gruppo di disponibilità. Il *livello di condizione di errore* specifica quale condizione di errore attiverà un failover automatico. I livelli delle condizioni di errore sono 5 e vanno dal livello meno restrittivo (livello 1), al livello più restrittivo (livello 5). Un dato livello di condizione include tutti i livelli meno restrittivi. Il livello più restrittivo, il livello 5, include le quattro condizioni meno restrittive e così via.  
  
> [!IMPORTANT]  
>  I database danneggiati e quelli sospetti non vengono rilevati da alcun livello della condizione di errore. Pertanto, di un database danneggiato o sospetto, per un errore hardware, un danneggiamento dati o per altro problema, non viene mai attivato un failover automatico.  
  
 Nella tabella seguente vengono descritte le condizioni di errore corrispondenti a ciascun livello.  
  
|Level|Condizione di errore|[!INCLUDE[tsql](../../../includes/tsql-md.md)] Valore|Valore PowerShell|  
|-----------|-----------------------|------------------------------|----------------------|  
|Uno|In caso di server inaccessibile. Specifica che viene avviato un failover automatico quando si verifica una delle condizioni seguenti:<br /><br /> Il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non è attivo.<br /><br /> Il lease del gruppo di disponibilità per la connessione al cluster WSFC scade poiché non viene ricevuto alcun acknowledgement dall'istanza del server. Per altre informazioni, vedere [How It Works: SQL Server Always On Lease Timeout](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx) (Funzionamento: timeout lease di SQL Server Always On).<br /><br /> <br /><br /> Si tratta del livello meno restrittivo.|1|**OnServerDown**|  
|Due|In caso di mancata risposta del server. Specifica che viene avviato un failover automatico quando si verifica una delle condizioni seguenti:<br /><br /> L'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non si connette al cluster e viene superata la soglia Timeout controllo integrità specificata dall'utente per il gruppo di disponibilità.<br /><br /> La replica di disponibilità si trova in uno stato di errore.|2|**OnServerUnresponsive**|  
|Tre|In caso di errori critici del server. Specifica che viene avviato un failover automatico in caso di errori interni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] critici, ad esempio spinlock orfani, gravi violazioni dell'accesso in scrittura o dumping eccessivo.<br /><br /> Si tratta del livello predefinito.|3|**OnCriticalServerError**|  
|Quattro|In caso di errori con gravità moderata del server. Specifica che viene avviato un failover automatico in caso di errori interni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con gravità moderata, ad esempio una condizione persistente di memoria insufficiente nel pool di risorse interno di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|4|**OnModerateServerError**|  
|Cinque|In qualsiasi condizione di errore qualificata. Specifica che viene avviato un failover automatico in caso di qualsiasi condizione di errore qualificata, tra cui:<br /><br /> Rilevamento di un deadlock nell'utilità di pianificazione.<br /><br /> Rilevamento di un deadlock irrisolvibile.<br /><br /> <br /><br /> Si tratta del livello più restrittivo.|5|**OnAnyQualifiedFailureConditions**|  
  
> [!NOTE]  
>  La mancata risposta da parte di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] alle richieste client non è rilevante per gruppi di disponibilità.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per configurare il failover automatico**  
  
-   [Modificare la modalità di disponibilità di una replica di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md). Il failover automatico richiede la modalità di disponibilità con commit sincrono.  
  
-   [Modificare la modalità di failover di una replica di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Configurare i criteri di failover flessibili per controllare le condizioni per il failover automatico &#40;Gruppi di disponibilità Always On&#41;](../../../database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   [How It Works: SQL Server Always On Lease Timeout](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx) (Funzionamento: timeout lease di SQL Server Always On).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Modalità di disponibilità &#40;gruppi di disponibilità AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Failover e modalità di failover &#40;Gruppi di disponibilità AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [Windows Server Failover Clustering &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Criteri di failover per istanze del cluster di failover](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)  
  
  
