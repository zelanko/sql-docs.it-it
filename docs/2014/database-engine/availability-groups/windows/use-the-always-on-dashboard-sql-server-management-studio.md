---
title: Usare il Dashboard AlwaysOn (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
- Availability Groups [SQL Server], dashboard
ms.assetid: c9ba2589-139e-42bc-99e1-94546717c64d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c4402cd9e7c02b598c47a851c8318e7c840bfbc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788728"
---
# <a name="use-the-alwayson-dashboard-sql-server-management-studio"></a>Utilizzare il Dashboard AlwaysOn (SQL Server Management Studio)
  Gli amministratori del database utilizzano il dashboard AlwaysOn per ottenere una vista immediata dell'integrità di un gruppo di disponibilità AlwaysOn e delle relative repliche di disponibilità e database in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Alcuni degli utilizzi tipici del dashboard AlwaysOn sono i seguenti:  
  
-   Scelta di una replica per un failover manuale.  
  
-   Stima della perdita di dati in caso di failover forzato.  
  
-   Valutazione delle prestazioni della sincronizzazione dei dati.  
  
-   Valutazione dell'impatto sulle prestazioni di una replica secondaria con commit sincrono  
  
 Il dashboard AlwaysOn fornisce indicatori delle prestazioni e stati dei gruppi di disponibilità principali che facilitano le decisioni operative relative alla disponibilità elevata utilizzando i tipi di informazioni seguenti.  
  
-   Stato di rollup della replica  
  
-   Modalità e stato di sincronizzazione  
  
-   Perdita di dati stimata  
  
-   Tempo di recupero stimato (ripetere aggiornamento)  
  
-   Dettagli della replica di database  
  
-   Modalità e stato di sincronizzazione  
  
-   Tempo per il ripristino del log  
  
 
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 È necessario essere connessi all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (istanza del server) che ospita la replica primaria o una replica secondaria di un gruppo di disponibilità.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre delle autorizzazioni CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION.  
  
##  <a name="SSMSProcedure"></a> Per avviare il AlwaysOn Dashboard  
  
1.  In Esplora oggetti connettersi all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui si desidera eseguire il dashboard AlwaysOn.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** , fare clic con il pulsante destro del mouse sul nodo **Gruppi di disponibilità** , quindi fare clic su **Mostra dashboard**.  
  
###  <a name="DashboardOptions"></a> Per modificare le opzioni del Dashboard AlwaysOn  
 È possibile usare la finestra di dialogo [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]**Opzioni** per configurare il comportamento del dashboard AlwaysOn di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per l'aggiornamento automatico e l'abilitazione di criteri AlwaysOn definiti automaticamente.  
  
1.  Dal menu **Strumenti** scegliere **Opzioni**.  
  
2.  Per aggiornare automaticamente il dashboard, nella finestra di dialogo **Opzioni** selezionare **Abilita aggiornamento automatico**, immettere l'intervallo di aggiornamento in secondi, quindi immettere per quante volte si desidera tentare di stabilire la connessione.  
  
3.  Per abilitare criteri definiti dall'utente, selezionare **Abilita criteri AlwaysOn definiti dall'utente**.  
  
##  <a name="AvGroupsView"></a> Riepilogo del gruppo di disponibilità  
 Nella schermata del gruppo di disponibilità viene visualizzata una riga di riepilogo per ogni gruppo di disponibilità per il quale l'istanza del server connesso ospita una replica. In questo riquadro sono visualizzate le colonne seguenti:  
  
 **Nome gruppo di disponibilità**  
 Nome di un gruppo di disponibilità per il quale l'istanza del server connesso ospita una replica.  
  
 **Istanza primaria**  
 Nome dell'istanza del server che ospita la replica primaria del gruppo di disponibilità.  
  
 **Modalità di failover**  
 Visualizza la modalità di failover per cui è configurata la replica. I possibili valori per le modalità di failover sono:  
  
-   **Automatico** Indica che una o più repliche sono in modalità di failover automatico.  
  
-   **Manuale**. Indica che non vi sono repliche in modalità di failover automatico.  
  
 **Problemi**  
 Fare clic sul collegamento **Problemi** per aprire la documentazione di risoluzione dei problemi relativa a un determinato problema. Per un elenco di tutti i problemi di criteri AlwaysOn, vedere [i criteri AlwaysOn per problemi operativi con gruppi di disponibilità AlwaysOn (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md).  
  
> [!TIP]  
>  Fare clic sulle intestazioni di colonna per ordinare le informazioni sul gruppo di disponibilità in base al nome del gruppo di disponibilità, all'istanza primaria, alla modalità di failover o al problema.  
  
##  <a name="AvGroupDetails"></a> Dettagli del gruppo di disponibilità  
 Le informazioni dettagliate riportate di seguito vengono visualizzate per il gruppo di disponibilità selezionato nello schermata di riepilogo:  
  
 **Stato gruppo di disponibilità**  
 Visualizza lo stato di integrità del gruppo di disponibilità.  
  
 **Primary instance**  
 Nome dell'istanza del server che ospita la replica primaria del gruppo di disponibilità.  
  
 **Failover mode**  
 Visualizza la modalità di failover per cui è configurata la replica. I possibili valori per le modalità di failover sono:  
  
-   **Automatico** Indica che una o più repliche sono in modalità di failover automatico.  
  
-   **Manuale**. Indica che non vi sono repliche in modalità di failover automatico.  
  
 **Stato cluster**  
 Nome e stato del cluster in cui l'istanza del server connesso e del gruppo di disponibilità è un nodo membro.  
  
##  <a name="AvReplicaDetails"></a> Dettagli replica di disponibilità  
 Nel riquadro **Replica di disponibilità** vengono visualizzate le colonne seguenti:  
  
 **Name**  
 Nome dell'istanza del server che ospita la replica di disponibilità. Questa colonna viene visualizzata per impostazione predefinita.  
  
 **Ruolo**  
 Indica il ruolo corrente della replica di disponibilità, ovvero **Primario** o **Secondario**. Per informazioni sui ruoli di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md). Questa colonna viene visualizzata per impostazione predefinita.  
  
 **Modalità di failover**  
 Visualizza la modalità di failover per cui è configurata la replica. I possibili valori per le modalità di failover sono:  
  
-   **Automatico** Indica che una o più repliche sono in modalità di failover automatico.  
  
-   **Manuale**. Indica che non vi sono repliche in modalità di failover automatico.  
  
 **Stato di sincronizzazione**  
 Indica se una replica secondaria è attualmente sincronizzata con la replica primaria. Questa colonna viene visualizzata per impostazione predefinita. I valori possibili sono:  
  
-   **Non sincronizzato**. Uno o più database nella replica non sono sincronizzati o non ne è ancora stato creato un join al gruppo di disponibilità.  
  
-   **Sincronizzazione in corso**. Uno o più database nella replica vengono sincronizzati.  
  
-   **Sincronizzato**. Tutti i database nella replica secondaria sono sincronizzati con i database primari corrispondenti nella replica primaria corrente o nell'ultima replica primaria.  
  
    > [!NOTE]  
    >  Nella modalità prestazioni, il database non si trova mai nello stato sincronizzato.  
  
-   **NULL**. Stato sconosciuto. Si ottiene questo valore quando l'istanza del server locale non è in grado di comunicare con il cluster di failover WSFC, ovvero il nodo locale non fa parte del quorum WSFC.  
  
 **Problemi**  
 Indica il nome del problema. Questo valore è visualizzato per impostazione predefinita. Per un elenco di tutti i problemi di criteri AlwaysOn, vedere [i criteri AlwaysOn per problemi operativi con gruppi di disponibilità AlwaysOn (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md).  
  
 **Modalità di disponibilità**  
 Indica la proprietà della replica impostata separatamente per ogni replica di disponibilità. Questo valore è nascosto per impostazione predefinita. I valori possibili sono:  
  
-   **Asincrona**. La replica secondaria non è mai sincronizzata con la replica primaria.  
  
-   **Synchronous**. Quando si esegue l'aggiornamento al database primario, un database secondario entra in questo stato e rimane aggiornato finché continua la sincronizzazione dati per il database.  
  
 **Modalità connessione primaria**  
 Indica la modalità utilizzata per connettersi alla replica primaria.  Questo valore è nascosto per impostazione predefinita.  
  
 **Modalità connessione secondaria**  
 Indica la modalità utilizzata per connettersi alla replica secondaria.  Questo valore è nascosto per impostazione predefinita.  
  
 **Stato connessione**  
 Indica se una replica secondaria è attualmente connessa alla replica primaria. Questa colonna è nascosta per impostazione predefinita. I valori possibili sono:  
  
-   **Disconnesso**. Per una replica di disponibilità remota, indica che è disconnessa dalla replica di disponibilità locale. La risposta della replica locale allo stato Disconnesso dipende dal relativo ruolo:  
  
    -   Sulla replica primaria, se una replica secondaria è disconnessa, i database secondari sono contrassegnati come **Non sincronizzato** sulla replica primaria e la replica primaria attende che la replica secondaria venga riconnessa.  
  
    -   Sulla replica secondaria, dopo avere rilevato che è disconnessa, tenta di riconnettersi alla replica primaria.  
  
-   **Connected**: Una replica di disponibilità remota attualmente connessa alla replica locale.  
  
 **Stato operativo**  
 Indica lo stato operativo corrente della replica secondaria. Questo valore è nascosto per impostazione predefinita. I valori possibili sono:  
  
 **0**. Failover in sospeso  
  
 **1**. In sospeso  
  
 **2**. Online  
  
 **3**. Offline  
  
 **4**. Non riuscito  
  
 **5**. Errore, nessun quorum  
  
 **NULL**. La replica non è locale.  
  
 **Ultimo errore di connessione.**  
 Numero dell'ultimo errore di connessione.  Questo valore è nascosto per impostazione predefinita.  
  
 **Descrizione ultimo errore di connessione**  
 Descrizione dell'ultimo errore di connessione.  Questo valore è nascosto per impostazione predefinita.  
  
 **Ora dell'ultimo errore di connessione**  
 Timestamp dell'ultimo errore di connessione. Questo valore è nascosto per impostazione predefinita.  
  
> [!NOTE]  
>  Per informazioni sui contatori delle prestazioni per le repliche di disponibilità, vedere [SQL Server, replica di disponibilità](../../../relational-databases/performance-monitor/sql-server-availability-replica.md).  
  
##  <a name="AvDbDetails"></a> Per raggruppare le informazioni su un gruppo di disponibilità  
 Per raggruppare le informazioni, fare clic su **Raggruppa per**, quindi selezionare una delle opzioni seguenti:  
  
-   **Repliche di disponibilità**  
  
-   **Database di disponibilità**  
  
-   **Synchronization state**  
  
-   **Conformità del failover**  
  
-   **Problemi**  
  
 Nel riquadro in cui sono visualizzate le informazioni raggruppate sono presenti le colonne seguenti:  
  
 **Name**  
 Nome del database di disponibilità. Questo valore è visualizzato per impostazione predefinita.  
  
 **Replica**  
 Nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che ospita la replica di disponibilità. Questo valore è visualizzato per impostazione predefinita.  
  
 **Stato di sincronizzazione**  
 Indica se il database di disponibilità è attualmente sincronizzato con la replica primaria. Questo valore è visualizzato per impostazione predefinita. I possibili stati di sincronizzazione sono i seguenti:  
  
-   **Non in sincronizzazione**.  
  
    -   Per il ruolo primario, indica che il database non è pronto per la sincronizzazione del log delle transazioni con i database secondari corrispondenti.  
  
    -   Per un database secondario, indica che il database non ha ancora avviato la sincronizzazione del log a causa di un problema di connessione, è stato sospeso o si trova in stati di transizione durante l'avvio o un cambio di ruolo.  
  
-   **Sincronizzazione in corso**.  
  
     Su una replica primaria:  
  
    -   Per un database primario, indica che questo database è pronto ad accettare una richiesta di analisi da un database secondario.  
  
    -   Su una replica secondaria, indica che è in corso uno spostamento dati attivo per quel database secondario.  
  
     Su una replica secondaria, indica che è in corso uno spostamento dati attivo per quella replica.  
  
-   **Sincronizzato**.  
  
     Per un database primario, indica che almeno un database secondario è sincronizzato.  
  
     Per un database secondario, indica che il database è sincronizzato con il database primario corrispondente.  
  
-   **Ripristino in corso**.  
  
     Indica la fase del processo di rollback in cui un database secondario ottiene attivamente le pagine dal database primario.  
  
    > [!CAUTION]  
    >  Quando un database si trova nello stato REVERTING, il failover forzato sulla replica secondaria può lasciare il database in uno stato in cui non può essere avviato.  
  
-   **Inizializzazione**.  
  
     Indica la fase di rollback in cui il log delle transazioni necessario a un database secondario per l'intercettazione dell'LSN di rollback viene fornito e finalizzato su una replica secondaria.  
  
    > [!CAUTION]  
    >  Quando un database si trova nello stato INITIALIZING, il failover forzato sulla replica secondaria lascerà sempre il database in uno stato in cui non può essere avviato.  
  
 **Failover Readiness**  
 Indica per quale replica di disponibilità è possibile eseguire il failover con o senza la potenziale perdita di dati. Questa colonna viene visualizzata per impostazione predefinita. I valori possibili sono:  
  
-   **Perdita di dati**  
  
-   **Nessuna perdita di dati**  
  
 **Problemi**  
 Indica il nome del problema. Questa colonna viene visualizzata per impostazione predefinita. I valori possibili sono:  
  
-   **Avvisi**. Fare clic per visualizzare le soglie e gli avvisi.  
  
-   **Critico**. Fare clic per visualizzare i problemi critici.  
  
 Per un elenco di tutti i problemi di criteri AlwaysOn, vedere [i criteri AlwaysOn per problemi operativi con gruppi di disponibilità AlwaysOn (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md).  
  
 **Sospeso**  
 Indica se il database è **Sospeso** o **Ripreso**. Questo valore è nascosto per impostazione predefinita.  
  
 **Motivo di sospensione**  
 Indica il motivo dello stato di sospensione. Questo valore è nascosto per impostazione predefinita.  
  
 **Perdita di dati stimata (secondi)**  
 Indica la differenza di orario dell'ultimo record del log delle transazioni nelle repliche primaria e secondaria. In caso di errore della replica primaria, andranno persi tutti i record del log delle transazioni entro il tempo specificato. Questo valore è nascosto per impostazione predefinita.  
  
 **Tempo di recupero stimato (secondi)**  
 Indica il tempo in secondi necessario per ripetere l'aggiornamento. Il *tempo di aggiornamento* è il tempo richiesto dalla replica secondaria per l'aggiornamento alla replica primaria. Questo valore è nascosto per impostazione predefinita.  
  
 **Prestazioni di sincronizzazione (secondi)**  
 Indica il tempo in secondi necessario per la sincronizzazione tra le repliche primaria e secondaria. Questo valore è nascosto per impostazione predefinita.  
  
 **Dimensione coda di invio log (KB)**  
 Indica il numero di record del log nei file di log del database primario che non sono stati inviati alla replica secondaria. Questo valore è nascosto per impostazione predefinita.  
  
 **Velocità di invio log (KB/sec)**  
 Indica la velocità in KB al secondo alla quale i record di log vengono inviati alla replica secondaria. Questo valore è nascosto per impostazione predefinita.  
  
 **Dimensione coda di rollforward (KB)**  
 Indica il numero di record del log nei file di log della replica secondaria di cui non è stato ancora eseguito il rollforward. Questo valore è nascosto per impostazione predefinita.  
  
 **Velocità fase di rollforward (KB/sec)**  
 Indica la velocità in KB al secondo alla quale viene eseguito il rollforward dei record di log. Questo valore è nascosto per impostazione predefinita.  
  
 **Velocità di invio flusso di file (KB/sec)**  
 Indica la velocità del flusso di file in KB al secondo con cui avviene l'invio delle transazioni alla replica. Questo valore è nascosto per impostazione predefinita.  
  
 **LSN di fine log**  
 Indica il numero di sequenza del file di log (LSN) effettivo corrispondente all'ultimo record di log nella cache log nelle repliche primarie e secondarie. Questo valore è nascosto per impostazione predefinita.  
  
 **LSN recupero**  
 Indica la fine del log delle transazioni prima che la replica scriva qualsiasi nuovo record del log dopo il failover o il recupero nella replica primaria. Questo valore è nascosto per impostazione predefinita.  
  
 **LSN troncamento**  
 Indica il valore minimo di troncamento del log per la replica primaria. Questo valore è nascosto per impostazione predefinita.  
  
 **LSN ultimo commit**  
 Indica l'LSN effettivo corrispondente all'ultimo record di commit nel log delle transazioni. Questo valore è nascosto per impostazione predefinita.  
  
 **Ora ultimo commit**  
 Indica l'ora che corrisponde all'ultimo record di commit. Questo valore è nascosto per impostazione predefinita.  
  
 **LSN ultimo invio**  
 Indica il punto fino a cui tutti i blocchi di log sono stati inviati dalla replica primaria. Questo valore è nascosto per impostazione predefinita.  
  
 **Ora ultimo invio**  
 Indica l'ora di invio dell'ultimo blocco del log. Questo valore è nascosto per impostazione predefinita.  
  
 **LSN ultima ricezione**  
 Indica il punto fino a cui tutti i blocchi di log sono stati ricevuti dalla replica secondaria che ospita il database secondario. Questo valore è nascosto per impostazione predefinita.  
  
 **Ora ultima ricezione**  
 Indica l'ora in cui è stato letto l'identificatore del blocco di log nell'ultimo messaggio ricevuto sulla replica secondaria. Questo valore è nascosto per impostazione predefinita.  
  
 **LSN ultima finalizzazione**  
 Indica il punto fino a cui tutti i record di log sono stati scaricati su disco sulla replica secondaria. Questo valore è nascosto per impostazione predefinita.  
  
 **Ora ultima finalizzazione**  
 Indica l'ora di ricezione dell'identificatore del blocco di log per il valore LSN finale sulla replica secondaria. Questo valore è nascosto per impostazione predefinita.  
  
 **LSN ultimo rollforward**  
 Indica l'LSN effettivo del record di log di cui è stato eseguito il rollforward per ultimo nella replica secondaria. Questo valore è nascosto per impostazione predefinita.  
  
 **Ora ultimo rollforward**  
 Indica l'ora di rollforward dell'ultimo record del log nel database secondario. Questo valore è nascosto per impostazione predefinita.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Usare i criteri AlwaysOn per visualizzare l'integrità di un gruppo di disponibilità &#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)   
 [Monitoraggio di Gruppi di disponibilità &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
