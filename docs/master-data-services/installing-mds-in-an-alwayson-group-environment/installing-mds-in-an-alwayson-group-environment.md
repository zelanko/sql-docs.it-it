---
title: Disponibilità elevata e ripristino di emergenza
ms.custom: seo-lt-2019
ms.date: 07/28/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: ''
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ad7041700d2ded9b20eb79b648d170333961745f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "73728098"
---
# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>Disponibilità elevata e ripristino di emergenza per Master Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive una soluzione per Master Data Services (MDS) ospitata in Always On configurazione del gruppo di disponibilità. Questo articolo descrive come installare e configurare SQL 2016 Master Data Services in un gruppo di disponibilità SQL 2016 Always On (AG). Lo scopo principale di questa soluzione consiste nel migliorare la disponibilità elevata e il recupero di emergenza dei dati di back-end di MDS ospitati in un database di SQL Server.

## <a name="introduction"></a>Introduzione

Questo articolo descrive una soluzione per Master Data Services (MDS) ospitata in una configurazione Always On gruppo di disponibilità. Questo articolo descrive come installare e configurare SQL 2016 MDS in un gruppo di disponibilità Always On (AG) di SQL 2016. Lo scopo principale di questa soluzione consiste nel migliorare la disponibilità elevata e il recupero di emergenza dei dati di back-end di MDS ospitati in un database di SQL Server.

Per implementare la soluzione, è necessario completare le attività seguenti illustrate in questo articolo.

1. [Installare e configurare Windows Server Failover Cluster (WSFC)](#windows-server-failover-cluster-wsfc).

2. [Configurare un gruppo di disponibilità always on](#sql-server-always-on-availability-group).

3. [Configurare MDS per l'esecuzione in un nodo WSFC](#configure-mds-to-run-on-an-wsfc-node).

Le sezioni precedenti presenteranno brevemente le tecnologie, seguite dalle istruzioni relative. Per informazioni dettagliate sulle tecnologie, vedere i collegamenti ai documenti in ogni sezione.

Questa soluzione descritta in questo articolo si basa su un gruppo di disponibilità, in cui ogni database dispone di più repliche sincrone o asincrone. Solo una replica accetta la transazione, ovvero accetta le richieste utente. Si tratta della replica primaria.

Ogni replica ha la propria archiviazione, pertanto non esiste alcuna archiviazione centralizzata condivisa in questa soluzione. Quando si verifica un errore software o hardware che interessa la replica primaria, è possibile eseguire il failover della replica primaria in una replica sincrona o asincrona automaticamente o manualmente in base alla configurazione e alle situazioni. In questo modo si garantisce la disponibilità elevata del database con interruzioni minime per gli utenti.

Le repliche asincrone sono in genere ospitate in un data center remoto rispetto a quello della replica primaria. In caso di scenari di emergenza, è possibile eseguire il failover della replica primaria in un altro data center. In questo modo si garantisce il ripristino di emergenza del database.

A scopo dimostrativo, la soluzione descritta in questo articolo usa le versioni seguenti del software. Le versioni precedenti dovrebbero funzionare allo stesso modo, con differenze minime.

- Windows Server 2012R2 con cluster di failover
- SQL Server 2016 con funzionalità Master Data Services

La soluzione usa anche due macchine virtuali, **MDS-HA1** e **MDS-HA2**, per ospitare due repliche. A condizione che sia supportato da un gruppo di disponibilità, MDS non limita il numero di repliche che è possibile usare.

In questo articolo si presuppone che l'utente disponga di una conoscenza di base di Windows Server, cluster di failover di Windows Server, AGs e SQL Server MDS.

## <a name="what-is-not-covered"></a>Argomenti non trattati

Il documento non copre gli argomenti seguenti:

- Come assicurare la disponibilità elevata e il recupero dopo un'emergenza di IIS, il server Web che ospita l'interfaccia utente di Master Data Services. MDS non impone alcun requisito specifico per IIS, quindi per assicurare la disponibilità elevata e il bilanciamento del carico di ISS possono essere usate le tecniche standard anche in questo contesto.

- Come usare un SQL Server Always On istanza del cluster di failover (FCI) per supportare la disponibilità elevata nel back-end MDS. Il clustering di failover di SQL Server è una soluzione a disponibilità elevata diversa, è ufficialmente supportata da SQL Server e funziona con MDS.

- Come usare una soluzione ibrida di un'istanza FCI e un gruppo di disponibilità per supportare la disponibilità elevata nel back-end MDS. La soluzione ibrida funziona con MDS.

## <a name="design-consideration"></a>Considerazioni sulla progettazione

Nella figura 1 viene illustrata una configurazione tipica utilizzata principalmente in un gruppo di disponibilità. Nel data center principale esistono due repliche con una relazione di commit sincrono ed entrambe hanno il privilegio di voto. Ciò consente di migliorare la disponibilità elevata nel caso in cui la replica primaria abbia esito negativo.

Nel data center del ripristino di emergenza esiste una replica secondaria con una relazione di commit asincrono con la replica primaria. Questo data center è in genere in un'area geografica diversa da quella del data center principale. La replica secondaria non ha il privilegio di voto.

Questa configurazione viene usata per ottenere il ripristino in caso di emergenza del data center primario, ad esempio un incendio, un terremoto e così via. La configurazione consente di ottenere disponibilità elevata e ripristino di emergenza con costi relativamente ridotti.

![Configurazione tipica per un gruppo di disponibilità Always On](media/Fig1_TypicalConfig.png)

Figura 1. Configurazione tipica di un gruppo di disponibilità Always On

Se non è necessario prendere in considerazione il ripristino di emergenza, non occorre avere una replica in un secondo data center. Se è necessario migliorare la disponibilità elevata, è possibile avere più repliche sincrone nello stessa data center principale.

Pertanto, è importante prendere in considerazione i requisiti e gli scenari e decidere di quante repliche sincrone e asincrone si ha bisogno e in quale data center.

## <a name="windows-server-failover-cluster-wsfc"></a>Windows Server Failover Cluster (WSFC)

In questa sezione vengono trattate le attività seguenti.

1. [Installare la funzionalità Windows Failover Cluster](#install-failover-cluster-feature).

2. [Creare un cluster di failover di Windows Server](#create-a-windows-server-failover-cluster).

Come illustrato nella figura 1 nella sezione precedente, la soluzione descritta in questo articolo include Windows Server Failover Cluster (WSFC). È necessario configurare WSFC perché gli AGs dipendono da WFSC per il rilevamento e il failover degli errori.

WSFC è una funzionalità che migliora la disponibilità elevata di applicazioni e servizi. È costituita da un gruppo di istanze di Windows Server indipendenti che eseguono il servizio cluster di failover Microsoft. Le istanze di Windows Server, o nodi come vengono talvolta chiamate, sono connesse in modo che possano comunicare tra loro rendendo possibile il rilevamento degli errori. WSFC offre la funzionalità di rilevamento degli errori e il failover. Se un nodo o un servizio del cluster hanno esito negativo, viene rilevato l'errore e un altro nodo inizia automaticamente o manualmente ad offrire i servizi ospitati sul nodo in errore. Di conseguenza, le interruzioni per gli utenti sono minime e la disponibilità del servizio è migliorata.  

### <a name="prerequisites"></a>Prerequisiti

Il sistema operativo Windows Server deve essere installato in tutte le istanze e tutti gli aggiornamenti devono essere corretti.

> [!NOTE]
> È **vivamente consigliabile** installare la stessa versione di Windows e lo stesso set di funzionalità in tutte le istanze per evitare problemi di incompatibilità.

### <a name="install-failover-cluster-feature"></a>Installare la funzionalità di cluster di failover

Completare i passaggi seguenti per ogni istanza di Windows Server per installare la funzionalità WSFC in ogni istanza. Sono necessarie autorizzazioni di amministratore.

1. Aprire **Server Manager** in Windows Server e fare clic su **Aggiungi ruoli e funzionalità** nel riquadro di destra. Verrà avviata la **Add Roles and Feature Wizard** (Procedura guidata Aggiungi ruoli e funzionalità).

2. Fare clic su **Avanti** fino ad accedere alla pagina **Funzionalità**.

3. Selezionare la casella di controllo **Clustering di failover** e fare clic su **Avanti** per completare l'installazione. Vedere Figura 2.

   Se viene chiesta una conferma nella finestra **Add features that are required for Failover clustering** (Aggiungere funzionalità necessarie per il clustering di failover), fare clic su **Aggiungi funzionalità**. Vedere Figura 3.

   ![Procedura guidata Aggiungi ruoli e funzionalità, clustering di failover](media/Fig2_SelectFeatures.png)

   Figura 2

   ![Procedura guidata Aggiungi ruoli e funzionalità, necessaria per il cluster di failover](media/Fig3_RequiredFeaturesFailover.png)

   Figura 3

4. Nella pagina **Conferma** fare clic su **Installa** per installare la funzionalità di clustering di failover.

5. Nella pagina **Risultato** assicurarsi che l'installazione sia riuscita e che non siano visualizzati errori e avvisi.

### <a name="create-a-windows-server-failover-cluster"></a>Creare un cluster di failover di Windows Server

Quando la funzionalità WSFC è installata in tutte le istante, è possibile configurarla. È necessario eseguire questa operazione solo in un nodo.

1. Aprire **Server Manager** in Windows Server e fare clic su **Gestione cluster di failover** dal menu **Strumento** nell'angolo superiore destro per avviare la gestione.

2. In **Gestione cluster di failover** fare clic su **Convalida configurazione** nel riquadro di destra. Vedere Figura 4.

   ![Gestione cluster di failover, Convalida configurazione](media/Fig4_ValidateConfig.png)

   Figura 4

3. In **Convalida guidata** **configurazione** fare clic su **Avanti**.

4. Nella finestra di dialogo **Selezione dei server o di un cluster** aggiungere i nomi dei server che ospiteranno SQL Server e fare clic su **Avanti**. Vedere Figura 5.

   In questo esempio sono state aggiunte due istanze, MDS-HA1 e MDS-HA2.

   ![Convalida guidata configurazione, Selezione dei server o di un cluster](media/Fig5_AddServer.png)

   Figura 5

5. Nella pagina **Opzioni di testing** fare clic su **Esegui tutti i test** e quindi su **Avanti**.

6. Fare clic su **Avanti** per completare la convalida.

   Nella pagina **Convalida in corso** viene visualizzo lo stato di avanzamento e nella pagina **Riepilogo** il riepilogo della convalida. Vedere figure 6 e 7.

7. Nella pagina **Riepilogo** controllare eventuali messaggi di avviso o errore.

   Gli errori devono essere corretti. Tuttavia, gli avvisi possono non costituire un problema. Un messaggio di avviso significa che l'elemento testato potrebbe soddisfare il requisito, ma c'è qualcosa da controllare. Ad esempio, nella figura 7 è illustrato un avviso "Convalida latenza di accesso al disco" che potrebbe essere dovuto al fatto che il disco è temporaneamente occupato da altre attività. Il messaggio può essere ignorato. Per altri dettagli, vedere la documentazione online per ogni messaggio di avviso e di errore. Vedere Figura 7.
   
   ![Convalida guidata configurazione, pagina Convalida in corso](media/Fig6_ValidationTests.png)

   Figura 6

   ![Convalida guidata configurazione, pagina Riepilogo](media/Fig7_ValidationSummary.png)

   Figura 7

8. Nella pagina **Riepilogo** verificare che la casella di controllo **Crea il cluster ora utilizzando i nodi convalidati** sia selezionata e fare clic su **Fine** per avviare la **Creazione guidata** **cluster**.

9. Nella **Creazione guidata** **cluster** fare clic su **Avanti**.

10. Nella pagina **Punto di accesso per l'amministrazione del cluster** immettere il nome del cluster WSFC e fare clic su **Avanti**. In questo esempio viene usato il nome cluster "MDS-HA". Vedere Figura 8.

   ![Immettere il nome del cluster](media/Fig8_EnterClusterName.png)

   Figura 8

11. Continuare a fare clic su **Avanti** per completare la creazione del cluster. Nella sezione **Riepilogo del cluster MDS-HA** vengono visualizzate le informazioni sul cluster. Vedere Figura 9.

   ![Visualizzazione informazioni di riepilogo per il cluster](media/Fig9_ClusterSummary.png)

   Figura 9

   Se in un secondo momento è necessario aggiungere un nodo, fare clic sull'azione **Aggiungi nodo** nel riquadro di destra in **Gestione cluster di failover**.

Note:

- La funzionalità WSFC potrebbe non essere disponibile in tutte le edizioni di Windows Server. Assicurarsi che l'edizione in uso abbia questa funzionalità.

- Verificare di avere le autorizzazioni appropriate per configurare WSFC in Active Directory. Per altre informazioni, vedere [Failover Cluster Step-by-Step Guide: Configure Accounts in Active Directory](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx) (Guida dettagliata del cluster di failover: Configurare gli account in Active Directory).

Per altre informazioni su WSFC, vedere [Cluster di failover](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx).

## <a name="sql-server-always-on-availability-group"></a>SQL Server Always On gruppo di disponibilità

In questa sezione vengono trattate le attività seguenti.

1. [Abilitare SQL Server Always on gruppo di disponibilità](#enable-sql-server-always-on-availability-groups-on-every-sql-server-instance).

2. [Creare un gruppo di disponibilità](#create-an-availability-group).

3. [Convalidare e testare il gruppo di disponibilità](#validation-and-test-the-availability-group).

Always On dispone di due funzionalità per fornire disponibilità elevata e ripristino di emergenza per MDS, entrambe basate su WSFC.

- Gruppo di disponibilità Always On (AG)

- Always On istanza del cluster di failover (FCI).

Un gruppo di disponibilità fornisce disponibilità a livello di database. Il gruppo di disponibilità, ovvero un set di database utente, e il relativo nome di rete virtuale vengono registrati come risorse in WSFC.

Failover offrono disponibilità elevata a livello di istanza. Il servizio SQL Server e i servizi correlati vengono registrati come risorse in WSFC. La soluzione delle istanze del cluster di failover richiede l'archiviazione simmetrica su disco condiviso, ad esempio condivisioni di file SAN o SMB, che devono essere disponibili a tutti i nodi nel cluster WFC.
   
### <a name="prerequisites"></a>Prerequisiti

- Installare SQL Server in tutti i nodi. Per altre informazioni, vedere [Installare SQL Server 2016](../../database-engine/install-windows/install-sql-server.md).

- (Scelta consigliata) Installare esattamente lo stesso set di funzionalità e la stessa versione di SQL Server in ogni nodo. In particolare, è necessario installare MDS.

- (Scelta consigliata) Usare la stessa configurazione per tutte le istanze di SQL Server. In particolare, configurare le stesse regole di confronto del server in tutte le istanze di SQL Server.

- (Scelta consigliata) Usare lo stesso account servizio per eseguire tutte le istanze di SQL Server. In caso contrario, è necessario concedere l'autorizzazione per ogni istanza di SQL Server per assicurarsi che le istanze di SQL Server possano comunicare tra loro.

- Verificare che l'impostazione di Windows Firewall consenta alle istanze di SQL Server di comunicare tra loro.

### <a name="enable-sql-server-always-on-availability-groups-on-every-sql-server-instance"></a>Abilitare SQL Server Always On gruppi di disponibilità in ogni istanza di SQL Server

1. In **Gestione configurazione SQL Server** fare clic su **Servizio SQL server** nel riquadro a sinistra, fare clic con il pulsante destro del mouse su **SQL Server** nel riquadro a destra e quindi su **Proprietà**. Vedere Figura 10.

   ![Finestra Proprietà di SQL Server](media/Fig10_SQLServerProperties.png)

   Figura 10

2. Nella finestra di dialogo **proprietà** **SQL Server (MSSQLSERVER)** fare clic sulla scheda **disponibilità elevata always on** , quindi selezionare la casella di controllo **Abilita always on gruppi di disponibilità** . Quando viene visualizzato un valore nella casella di testo **Nome cluster di failover Windows**, fare clic su **OK** per continuare. Vedere Figura 11.

   ![Abilita Always On opzione gruppi di disponibilità](media/Fig11_EnableAlwaysOn.png)

   Figura 11

3. Quando viene visualizzata una pagina di avviso, fare clic su **OK** per continuare. Vedere Figura 12.

   ![Conferma arresto e riavvio servizio](media/Fig12_WarningServiceStopStart.png)

   Figura 12

4. Fare clic su **Riavvia** per riavviare il servizio **SQL Server** e rendere effettiva la modifica. Vedere Figura 10.

> [!NOTE]
> È possibile modificare l'account del servizio che esegue il servizio SQL Server tramite **Gestione configurazione SQL Server**. Fare clic sulla scheda **Accedi** nella finestra di dialogo **Proprietà** **SQL Server (MSSQLSERVER)**. Vedere Figura 11.

### <a name="create-an-availability-group"></a>Creare un gruppo di disponibilità

Una volta abilitata la funzionalità gruppo di disponibilità in tutte le istanze di SQL Server, viene creato un nuovo gruppo di disponibilità che contiene il database MDS in un nodo.

Il gruppo di disponibilità può essere creato solo sui database esistenti. Pertanto, o si crea un database MDS in un nodo, oppure si crea un database temporaneo che viene poi eliminato. In questo esempio viene creato un database MDS vuoto e un gruppo di disponibilità in tale database.

1. Avviare **SQL Server Management Studio** (**SSMS**) in un nodo e connettersi all'istanza di SQL Server locale con le credenziali appropriate.

2. In SSMS aprire una finestra di una **nuova query** ed eseguire lo script seguente per creare un database vuoto. Sostituire C:\\temp con il percorso che si vuole usare per eseguire un backup completo.

   ```sql
   CREATE DATABASE MDS\_Sample
   GO
   BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
   GO
   ```

   > [!NOTE]
   > Un backup completo del database è necessario per la creazione del gruppo di disponibilità nel database.

3. Nella **Esplora oggetti**espandere la cartella **Always on disponibilità elevata** e fare clic su **creazione guidata gruppo di disponibilità** per avviare la **creazione guidata nuovo gruppo di disponibilità**. Vedere Figura 13.

   ![Avvio della Creazione guidata Gruppo di disponibilità](media/Fig13_AvailabilityGroupsFolder.png)

   Figura 13

4. Nella **Creazione guidata Gruppo di disponibilità** fare clic su **Avanti** per visualizzare la pagina **Specifica nome**. Digitare un nome per il gruppo di disponibilità e fare clic su **Avanti**. Vedere Figura 14.

   ![Immettere il nome del gruppo di disponibilità](media/Fig14_AvailabilityGroupName.png)

   Figura 14

5. Fare clic sul database appena creato nella pagina **Selezione database** e fare clic su **Avanti**. Vedere Figura 15.

   ![Selezionare il database](media/Fig15_AvailabilityGroupSelectDatabase.png)

   Figura 15

6. Nella pagina **Specifica repliche** aggiungere un'altra replica facendo clic su **Aggiungi replica**. La pagina elenca già le istanze correnti di SQL Server locale come replica. Vedere Figura 16.

7. Nella finestra di dialogo **Connetti a server** aggiungere le credenziali appropriate e fare clic su **Connetti**.

   ![Connessione a un'istanza di SQL Server](media/Fig16_AddReplicaConnectServer.png)

   Figura 16

   A questo punto dovrebbero essere visualizzate due repliche nell'elenco. Ripetere questo passaggio per aggiungere altri nodi come repliche. Vedere Figura 17.

   ![Visualizzazione elenco repliche](media/Fig17_AvailabilityGroupSQLReplicas.png)

   Figura 17

   Per ogni replica, configurare le impostazioni **Commit sincrono**, **Failover automatico** e **Secondario leggibile** seguenti. Vedere Figura 17.

**Commit sincrono**: in questo modo si garantisce che se viene eseguito il commit di una transazione nella replica primaria di un database, viene eseguito anche in tutte le altre repliche sincrone. Il commit asincrono non garantisce questo aspetto e potrebbe rimanere indietro rispetto alla replica primaria.

In genere, è consigliabile abilitare il commit sincrono solo quando i due nodi sono nello stesso data center. Se sono in data center diversi, il commit sincrono può rallentare le prestazioni del database. Se questa casella di controllo non è selezionata, viene usato il commit asincrono.

**Failover automatico:** quando la replica primaria è inattiva, il gruppo di disponibilità esegue automaticamente il failover nella replica secondaria se è stato selezionato il failover automatico. Questa opzione può essere abilitata solo sulle repliche con commit sincrono.

**Secondario leggibile:** per impostazione predefinita, gli utenti non possono connettersi alle repliche secondarie. Questa opzione consente agli utenti di connettersi a una replica secondaria con accesso in sola lettura.

8. Nella pagina **Specifica repliche** fare clic sulla scheda **Listener** ed eseguire le operazioni seguenti. Vedere Figura 18.

   a. Fare clic su **Crea un listener del gruppo di disponibilità** per configurare un listener del gruppo di disponibilità per la connessione al database MDS.

   b. Immettere un **Nome DNS del listener**, ad esempio MDSSQLServer.

   c. Immettere la porta SQL predefinita, 1433, nella casella di testo **Porta**.

   d. Immettere DHCP nella casella di testo **Modalità di rete** e fare clic su **Avanti** per continuare.

   > [!NOTE]
   > Facoltativamente, è possibile scegliere "Indirizzo IP statico" come **Modalità di rete** e immettere un indirizzo IP statico. È anche possibile immettere una porta diversa dalla 1433.

   ![Configurare il listener](media/Fig18_AvailabilityGroupCreateListener.png)

   Figura 18

9. Nella pagina **Seleziona sincronizzazione dati** fare clic su **Completa** e specificare una condivisione di rete cui possano accedere tutti i nodi. Scegliere **Avanti** per continuare. Vedere Figura 19.

   Tale condivisione di rete verrà usata per archiviare il backup di database per creare le repliche secondarie. Se tale preferenza non è disponibile per l'organizzazione, scegliere un altro tipo di sincronizzazione dei dati. Per usare altre opzioni per creare repliche secondarie, vedere [SQL Server 2016 always on gruppo di disponibilità](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) . Nella figura 17 vengono elencate anche altre opzioni.

   ![Configurazione della sincronizzazione dei dati](media/Fig19_AvailabilityGroupDataSync.png)

   Figura 19 

10. Nella pagina **Convalida** assicurarsi che tutte le convalide siano state passate correttamente e correggere eventuali errori. Scegliere **Avanti** per continuare.

11. Nella pagina **Riepilogo** esaminare tutte le impostazioni di configurazione e fare clic su **Fine**. In questo modo verrà creato e configurato il gruppo di disponibilità.

12. Nella pagina **Risultato** verificare che tutti i passaggi necessari siano stati completati.

### <a name="validation-and-test-the-availability-group"></a>Convalidare e testare il gruppo di disponibilità

1. Aprire SSMS e connettersi al nome DNS del listener appena creato nella sezione [Creare un gruppo di disponibilità](#create-an-availability-group). In questo esempio è MDSSQLServer.

2. In **Esplora oggetti**espandere la cartella **Always on disponibilità elevata** , fare clic con il pulsante destro del mouse sul gruppo di disponibilità appena creato nella sezione [creare un gruppo di disponibilità](#create-an-availability-group) e quindi scegliere **Mostra dashboard**. Vedere Figura 20. Viene visualizzato lo stato del nuovo gruppo di disponibilità e delle relative repliche.

   ![Visualizzare il dashboard](media/Fig20_ShowDashboard.png)

   Figura 20 

3. Fare clic su **Failover** per eseguire il failover in una replica sincrona e in una replica asincrona. In questo modo è possibile verificare che il failover avvenga senza problemi.

   La configurazione del gruppo di disponibilità è stata completata.

Per altre informazioni sui gruppi di disponibilità Always On, vedere [SQL Server 2016 always on gruppi di disponibilità](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md).

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>Configurare MDS per l'esecuzione in un nodo WSFC

La soluzione presentata in questo articolo richiede solo il database back-end di MDS in esecuzione in WSFC. Altre parti di MDS, come ad esempio applicazioni Web e Gestione configurazione MDS, possono essere eseguite nel nodo WSFC o all'esterno di WSFC, purché MDS possa connettersi al gruppo di disponibilità.

1. Aprire **Gestione configurazione Master Data Services** in un nodo, fare clic su **Configurazione database** e fare clic su **Crea database** per avviare la **Creazione guidata database**.

2. Nella pagina **Server database** digitare il nome DNS del listener del gruppo di disponibilità nella casella di testo **Istanza di SQL Server**, fare clic su **Test connessione** e fare clic su **Avanti**. Vedere Figura 21.

   ![Configurare il server del database con listener del gruppo di disponibilità](media/Fig21_MDSDatabaseServerListener.png)

   Figura 21

3. Nella pagina **Database** digitare il nome del database creato nella sezione [Creare un gruppo di disponibilità](#create-an-availability-group) e fare clic su **Avanti**. Vedere figura 22.

   ![Creare e configurare il database](media/Fig22_MDSCreateDatabase.png)

   Figura 22

4. Completare la **Creazione guidata** **database**. Per altre informazioni, vedere [Installazione e configurazione di Master Data Services](../master-data-services-installation-and-configuration.md).

5. Fare clic su **Applicazioni Web** in **Gestione configurazione Master Data Services** per configurare l'applicazione Web e fare clic su **Applica** per applicare le impostazioni a MDS. Vedere figura 23. Per altre informazioni, vedere [Installazione e configurazione di Master Data Services](../master-data-services-installation-and-configuration.md).

   ![Configurare l'applicazione Web](media/Fig23_MDSWebApplication.png)

   Figura 23

   L'installazione di MDS è stata completata. È possibile ripetere i passaggi sopra descritti per configurare MDS affinché venga eseguito in tutti i nodi. Ogni gruppo di disponibilità ha il proprio database back-end.

6. Se in precedenza è stato creato un database temporaneo (vedere la sezione [creare un gruppo di disponibilità](#create-an-availability-group) ) per creare un gruppo di disponibilità, è necessario eliminare il database temporaneo

   Per altre informazioni su Master Data Services, vedere [Master Data Services](../master-data-services-overview-mds.md).

## <a name="conclusion"></a>Conclusioni

In questo white paper è stato illustrato come configurare e configurare il database back-end Master Data Services come parte di un gruppo di disponibilità. Questa configurazione offre disponibilità elevata e ripristino di emergenza nel database back-end di Master Data Services. Per implementare questa configurazione, è necessario installare e configurare Windows Server failover cluster, AG e Master Data Services.

## <a name="feedback"></a>Commenti e suggerimenti

Il documento è risultato utile? Per commenti e suggerimenti, fare clic su **Commenti** nella parte inferiore dell'articolo. 

I commenti e i suggerimenti ci consentono di migliorare la qualità della documentazione pubblicata. 

