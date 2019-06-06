---
title: Creare e configurare un gruppo di disponibilità per SQL Server in Linux | Microsoft Docs
description: Questa esercitazione illustra come creare e configurare i gruppi di disponibilità per SQL Server in Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 06/28/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 1841b7e38e47ffa1192b19564e1c6596ea9804a3
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719385"
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>Creare e configurare un gruppo di disponibilità per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questa esercitazione illustra come creare e configurare un gruppo di disponibilità (AG) per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux. A differenza di [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] e in precedenza su Windows, è possibile abilitare gruppi di disponibilità con o senza la creazione del cluster Pacemaker sottostante prima di tutto. Integrazione con il cluster, se necessario, non viene eseguita fino alla versione successiva.

L'esercitazione include le attività seguenti:
 
> [!div class="checklist"]
> * Abilitare gruppi di disponibilità.
> * Creare i certificati e gli endpoint di gruppo di disponibilità.
> * Usare [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) o Transact-SQL per creare un gruppo di disponibilità.
> * Creare il [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] account di accesso e le autorizzazioni per Pacemaker.
> * Creare la disponibilità del gruppo di risorse in un cluster Pacemaker (solo per il tipo esterno).

## <a name="prerequisite"></a>Prerequisiti
- Distribuire il cluster a disponibilità elevata Pacemaker, come descritto in [distribuire un cluster Pacemaker per SQL Server in Linux](sql-server-linux-deploy-pacemaker-cluster.md).


## <a name="enable-the-availability-groups-feature"></a>Abilitare la funzionalità gruppi di disponibilità

A differenza di su Windows, è possibile usare PowerShell o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] funzionalità (AG) di gruppi di Configuration Manager per abilitare la disponibilità. In Linux, è necessario usare `mssql-conf` per abilitare la funzionalità. Esistono due modi per abilitare la funzionalità gruppi di disponibilità: usare la `mssql-conf` utilità oppure modificare il `mssql.conf` file manualmente.

> [!IMPORTANT]
> La funzionalità gruppo di disponibilità deve essere abilitata per le repliche di sola configurazione, anche in [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)].

### <a name="use-the-mssql-conf-utility"></a>Usare l'utilità mssql-conf

Prompt dei comandi, eseguire quanto segue:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>Modificare il file mssql.conf

È inoltre possibile modificare il `mssql.conf` file, che si trova sotto il `/var/opt/mssql` cartella, aggiungere le righe seguenti:

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-includessnoversion-mdincludesssnoversion-mdmd"></a>Riavvio [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Dopo aver abilitato gruppi di disponibilità, come in Windows, è necessario riavviare [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Che può essere eseguita nel modo seguente:

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>Creare l'endpoint di gruppo di disponibilità e certificati

Un gruppo di disponibilità Usa endpoint TCP per la comunicazione. In Linux, gli endpoint per un gruppo di disponibilità sono supportati solo se si usano certificati per l'autenticazione. Ciò significa che il certificato da un'istanza deve essere ripristinato in tutte le altre istanze che saranno le repliche nello stesso gruppo di disponibilità. Il processo dei certificati è necessario anche per una replica di sola configurazione. 

Creazione di endpoint e il ripristino dei certificati possono essere eseguite solo tramite Transact-SQL. È possibile utilizzare non [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-anche i certificati generati. È necessario anche un processo per gestire e sostituire i certificati che scadono.

> [!IMPORTANT]
> Se si prevede di usare il [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] procedura guidata per creare il gruppo di disponibilità, è comunque necessario creare e ripristinare i certificati tramite Transact-SQL in Linux.

Per la sintassi completa le opzioni disponibili per i vari comandi (ad esempio aggiuntiva di sicurezza), consultare:

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [CREARE CERTIFICATI](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> Anche se verrà creato un gruppo di disponibilità, viene utilizzato il tipo di endpoint *FOR DATABASE_MIRRORING*, perché alcuni aspetti sottostante una volta sono stati condivisi con tale funzionalità attualmente deprecata.

In questo esempio creerà i certificati per una configurazione a tre nodi. I nomi delle istanze sono LinAGN1 LinAGN2 e LinAGN3.

1.  Eseguire le operazioni seguenti sul LinAGN1 per creare la chiave master, un certificato e un endpoint, nonché eseguire il backup del certificato. In questo esempio viene utilizzata la tipica porta TCP 5022 per l'endpoint.
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN1_Cert
    WITH SUBJECT = 'LinAGN1 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN1_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN1_Cert,
        ROLE = ALL);
    
    GO
    ```
    
2.  Eseguire la stessa operazione nel LinAGN2:
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    WITH SUBJECT = 'LinAGN2 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN2_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN2_Cert,
        ROLE = ALL);
    
    GO
    ```
    
3.  Infine, seguire la stessa sequenza in LinAGN3:
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    WITH SUBJECT = 'LinAGN3 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN3_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN3_Cert,
        ROLE = ALL);
    
    GO
    ```
    
4.  Usando `scp` o un'altra utilità, copiare i backup del certificato in ogni nodo che farà parte del gruppo di disponibilità.
    
    In questo esempio:
    
    - Copiare LinAGN1_Cert.cer LinAGN2 e LinAGN3
    - Copiare LinAGN2_Cert.cer LinAGN1 e LinAGN3.
    - Copiare LinAGN3_Cert.cer LinAGN1 e LinAGN2.
    
5.  Modificare la proprietà e il gruppo associato il file del certificato copiato a `mssql`.
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  Creare account di accesso a livello di istanza e gli utenti associati a LinAGN2 e LinAGN3 su LinAGN1.
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  Ripristinare LinAGN2_Cert e LinAGN3_Cert su LinAGN1. I certificati delle altre repliche è un aspetto importante della sicurezza e la comunicazione del gruppo di disponibilità.
    
    ```SQL
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
8.  Grant the logins associated with LinAG2 and LinAGN3 permission to connect to the endpoint on LinAGN1.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
9.  Creare account di accesso a livello di istanza e gli utenti associati a LinAGN1 e LinAGN3 su LinAGN2.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10. Ripristinare LinAGN1_Cert e LinAGN3_Cert su LinAGN2.
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    ```
    
11. Concedere agli account di accesso associato LinAG1 e LinAGN3 dell'autorizzazione per connettersi all'endpoint in LinAGN2.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12. Creare account di accesso a livello di istanza e gli utenti associati a LinAGN1 e LinAGN2 su LinAGN3.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13. Ripristinare LinAGN1_Cert e LinAGN2_Cert su LinAGN3. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    ```
    
14. Concedere agli account di accesso associato LinAG1 e LinAGN2 dell'autorizzazione per connettersi all'endpoint in LinAGN3.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>Creare il gruppo di disponibilità

In questa sezione viene illustrato come utilizzare [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) o Transact-SQL per creare il gruppo di disponibilità per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>Utilizzare [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)].

Questa sezione illustra come creare un gruppo di disponibilità con un tipo di cluster External tramite SSMS con la creazione guidata gruppo di disponibilità.

1.  In SQL Server Management Studio, espandere **disponibilità elevata AlwaysOn**, fare clic destro **gruppi di disponibilità**e selezionare **Creazione guidata nuovo gruppo di disponibilità**.

2.  Nella finestra di dialogo Introduction, fare clic su **successivo**.

3.  Nella finestra di dialogo specificare le opzioni di gruppo di disponibilità, immettere un nome per il gruppo di disponibilità e selezionare un tipo di cluster di EXTERNAL o nessuno nell'elenco a discesa. Esterno deve essere usato quando Pacemaker verrà distribuito. Nessuno è per scenari specializzati, ad esempio lettura con scalabilità orizzontale. Se si seleziona l'opzione per il rilevamento dell'integrità a livello di database è facoltativa. Per altre informazioni su questa opzione, vedere [opzione failover di rilevamento dell'integrità a livello di disponibilità gruppo database](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md). Scegliere **Avanti**.

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  Nella finestra di dialogo Seleziona database, selezionare i database che faranno parte del gruppo di disponibilità. Ogni database deve avere un backup completo prima di aggiungerlo a un gruppo di disponibilità. Scegliere **Avanti**.

5.  Nella finestra di dialogo specifica repliche, fare clic su **Aggiungi Replica**.

6.  Nella finestra di dialogo Connetti al Server, immettere il nome dell'istanza di Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] che sarà la replica secondaria e le credenziali per connettersi. Fare clic su **Connetti**.

7.  Ripetere i due passaggi precedenti per l'istanza che conterrà una replica di sola configurazione o un'altra replica secondaria.

8.  Tutte le tre istanze dovrebbero ora essere elencate nella finestra di dialogo specifica repliche. Se si usa un tipo di cluster External, per la replica secondaria che sarà una replica secondaria true, assicurarsi che la modalità di disponibilità corrisponde a quello della replica primaria e la modalità di failover è impostata su External. Per la replica di sola configurazione, selezionare solo una modalità di disponibilità della configurazione.

    L'esempio seguente illustra un gruppo di disponibilità con due repliche, un tipo di cluster External e una replica di sola configurazione.

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    L'esempio seguente illustra un gruppo di disponibilità con due repliche, un tipo di cluster None, e una replica di sola configurazione.

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  Se si desidera modificare le preferenze di backup, fare clic sulla scheda Preferenze di Backup. Per altre informazioni sulle preferenze di backup con gruppi di disponibilità, vedere [configurare il backup su repliche di disponibilità](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).

10. Se con database secondari leggibili o la creazione di un gruppo di disponibilità con un cluster di tipo None per scalabilità in lettura, è possibile creare un listener selezionando la scheda Listener. Inoltre è possibile aggiungere un listener in un secondo momento. Per creare un listener, scegliere l'opzione **creare un listener del gruppo di disponibilità** e immettere un nome e una porta TCP/IP se si desidera utilizzare un indirizzo IP DHCP statico o assegnato automaticamente. Tenere presente che per un gruppo di disponibilità con un tipo di cluster None, l'indirizzo IP deve essere statico e impostare all'indirizzo IP della replica primaria.

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. Se viene creato un listener per gli scenari leggibili, SQL Server Management Studio 17.3 o successiva consente di creare il routing in sola lettura nella procedura guidata. Può anche essere aggiunto in un secondo momento tramite SSMS o Transact-SQL. Per aggiungere routing ora di sola lettura:

    a.  Selezionare la scheda di Routing di sola lettura.

    b.  Immettere l'URL per le repliche di sola lettura. Questi URL sono simili agli endpoint, ad eccezione del fatto che usa la porta dell'istanza, non l'endpoint.

    c.  Selezionare ogni URL e dal basso, selezionare le repliche leggibili. Per la selezione multipla, tenere premuto MAIUSC o fare clic e trascinare.

12. Scegliere **Avanti**.

13. Scegli modalità di inizializzazione nelle repliche secondarie. L'impostazione predefinita consiste nell'usare [il seeding automatico](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md), che richiede lo stesso percorso in tutti i server che fanno parte del gruppo di disponibilità. È anche possibile la procedura guidata eseguire una backup, copia e ripristino (la seconda opzione); aggiungerlo se hanno manualmente il backup, copiata e ripristinato il database nelle repliche (terza opzione); o aggiungere il database in un secondo momento (ultima opzione). Come con i certificati, se si apportano i backup e copiarli manualmente, le autorizzazioni per i file di backup deve essere impostato nelle altre repliche. Scegliere **Avanti**.

14. Nella finestra di dialogo convalida, se tutti gli elementi non arrivi come esito positivo, provare a utilizzare. Alcuni avvisi siano accettabili e non irreversibili, ad esempio se non si crea un listener. Scegliere **Avanti**.

15. Nella finestra di dialogo riepilogo, fare clic su **fine**. A questo punto verrà avviata la procedura per creare il gruppo di disponibilità.

16. Una volta completata la creazione del gruppo di disponibilità, fare clic su **Chiudi** sui risultati. È ora possibile visualizzare il gruppo di disponibilità nelle repliche nelle viste a gestione dinamica, nonché nella cartella disponibilità elevata Always On in SQL Server Management Studio.

### <a name="use-transact-sql"></a>Usare Transact-SQL

In questa sezione vengono illustrati esempi di creazione di un gruppo di disponibilità con Transact-SQL. Il listener e routing di sola lettura può essere configurati dopo aver creato il gruppo di disponibilità. Il gruppo di disponibilità può essere modificato con `ALTER AVAILABILITY GROUP`, ma la modifica del tipo di cluster non può essere eseguita [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Se non si intendeva creare un gruppo di disponibilità con un tipo di cluster External, è necessario eliminarla e ricrearla con un tipo di cluster None. Altre informazioni e altre opzioni sono disponibili ai collegamenti seguenti:

-   [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [Configurare il Routing di sola lettura per un gruppo di disponibilità (SQL Server)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [Creare o configurare un listener del gruppo di disponibilità (SQL Server)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one---two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>Repliche di esempio uno-due con una sola configurazione replica (tipo di cluster esterna)

In questo esempio viene illustrato come creare un gruppo di disponibilità con due repliche che usa una replica di sola configurazione.

1.  Eseguire sul nodo che sarà la replica primaria che contiene la copia di lettura/scrittura completa dei database. Questo esempio viene usato il seeding automatico.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1' WITH (
       ENDPOINT_URL = N' TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       SEEDING_MODE = AUTOMATIC),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       AVAILABILITY_MODE = CONFIGURATION_ONLY);
       
    GO
    ```
    
2.  Nella finestra di query connessa a altra replica, eseguire il comando seguente per creare un join della replica al gruppo di disponibilità e avviare il processo di seeding dalla replica primaria alla replica secondaria.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3. Nella finestra di query connessa alla replica di sola configurazione, creare un join al gruppo di disponibilità.
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two---three-replicas-with-read-only-routing-external-cluster-type"></a>Repliche di esempio due-tre con il routing di sola lettura (tipo di cluster esterna)

Questo esempio mostra tre completa le repliche e la modalità sola lettura e routing possono essere configurati come parte della creazione iniziale del gruppo di disponibilità.

1.  Eseguire sul nodo che sarà la replica primaria che contiene la copia di lettura/scrittura completa dei database. Questo esempio viene usato il seeding automatico.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN2.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:1433')),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN2.FullyQualified.Name:1433')),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN3.FullyQualified.Name:1433'))
    LISTENER '<ListenerName>' (WITH IP = ('<IPAddress>', '<SubnetMask>'), Port = 1433);
    
    GO
    ```
    
    Alcuni aspetti da considerare questa configurazione:
    
    - *AGName* è il nome del gruppo di disponibilità.
    - *DBName* è il nome del database che verrà usato con il gruppo di disponibilità. Può anche essere un elenco di nomi separati da virgole.
    - *ListenerName* è un nome diverso da quello di uno dei nodi del server sottostanti. Si sarà registrato in DNS insieme a *IPAddress*.
    - *IPAddress* è un indirizzo IP associato *ListenerName*. È inoltre univoco e non uguale a uno dei nodi del server /. Le applicazioni e gli utenti finali useranno entrambi *ListenerName* oppure *IPAddress* per connettersi al gruppo di disponibilità.
    - *Subnet mask* è la subnet mask *IPAddress*, ad esempio 255.255.255.0.

2.  Nella finestra di query connessa a altra replica, eseguire il comando seguente per creare un join della replica al gruppo di disponibilità e avviare il processo di seeding dalla replica primaria alla replica secondaria.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  Ripetere il passaggio 2 per la replica di terza.

#### <a name="example-three---two-replicas-with-read-only-routing-none-cluster-type"></a>Repliche di esempio due di tre con sola lettura di routing (nessuno tipo di cluster)

In questo esempio viene illustrata la creazione di una configurazione con due repliche utilizzando un tipo di cluster None. Viene usato per lo scenario di scalabilità in lettura in cui non è previsto alcun failover. Verrà creato il listener che è effettivamente la replica primaria, nonché di sola lettura il routing, usando la funzionalità round robin.

1.  Eseguire sul nodo che sarà la replica primaria che contiene la copia di lettura/scrittura completa dei database. Questo esempio viene usato il seeding automatico.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = NONE)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name: <PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name'.'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:<PortOfInstance>'));
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:<PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL =N'TCP://LinAGN2.FullyQualified.Name:<PortOfInstance>'));
    LISTENER '<ListenerName>' (WITH IP = ('<PrimaryReplicaIPAddress>', '<SubnetMask>'), Port = <PortOfListener>);
    
    GO
    ```
    
    Where
    - *AGName* è il nome del gruppo di disponibilità.
    - *DBName* è il nome del database che verrà usato con il gruppo di disponibilità. Può anche essere un elenco di nomi separati da virgole.
    - *PortOfEndpoint* è il numero di porta utilizzato dall'endpoint creato.
    - *PortOfInstance* è il numero di porta utilizzato dall'istanza di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].
    - *ListenerName* è un nome che è diverso da quello di qualsiasi delle repliche sottostante, ma non verrà effettivamente usato.
    - *PrimaryReplicaIPAddress* è l'indirizzo IP della replica primaria.
    - *Subnet mask* è la subnet mask *IPAddress*. Ad esempio 255.255.255.0.
    
2.  Partecipa alla replica secondaria al gruppo di disponibilità e avviare il seeding automatico.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>Creare il [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] account di accesso e le autorizzazioni per Pacemaker

Un cluster Pacemaker di elevata disponibilità sottostante [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux deve accedere al [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] istanza, nonché le autorizzazioni nel gruppo di disponibilità se stesso. Questi passaggi creano account di accesso e le autorizzazioni associate, oltre a un file che viene descritto come accedere a Pacemaker [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

1.  Nella finestra di query connessa alla prima replica, eseguire quanto segue:

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD ='<StrongPassword>';
    
    GO
    
    GRANT VIEW SERVER STATE TO PMLogin;
    
    GO
    
    GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::<AGThatWasCreated> TO PMLogin;
    
    GO
    ```
    
2.  Nel nodo 1, immettere il comando 
    ```bash
    sudo emacs /var/opt/mssql/secrets/passwd
    ```
    
    Si aprirà l'editor Emacs.
    
3.  Nell'editor, immettere le due righe seguenti:

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  Tenere premuto il tasto CTRL e quindi premere X, quindi C, per chiuderla e salvare il file.

5.  Execute 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    Per bloccare il file.

6.  Ripetere i passaggi 1-5 negli altri server che fungerà da repliche.

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>Creare la disponibilità del gruppo di risorse del cluster Pacemaker (solo esterno)

Dopo una data di disponibilità gruppo viene creato in [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], le risorse corrispondenti devono essere create in Pacemaker, se viene specificato un tipo di cluster External. Esistono due risorse associate a un gruppo di disponibilità: il gruppo di disponibilità e un indirizzo IP. Configurare la risorsa indirizzo IP è facoltativo se non si usa la funzionalità di listener, ma è consigliato.

La risorsa del gruppo di disponibilità creato è un tipo speciale di risorsa denominata un clone. La risorsa del gruppo di disponibilità ha essenzialmente le copie in ogni nodo e vi è una risorsa di controllo denominata master. Lo schema è associato con il server che ospita la replica primaria. Le repliche secondarie (normale o di sola configurazione) vengono considerate gli slave e può essere promosso al master in un failover.

1.  Creare la risorsa del gruppo di disponibilità con la sintassi seguente:

    **Ubuntu e Red Hat Enterprise Linux (RHEL)**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failure-timeout=30s --master meta notify=true
    ```

    >[!NOTE]
    >In RHEL 7.4, è possibile riscontrare un avviso con l'uso di - master. Per evitare questo problema, usare `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failover-timeout=30s master notify=true`
   
    **SUSE Linux Enterprise Server (SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
    meta failure-timeout=60s \
    op start timeout=60s \
    op stop timeout=60s \
    op promote timeout=60s \
    op demote timeout=10s \
    op monitor timeout=60s interval=10s \
    op monitor timeout=60s interval=11s role="Master" \
    op monitor timeout=60s interval=12s role="Slave" \
    op notify timeout=60s
    ms ms-ag_cluster <NameForAGResource> \
    meta master-max="1" master-node-max="1" clone-max="3" \
    clone-node-max="1" notify="true" \
    commit
    ```
    
    in cui *NameForAGResource* è il nome univoco assegnato a questa risorsa cluster per il gruppo di disponibilità, e *AGName* è il nome del gruppo di disponibilità che è stato creato.
 
2.  Creare la risorsa indirizzo IP per il gruppo di disponibilità che verrà associato alla funzionalità di listener.

    **Ubuntu e RHEL**
    
    ```bash
    sudo pcs resource create <NameForIPResource> ocf:heartbeat:IPaddr2 ip=<IPAddress> cidr_netmask=<Netmask>
    ```

    **SLES**
    
    ```bash
    crm configure \
    primitive <NameForIPResource> \
       ocf:heartbeat:IPaddr2 \
       params ip=<IPAddress> \
          cidr_netmask=<Netmask>
    ```
    
    in cui *NameForIPResource* è il nome univoco per la risorsa IP, e *IPAddress* è l'indirizzo IP statico assegnato alla risorsa. In SLES, devi anche specificare la subnet mask. Ad esempio, 255.255.255.0 avrebbe un valore pari a 24 per *subnet mask.*
    
3.  Per assicurarsi che l'indirizzo IP e la risorsa del gruppo di disponibilità sono in esecuzione nello stesso nodo, è necessario configurare un vincolo con più sedi.

    **Ubuntu e RHEL**
    
    ```bash
    sudo pcs constraint colocation add <NameForIPResource> <NameForAGResource>-master INFINITY with-rsc-role=Master
    ```

    **SLES**
    
    ```bash
    crm configure <NameForConstraint> inf: \
    <NameForIPResource> <NameForAGResource>:Master 
    commit
    ```
    
    in cui *NameForIPResource* è il nome per una risorsa IP *NameForAGResource* è il nome della risorsa del gruppo di disponibilità e in SLES, *NameForConstraint* è il nome per il vincolo.

4.  Creare un vincolo per assicurarsi che la risorsa del gruppo di disponibilità sia attivo e in esecuzione prima dell'indirizzo IP. Mentre il vincolo di condivisione percorso implica un vincolo di ordinamento, questo applica.

    **Ubuntu e RHEL**
    
    ```bash
    sudo pcs constraint order promote <NameForAGResource>-master then start <NameForIPResource>
    ```
    
    **SLES**
    
    ```bash
    crm configure \
    order <NameForConstraint> inf: <NameForAGResource>:promote <NameForIPResource>:start
    commit
    ```
    
    in cui *NameForIPResource* è il nome per una risorsa IP *NameForAGResource* è il nome della risorsa del gruppo di disponibilità e in SLES, *NameForConstraint* è il nome per il vincolo.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come creare e configurare un gruppo di disponibilità per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux. Si è appreso come a:
> [!div class="checklist"]
> * Abilitare gruppi di disponibilità.
> * Gli endpoint di creazione del gruppo di disponibilità e certificati.
> * Usare [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) o Transact-SQL per creare un gruppo di disponibilità.
> * Creare il [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] account di accesso e le autorizzazioni per Pacemaker.
> * Creare risorse del gruppo di disponibilità in un cluster Pacemaker.

Per la maggior parte delle attività di amministrazione del gruppo di disponibilità, tra cui gli aggiornamenti e il failover, vedere:

> [!div class="nextstepaction"]
> [Funzioni gruppo di disponibilità elevata per SQL Server in Linux](sql-server-linux-availability-group-failover-ha.md)

