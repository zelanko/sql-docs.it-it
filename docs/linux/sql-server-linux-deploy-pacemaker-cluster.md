---
title: Distribuire un cluster Pacemaker per SQL Server in Linux
description: Questa esercitazione illustra come distribuire un cluster Pacemaker per SQL Server in Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/11/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ee3b4aac2e1bcdcc37de17a569f080d3b9bc87cc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68077468"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Distribuire un cluster Pacemaker per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questa esercitazione illustra le attività necessarie per distribuire un cluster Pacemaker in Linux per un gruppo di disponibilità Always On o un'istanza del cluster di failover di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Diversamente da quanto avviene per lo stack Windows Server/[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] strettamente associato, la creazione di un cluster Pacemaker e la configurazione di un gruppo di disponibilità in Linux possono essere eseguite prima o dopo l'installazione di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. L'integrazione e la configurazione delle risorse per la parte Pacemaker di una distribuzione di un gruppo di disponibilità o di un'istanza del cluster di failover vengono eseguite dopo la configurazione del cluster.
> [!IMPORTANT]
> Un gruppo di disponibilità con un cluster di tipo None *non* richiede un cluster Pacemaker né può essere gestito da Pacemaker. 

> [!div class="checklist"]
> * Installare il componente aggiuntivo per la disponibilità elevata e installare Pacemaker.
> * Preparare i nodi per Pacemaker (solo RHEL e Ubuntu).
> * Creare il cluster Pacemaker.
> * Installare i pacchetti per la disponibilità elevata di SQL Server e SQL Server Agent.
 
## <a name="prerequisite"></a>Prerequisito
[Installare SQL Server 2017](sql-server-linux-setup.md).

## <a name="install-the-high-availability-add-on"></a>Installare il componente aggiuntivo per la disponibilità elevata
Usare la sintassi seguente per installare i pacchetti che costituiscono il componente aggiuntivo per la disponibilità elevata per ogni distribuzione di Linux. 

**Red Hat Enterprise Linux (RHEL)**
1.  Registrare il server usando la sintassi seguente. Viene richiesto di specificare un nome utente e una password validi.
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  Elencare i pool disponibili per la registrazione.
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  Eseguire il comando seguente per associare la disponibilità elevata di RHEL alla sottoscrizione
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    dove *PoolId* è l'ID del pool per la sottoscrizione della disponibilità elevata del passaggio precedente.
    
4.  Abilitare il repository per poter usare il componente aggiuntivo per la disponibilità elevata.
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Installare Pacemaker.
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

Installare il modello di disponibilità elevata in YaST o eseguire questa operazione durante l'installazione principale del server. L'installazione può essere eseguita usando un file ISO o un DVD come origine oppure online.
> [!NOTE]
> In SLES il componente aggiuntivo per la disponibilità elevata viene inizializzato al momento della creazione del cluster.

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Preparare i nodi per Pacemaker (solo RHEL e Ubuntu)
Pacemaker stesso usa un utente creato durante la distribuzione, denominato *hacluster*. L'utente viene creato quando il componente aggiuntivo per la disponibilità elevata è installato in RHEL e Ubuntu.
1. In ogni server che fungerà da nodo del cluster Pacemaker creare la password per un utente che verrà usato dal cluster. Il nome usato negli esempi è *hacluster*, ma è possibile usare qualsiasi nome. Il nome e la password devono essere gli stessi in tutti i nodi che fanno parte del cluster Pacemaker.
   
    ```bash
    sudo passwd hacluster
    ```
    
2. In ogni nodo che farà parte del cluster Pacemaker abilitare e avviare il servizio `pcsd` con i comandi seguenti (RHEL e Ubuntu):

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   Eseguire quindi
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   per assicurarsi che `pcsd` venga avviato.
3. Abilitare il servizio Pacemaker in ogni nodo possibile del cluster Pacemaker.
   
   ```bash
   sudo systemctl start pacemaker
   ```

   In Ubuntu viene visualizzato un errore:
   
   *pacemaker Default-Start contains no runlevels, aborting.* (L'avvio predefinito di Pacemaker non contiene livelli di esecuzione. Interruzione in corso.).
   
   Questo è un errore noto. Nonostante l'errore, l'abilitazione del servizio Pacemaker ha esito positivo e questo bug verrà risolto in futuro.
   
4. Successivamente, creare e avviare il cluster Pacemaker. In questa fase esiste una differenza tra RHEL e Ubuntu. Anche se in entrambe le distribuzioni l'installazione di `pcs` configura un file di configurazione predefinito per il cluster Pacemaker, in RHEL l'esecuzione di questo comando elimina definitivamente qualsiasi configurazione esistente e crea un nuovo cluster.

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>Creare il cluster Pacemaker 
Questa sezione illustra come creare e configurare il cluster per ogni distribuzione di Linux.

**RHEL**

1. Autorizzare i nodi
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 ... NodeN> -u hacluster
   ```
   
   dove *NodeX* è il nome del nodo.
2. Creare il cluster
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   dove *PMClusterName* è il nome assegnato al cluster Pacemaker e *Nodelist* è l'elenco di nomi dei nodi separati da uno spazio.

**Ubuntu**

La configurazione di Ubuntu è simile a quella di RHEL. Esiste tuttavia un'importante differenza: l'installazione dei pacchetti di Pacemaker crea una configurazione di base per il cluster e abilita e avvia `pcsd`. Se si prova a configurare il cluster Pacemaker seguendo esattamente le istruzioni per RHEL, si verifica un errore. Per risolvere il problema, seguire questa procedura: 
1. Rimuovere la configurazione di Pacemaker predefinita da ogni nodo.
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. Seguire i passaggi nella sezione RHEL per la creazione del cluster pacemaker.

**SLES**

Il processo per la creazione di un cluster Pacemaker è completamente diverso in SLES rispetto a RHEL e Ubuntu. I passaggi seguenti illustrano come creare un cluster con SLES.
1. Avviare il processo di configurazione del cluster eseguendo 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   in uno dei nodi. È possibile che venga richiesto che NTP non sia configurato e che non siano presenti dispositivi watchdog. In questo modo non si verificheranno problemi. Il watchdog è correlato a STONITH se si usa l'isolamento predefinito di SLES, che è basato sulla risorsa di archiviazione. È possibile configurare NTP e il watchdog in un secondo momento.
   
2. Viene richiesto di configurare Corosync. Viene chiesto l'indirizzo di rete a cui eseguire l'associazione, nonché l'indirizzo multicast e la porta. L'indirizzo di rete è la subnet usata, ad esempio 192.191.190.0. È possibile accettare le impostazioni predefinite a ogni prompt o modificarle se necessario.
   
3. Viene quindi chiesto se si vuole configurare SBD, ovvero l'isolamento basato su disco. Questa configurazione può essere eseguita in un secondo momento, se necessario. Se SBD non viene configurato, diversamente da quanto avviene per RHEL e Ubuntu, `stonith-enabled` verrà impostato sul valore predefinito false.
   
4. Viene infine chiesto se si vuole configurare un indirizzo IP per l'amministrazione. Questo indirizzo IP è facoltativo, ma funziona in modo simile all'indirizzo IP per un cluster WSFC (Windows Server Failover Cluster) perché crea un indirizzo IP nel cluster da usare per la connessione tramite HAWK (HA Web Konsole). Anche questa configurazione è facoltativa.
   
5. Verificare che il cluster sia operativo eseguendo 
   ```bash
   sudo crm status
   ```
   
6. Cambiare la password *hacluster* con 
   ```bash
   sudo passwd hacluster
   ```
   
7. Se è stato configurato un indirizzo IP per l'amministrazione, è possibile testarlo in un browser. In questo modo viene testata anche la modifica della password per *hacluster*.
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. In un altro server SLES che sarà un nodo del cluster eseguire 
   ```bash
   sudo ha-cluster-join
   ```
   
9. Quando richiesto, immettere il nome o l'indirizzo IP del server configurato come primo nodo del cluster nei passaggi precedenti. Il server viene aggiunto come nodo al cluster esistente.
   
10. Verificare che il nodo sia stato aggiunto eseguendo 
   ```bash
   sudo crm status
   ```
   
11. Cambiare la password *hacluster* con 
   ```bash
   sudo passwd hacluster
   ```
   
12. Ripetere i passaggi da 8 a 11 per tutti gli altri server da aggiungere al cluster.

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>Installare i pacchetti per la disponibilità elevata di SQL Server e SQL Server Agent
Usare i comandi seguenti per installare il pacchetto per la disponibilità elevata di SQL Server e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent, se non sono già installati. L'installazione del pacchetto per la disponibilità elevata dopo l'installazione di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] richiede un riavvio di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in modo che sia possibile usarlo. Queste istruzioni presuppongono che i repository per i pacchetti Microsoft siano già stati configurati, perché [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] deve essere installato ora.
> [!NOTE]
> - Se non si userà [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent per il log shipping o per altro, non è necessario installarlo, quindi il pacchetto *mssql-server-agent* può essere ignorato.
> - Gli altri pacchetti facoltativi per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux, Ricerca full-text di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] (*mssql-server-fts*) e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-is*), non sono obbligatori per la disponibilità elevata, sia per un'istanza del cluster di failover che per un gruppo di disponibilità.

**RHEL**

```bash
sudo yum install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**Ubuntu**

```bash
sudo apt-get install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**SLES**

```bash
sudo zypper install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

## <a name="next-steps"></a>Passaggi successivi

Questa esercitazione ha illustrato come distribuire un cluster Pacemaker per SQL Server in Linux. Si è appreso come:
> [!div class="checklist"]
> * Installare il componente aggiuntivo per la disponibilità elevata e installare Pacemaker.
> * Preparare i nodi per Pacemaker (solo RHEL e Ubuntu).
> * Creare il cluster Pacemaker.
> * Installare i pacchetti per la disponibilità elevata di SQL Server e SQL Server Agent.

Per creare e configurare un gruppo di disponibilità per SQL Server in Linux, vedere:

> [!div class="nextstepaction"]
> [Creare e configurare un gruppo di disponibilità per SQL Server in Linux](sql-server-linux-create-availability-group.md).

