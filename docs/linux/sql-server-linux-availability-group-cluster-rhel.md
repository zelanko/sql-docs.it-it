---
title: Configurare Cluster di RHEL per il gruppo di disponibilità di SQL Server
titleSuffix: SQL Server
description: Informazioni sui cluster di gruppo di disponibilità durante l'esecuzione di Red Hat Enterprise Linux (RHEL)
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/12/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.openlocfilehash: 44d39a44597a789c031ee10b862bffa2af6da883
ms.sourcegitcommit: 7d4a3fc0f2622cbc6930d792be4a9b3fcac4c4b6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2019
ms.locfileid: "58305630"
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>Configurare Cluster di RHEL per il gruppo di disponibilità di SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo documento illustra come creare un cluster del gruppo di disponibilità di tre nodi per SQL Server su Red Hat Enterprise Linux. Per la disponibilità elevata, un gruppo di disponibilità in Linux richiede tre nodi, vedere la [elevata disponibilità e protezione dei dati per le configurazioni di gruppo di disponibilità](sql-server-linux-availability-group-ha.md). Il livello di clustering si basa su Red Hat Enterprise Linux (RHEL) [componente aggiuntivo a disponibilità elevata](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) costruita basandosi su [Pacemaker](https://clusterlabs.org/). 

> [!NOTE] 
> Accesso alla documentazione completa di Red Hat richiede una sottoscrizione valida. 

Per altre informazioni su configurazione del cluster, le opzioni degli agenti delle risorse e gestione, visitare [documentazione di riferimento RHEL](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).

> [!NOTE] 
> SQL Server non è come strettamente integrato con Pacemaker in Linux con Windows Server failover clustering. Un'istanza di SQL Server non è a conoscenza del cluster. Pacemaker fornisce l'orchestrazione della risorsa cluster. Inoltre, il nome di rete virtuale è specifico per Windows Server failover clustering, è disponibile un equivalente in Pacemaker. Disponibilità gruppo viste a gestione dinamica (DMV) che le informazioni del cluster di query restituiscono righe vuote nei cluster Pacemaker. Per creare un listener per la riconnessione dopo il failover trasparente, registrare manualmente il nome del listener in DNS con l'indirizzo IP usato per creare la risorsa IP virtuale. 

Le sezioni seguenti illustrano i passaggi per configurare un cluster Pacemaker e aggiungere un gruppo di disponibilità come risorsa nel cluster per la disponibilità elevata.

## <a name="roadmap"></a>Guida di orientamento

I passaggi per creare un gruppo di disponibilità nei server Linux per la disponibilità elevata sono diversi dai passaggi in un cluster di failover di Windows Server. L'elenco seguente descrive i passaggi generali: 

1. [Configurare SQL Server nei nodi del cluster](sql-server-linux-setup.md).

2. [Creare il gruppo di disponibilità](sql-server-linux-availability-group-configure-ha.md). 

3. Configurare un cluster di resource manager, ad esempio Pacemaker. Queste istruzioni sono in questo documento.
   
   Il modo per configurare un gestore di risorse cluster dipende la distribuzione Linux specifica. 

   >[!IMPORTANT]
   >Gli ambienti di produzione richiedono un agente di isolamento, ad esempio STONITH per la disponibilità elevata. Le dimostrazioni in questa documentazione non usano gli agenti di fencing. Le dimostrazioni sono per i test e convalida solo. 
   
   >Un cluster Linux Usa l'isolamento per restituire il cluster a uno stato noto. Il modo per configurare l'isolamento varia a seconda della distribuzione e l'ambiente. Attualmente, l'isolamento non è disponibile in alcuni ambienti cloud. Per altre informazioni, vedere [criteri di supporto per RHEL cluster disponibilità elevata - piattaforme di virtualizzazione](https://access.redhat.com/articles/29440).

5. [Aggiungere il gruppo di disponibilità come una risorsa in cluster](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).  

## <a name="configure-high-availability-for-rhel"></a>Configurare la disponibilità elevata per RHEL

Per configurare la disponibilità elevata per RHEL, abilitare la sottoscrizione di un'elevata disponibilità e quindi configurare Pacemaker.

### <a name="enable-the-high-availability-subscription-for-rhel"></a>Abilitare la sottoscrizione di disponibilità elevata per RHEL

Ogni nodo nel cluster deve avere una sottoscrizione appropriata per RHEL e la disponibilità elevata Add. Esaminare i requisiti nel [come installare i pacchetti di cluster di disponibilità elevata in Red Hat Enterprise Linux](https://access.redhat.com/solutions/45930). Seguire questi passaggi per configurare la sottoscrizione e il repository:

1. Registrare il sistema.

   ```bash
   sudo subscription-manager register
   ```

   Specificare nome utente e password.   

1. Elencare i pool disponibili per la registrazione.

   ```bash
   sudo subscription-manager list --available
   ```

   Dall'elenco dei pool disponibile, prendere nota dell'ID del pool per la sottoscrizione di disponibilità elevata.

1. Aggiornare lo script seguente. Sostituire `<pool id>` con l'ID del pool per la disponibilità elevata dal passaggio precedente. Eseguire lo script per collegare la sottoscrizione.

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. Abilitare il repository.

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

Per altre informazioni, vedere [Pacemaker - l'Open Source, il Cluster a disponibilità elevata](https://clusterlabs.org/pacemaker/). 

Dopo aver configurato la sottoscrizione, completare i passaggi seguenti per configurare Pacemaker:

### <a name="configure-pacemaker"></a>Configurare Pacemaker

Dopo aver registrato la sottoscrizione, completare i passaggi seguenti per configurare Pacemaker:
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

Dopo aver configurato Pacemaker, usare `pcs` per interagire con il cluster. Eseguire tutti i comandi in un nodo dal cluster. 

## <a name="configure-fencing-stonith"></a>Configurare l'isolamento (STONITH)

I fornitori del cluster pacemaker richiedono STONITH deve essere abilitata e un dispositivo di fencing configurato per l'installazione del cluster supportate. STONITH è l'acronimo di "girare in altro nodo nell'intestazione". Se cluster resource manager non è possibile determinare lo stato di un nodo o di una risorsa in un nodo, fencing porta nuovamente il cluster a uno stato noto.

Isolamento a livello di risorse garantisce che non vi sia alcun danneggiamento dei dati in caso di interruzione tramite la configurazione di una risorsa. Ad esempio, è possibile utilizzare l'isolamento a livello di risorsa per contrassegnare il disco in un nodo come obsoleta quando il collegamento di comunicazione si arresta. 

Isolamento a livello di nodo assicura che un nodo non viene eseguita alcuna risorsa. In tal caso, reimpostare il nodo. Pacemaker supporta una vasta gamma di dispositivi di conflitti. Gli esempi includono un uninterruptible power supply o gestione schede di interfaccia di per i server.

Per informazioni su STONITH e l'isolamento, vedere gli articoli seguenti:

* [Cluster pacemaker da zero](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/index.html)
* [L'isolamento e STONITH](https://clusterlabs.org/doc/crm_fencing.html)
* [Componente aggiuntivo disponibilità elevata di Red Hat con Pacemaker: Isolamento](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

Poiché il livello del nodo recinzioni configurazione dipende principalmente dall'ambiente, disabilitarlo per questa esercitazione (può essere configurato in un secondo momento). Lo script seguente disabilita isolamento a livello di nodo:

```bash
sudo pcs property set stonith-enabled=false
```
  
>[!IMPORTANT]
>La disabilitazione di STONITH è solo a scopo di test. Se si prevede di utilizzare Pacemaker in un ambiente di produzione, è necessario pianificare un'implementazione di STONITH a seconda dell'ambiente e lasciarla abilitata. RHEL non fornisce gli agenti di fencing per ambienti cloud (tra cui Azure) o Hyper-V. Consequentially, il fornitore del cluster non offre il supporto per l'esecuzione di cluster di produzione in questi ambienti. Microsoft sta lavorando a una soluzione per questo divario che sarà disponibile nelle versioni future.

## <a name="set-cluster-property-cluster-recheck-interval"></a>Impostare proprietà di cluster del cluster-Ricontrolla-intervallo

`cluster-recheck-interval` indica l'intervallo di polling in corrispondenza del quale il cluster controlla modifiche nei parametri delle risorse, i vincoli o altre opzioni di cluster. Se una replica diventa inattiva, il cluster tenta di riavviare la replica in base all'intervallo è associato mediante il `failure-timeout` valore e il `cluster-recheck-interval` valore. Ad esempio, se `failure-timeout` è impostato su 60 secondi e `cluster-recheck-interval` è impostato su 120 secondi, il riavvio viene eseguito un tentativo in base all'intervallo è maggiore di 60 secondi ma inferiore a 120 secondi. È consigliabile impostare timeout errore 60s e controlla di nuovo-cluster-interval su un valore maggiore di 60 secondi. Non è consigliabile impostare intervallo-cluster-nuova verifica su un valore ridotto.

Per aggiornare il valore della proprietà da `2 minutes` eseguire:

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Tutte le distribuzioni, inclusi RHEL 7.3 e 7.4, che usano la versione più recente disponibile Pacemaker pacchetto 1.1.18-11.el7 introducono un cambiamento di comportamento per l'impostazione di start-errore-è-errore irreversibile cluster quando il relativo valore è false. Questa modifica interessa il flusso di lavoro di failover. Se una replica primaria si verifica un'interruzione, il cluster è previsto per il failover su una delle repliche secondarie disponibili. Al contrario, gli utenti noteranno che il cluster insiste avviare la replica primaria non riuscita. Se tale database primario non torna online (a causa di un'interruzione dell'alimentazione permanente), il cluster mai effettua il failover a un'altra replica secondaria disponibile. Grazie a questa modifica, una configurazione consigliata in precedenza per impostare start-errore-è-errore irreversibile non è più valida e l'impostazione deve essere ripristinato il valore predefinito di `true`. Inoltre, la risorsa del gruppo di disponibilità deve essere aggiornato per includere il `failover-timeout` proprietà. 

Per aggiornare il valore della proprietà da `true` eseguire:

```bash
sudo pcs property set start-failure-is-fatal=true
```

Per aggiornare il `ag_cluster` proprietà della risorsa `failure-timeout` a `60s` eseguire:

```bash
pcs resource update ag_cluster meta failure-timeout=60s
```


Per informazioni sulla proprietà del cluster Pacemaker, vedere [proprietà cluster Pacemaker](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html).

## <a name="create-a-sql-server-login-for-pacemaker"></a>Creare un account di accesso di SQL Server per Pacemaker

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Crea risorsa gruppo di disponibilità

Per creare la risorsa del gruppo di disponibilità, usare `pcs resource create` comando e impostare le proprietà della risorsa. Il comando seguente crea una `ocf:mssql:ag` tipo di risorsa per il gruppo di disponibilità con nome primario/secondario `ag1`.

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s master notify=true
``` 

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>Creare una risorsa IP virtuale

Per creare la risorsa indirizzo IP virtuale, eseguire il comando seguente in un nodo. Usare un indirizzo IP statico disponibile dalla rete. Sostituire l'indirizzo IP tra `<10.128.16.240>` con un indirizzo IP valido.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Non c'è Nessun nome server virtuale equivalente in Pacemaker. Per usare una stringa di connessione che punta al nome del server stringa anziché un indirizzo IP, registrare l'indirizzo risorsa IP virtuale e il nome del server virtuale desiderato nel DNS. Per le configurazioni di ripristino di emergenza, registrare il nome del server virtuale desiderato e l'indirizzo IP con i server DNS primario sia il sito di ripristino di emergenza.

## <a name="add-colocation-constraint"></a>Aggiungi vincolo di condivisione del percorso

Quasi ogni decisione di in un cluster Pacemaker, come scegliere in cui deve essere eseguita una risorsa, viene eseguita confrontando i punteggi. I punteggi vengono calcolati per ogni risorsa. Cluster resource manager sceglie il nodo con il punteggio più alto per una determinata risorsa. Se un nodo ha un punteggio negativo per una risorsa, la risorsa non è possibile eseguire su tale nodo.

In un cluster pacemaker, è possibile modificare le decisioni del cluster con vincoli. I vincoli hanno un punteggio. Se un vincolo ha un punteggio minore `INFINITY`, Pacemaker lo considera come indicazioni. Un punteggio pari a `INFINITY` è obbligatorio.

Per assicurarsi che la replica primaria e le risorse di indirizzo ip virtuale eseguiti nello stesso host, definire un vincolo di condivisione del percorso con un punteggio pari a infinito. Per aggiungere il vincolo di condivisione del percorso, eseguire il comando seguente in un nodo.

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Aggiungi vincolo di ordinamento

Il vincolo di condivisione percorso ha un vincolo di ordinamento implicito. Sposta la risorsa IP virtuale prima di spostare la risorsa del gruppo di disponibilità. Per impostazione predefinita è la sequenza di eventi:

1. Problemi degli utenti `pcs resource move` al gruppo di disponibilità primario da node1 a node2.
1. La risorsa IP virtuale viene arrestata nel nodo 1.
1. La risorsa IP virtuale verrà avviata nel nodo 2.
  
   >[!NOTE]
   >A questo punto, l'indirizzo IP temporaneamente punti al nodo 2 mentre il nodo 2 è ancora un pre-failover secondario. 
   
1. Il gruppo di disponibilità primario nel nodo 1 viene abbassato di livello a quello secondario.
1. Il gruppo di disponibilità secondario nel nodo 2 viene promossa a primaria. 

Per evitare temporaneamente che puntano al nodo con il database secondario pre-failover l'indirizzo IP, aggiungere un vincolo di ordinamento. 

Per aggiungere un vincolo di ordinamento, eseguire il comando seguente in un nodo:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Dopo aver configurato il cluster e aggiungere il gruppo di disponibilità come risorsa cluster, è possibile usare Transact-SQL per eseguire il failover le risorse di gruppo di disponibilità. Risorse del cluster SQL Server in Linux non sono collegate come strettamente con il sistema operativo perché sono in un Server Failover Cluster WSFC (Windows). Servizio SQL Server non riconosce la presenza del cluster. Tutte le orchestrazioni vengono eseguite mediante gli strumenti di gestione di cluster. In Ubuntu o RHEL, usare `pcs` e in uso SLES `crm` strumenti. 

Eseguire manualmente il failover il gruppo di disponibilità con `pcs`. Non avviare il failover con Transact-SQL. Per istruzioni, vedere [Failover](sql-server-linux-availability-group-failover-ha.md#failover).

## <a name="next-steps"></a>Passaggi successivi

[Funzionamento di gruppo di disponibilità elevata](sql-server-linux-availability-group-failover-ha.md)
