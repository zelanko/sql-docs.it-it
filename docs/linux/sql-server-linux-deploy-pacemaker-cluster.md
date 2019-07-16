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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077468"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Distribuire un cluster Pacemaker per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questa esercitazione illustra le attività necessarie per distribuire un cluster Pacemaker di Linux per una [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] gruppo disponibilità Always On (AG) o istanza del cluster di failover (FCI). A differenza dei Server Windows fortemente accoppiato / [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] stack, la creazione del cluster Pacemaker, nonché configurazione del gruppo (AG) di disponibilità in Linux può essere eseguita prima o dopo l'installazione di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Dopo aver configurato il cluster, viene eseguita l'integrazione e la configurazione delle risorse per la parte di Pacemaker di una distribuzione del gruppo di disponibilità o FCI.
> [!IMPORTANT]
> Un gruppo di disponibilità con un tipo di cluster None viene *non* richiedono un cluster Pacemaker, né possono essere gestito da Pacemaker. 

> [!div class="checklist"]
> * Installare il componente aggiuntivo disponibilità elevata e Pacemaker.
> * Preparare i nodi per Pacemaker (RHEL e soltanto Ubuntu).
> * Creare il cluster Pacemaker.
> * Installare i pacchetti di SQL Server a disponibilità elevata e SQL Server Agent.
 
## <a name="prerequisite"></a>Prerequisiti
[Installare SQL Server 2017](sql-server-linux-setup.md).

## <a name="install-the-high-availability-add-on"></a>Installare il componente aggiuntivo disponibilità elevata
Usare la sintassi seguente per installare i pacchetti che costituiscono il componente aggiuntivo disponibilità elevata (HA) per ogni distribuzione di Linux. 

**Red Hat Enterprise Linux (RHEL)**
1.  Registrare il server usando la sintassi seguente. Viene chiesto di immettere un nome utente valido e una password.
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  Elencare i pool disponibili per la registrazione.
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  Eseguire il comando seguente per associare un'elevata disponibilità RHEL con la sottoscrizione
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    in cui *PoolId* è l'ID del pool per la sottoscrizione di disponibilità elevata nel passaggio precedente.
    
4.  Abilitare il repository per poter utilizzare il componente aggiuntivo disponibilità elevata.
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Installa Pacemaker.
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

Installare il modello di disponibilità elevata in YaST o eseguire operazioni come parte dell'installazione del server principale. L'installazione può essere eseguita con un ISO o DVD come origine o recuperandolo online.
> [!NOTE]
> In SLES, il componente aggiuntivo a disponibilità elevata verrà inizializzato quando viene creato il cluster.

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Preparare i nodi per Pacemaker (RHEL e soltanto Ubuntu)
Pacemaker Usa un utente creato nella distribuzione denominata *hacluster*. L'utente viene creata quando viene installato il componente aggiuntivo a disponibilità elevata in Ubuntu e RHEL.
1. In ogni server che fungerà da un nodo del cluster Pacemaker, creare la password di un utente può essere usato dal cluster. Il nome usato negli esempi viene *hacluster*, ma è possibile utilizzare qualsiasi nome. Il nome e la password deve essere lo stesso in tutti i nodi che fanno parte del cluster Pacemaker.
   
    ```bash
    sudo passwd hacluster
    ```
    
2. In ogni nodo che farà parte del cluster Pacemaker, abilitare e avviare il `pcsd` servizio con i comandi seguenti (RHEL e Ubuntu):

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   Eseguire quindi
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   Per garantire che `pcsd` viene avviato.
3. Abilitare il servizio Pacemaker in ogni nodo del cluster Pacemaker possibili.
   
   ```bash
   sudo systemctl start pacemaker
   ```

   In Ubuntu, viene visualizzato un errore:
   
   *pacemaker di avvio predefinita non contiene nessun runlevels, l'interruzione.*
   
   Questo errore è un problema noto. Nonostante l'errore, abilitare il servizio Pacemaker ha esito positivo e questo bug verrà corretto in un determinato momento nel futuro.
   
4. Successivamente, creare e avviare il cluster Pacemaker. C'è una differenza tra Ubuntu e RHEL in questo passaggio. Mentre in entrambe le distribuzioni, installando `pcs` consente di configurare un file di configurazione predefinito per il cluster, Pacemaker in RHEL, eseguire questo comando Elimina una configurazione esistente e crea un nuovo cluster.

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>Creare il cluster Pacemaker 
Questa sezione illustra come creare e configurare il cluster per ogni distribuzione di Linux.

**RHEL**

1. Autorizzare i nodi
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 ... NodeN> -u hacluster
   ```
   
   in cui *NodeX* è il nome del nodo.
2. Creare il cluster
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   in cui *PMClusterName* è il nome assegnato al cluster Pacemaker e *Nodelist* è riportato l'elenco di nomi dei nodi separati da uno spazio.

**Ubuntu**

Configurazione di Ubuntu è simile a RHEL. Tuttavia, è un'importante differenza: installazione dei pacchetti Pacemaker crea una configurazione di base per il cluster e attiva e avvia `pcsd`. Se si prova a configurare il cluster Pacemaker, seguendo le istruzioni di RHEL esattamente, viene visualizzato un errore. Per risolvere questo problema, procedere come segue: 
1. Rimuovere la configurazione di Pacemaker predefinita da ogni nodo.
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. Seguire i passaggi nella sezione relativa a RHEL per la creazione del cluster Pacemaker.

**SLES**

Il processo per la creazione di un cluster Pacemaker è completamente diverso in SLES, piuttosto che su Ubuntu e RHEL. I passaggi seguenti documentano come creare un cluster con SLES.
1. Avviare il processo di configurazione cluster eseguendo 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   in uno dei nodi. Potrebbe essere richiesto che NTP non è configurato e che non viene trovata alcuna periferica watchdog. Va bene per operazioni di tutto. Watchdog è correlato a STONITH se si usa l'isolamento predefinito di SLES che è basato sull'archiviazione. NTP e i watchdog possono essere configurati in un secondo momento.
   
2. Viene chiesto di configurare Corosync. Viene richiesto per l'indirizzo di rete da associare, nonché l'indirizzo multicast e la porta. L'indirizzo di rete è la subnet che si sta utilizzando; ad esempio, 192.191.190.0. È possibile accettare le impostazioni predefinite in ogni prompt, o se necessario, modificarle.
   
3. Successivamente, viene chiesto se si desidera configurare SBD, ovvero l'isolamento basato su disco. Questa configurazione può essere eseguita in un secondo momento se necessario. Se non SBD è configurata, a differenza di su Ubuntu e RHEL `stonith-enabled` per impostazione predefinita sarà essere impostato su false.
   
4. Infine, viene chiesto se si desidera configurare un indirizzo IP per l'amministrazione. Questo indirizzo IP è facoltativo, ma funzionalità simile per l'indirizzo IP per un cluster di failover di Windows Server (WSFC) nel senso che viene creato un indirizzo IP del cluster da utilizzare per la connessione ad esso tramite a disponibilità elevata Web Konsole (HAWK). Anche questa configurazione, è facoltativa.
   
5. Assicurarsi che il cluster sia attivo e in esecuzione eseguendo 
   ```bash
   sudo crm status
   ```
   
6. Modifica il *hacluster* password con 
   ```bash
   sudo passwd hacluster
   ```
   
7. Se è stato configurato un indirizzo IP per l'amministrazione, è possibile eseguirne il test in un browser, che consente anche di testare la modifica della password per *hacluster*.
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. In un altro server SLES che sarà un nodo del cluster, eseguire 
   ```bash
   sudo ha-cluster-join
   ```
   
9. Quando richiesto, immettere il nome o indirizzo IP del server in cui è stato configurato come primo nodo del cluster nei passaggi precedenti. Il server viene aggiunto come nodo al cluster esistente.
   
10. Verificare che il nodo sia stato aggiunto tramite l'esecuzione 
   ```bash
   sudo crm status
   ```
   
11. Modifica il *hacluster* password con 
   ```bash
   sudo passwd hacluster
   ```
   
12. Ripetere i passaggi da 8 a 11 per tutti gli altri server da aggiungere al cluster.

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>Installare i pacchetti di SQL Server a disponibilità elevata e SQL Server Agent
Usare i comandi seguenti per installare il pacchetto SQL Server a disponibilità elevata e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente, se non sono già installati. Installazione del pacchetto a disponibilità elevata dopo l'installazione [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] richiede il riavvio del [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] per poter essere utilizzato. Queste istruzioni presuppongono che i repository per i pacchetti Microsoft sono già stati configurati, poiché [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] devono essere installati a questo punto.
> [!NOTE]
> - Se non userà [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent per il log shipping o qualsiasi altro utilizzo, non deve essere installato, pertanto il pacchetto *mssql-server-agent* può essere ignorato.
> - Gli altri pacchetti facoltativi per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] ricerca Full-Text (*mssql-server-fts*) e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-è*), non sono obbligatorio per la disponibilità elevata, per un'istanza FCI o un gruppo di disponibilità.

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

In questa esercitazione è stato descritto come distribuire un cluster Pacemaker per SQL Server in Linux. Si è appreso come a:
> [!div class="checklist"]
> * Installare il componente aggiuntivo disponibilità elevata e Pacemaker.
> * Preparare i nodi per Pacemaker (RHEL e soltanto Ubuntu).
> * Creare il cluster Pacemaker.
> * Installare i pacchetti di SQL Server a disponibilità elevata e SQL Server Agent.

Per creare e configurare un gruppo di disponibilità per SQL Server in Linux, vedere:

> [!div class="nextstepaction"]
> [Creare e configurare un gruppo di disponibilità per SQL Server in Linux](sql-server-linux-create-availability-group.md).

