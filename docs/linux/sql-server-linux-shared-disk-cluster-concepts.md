---
title: 'Istanze del Cluster di failover: SQL Server in Linux'
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 31d53db207dd7c3fa213e96261062b2575562e31
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833200"
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>Istanze del Cluster di failover: SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra i concetti relativi alle istanze del cluster failover di SQL Server (FCI) in Linux. 

Per creare un SQL Server FCI in Linux, vedere [configurare SQL Server FCI in Linux](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>Il livello di Clustering

* In RHEL, il livello di clustering è basato su Red Hat Enterprise Linux (RHEL) [componente aggiuntivo a disponibilità elevata](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf). 

    > [!NOTE] 
    > L'accesso al componente aggiuntivo Red Hat a disponibilità elevata e alla documentazione richiede una sottoscrizione. 

* SLES, il livello di clustering si basa su SUSE Linux Enterprise [estensione a disponibilità elevata (Georgiano)](https://www.suse.com/products/highavailability).

    Per altre informazioni su configurazione del cluster, opzioni dell'agente di risorsa, gestione, le procedure consigliate e indicazioni, vedere [SUSE Linux Enterprise ad alta disponibilità estensione 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

Sia il componente RHEL a disponibilità elevata e il HAE SUSE sono basate sulla [Pacemaker](https://clusterlabs.org/).

Come illustrato nella figura seguente, archiviazione viene presentata a due server. Componenti di clustering - Corosync e Pacemaker - coordinano le comunicazioni e gestione delle risorse. Uno dei server con connessione attiva per le risorse di archiviazione e SQL Server. Quando Pacemaker rileva un errore i componenti di clustering gestiscono lo spostamento avvenga a altro nodo.  

![Red Hat Enterprise Linux 7 condiviso del disco Cluster SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> A questo punto, l'integrazione con Pacemaker in Linux SQL Server non è accoppiato come con WSFC per Windows. All'interno di SQL, non è possibile sapere sulla presenza del cluster, tutte le orchestrazioni non rientra e il servizio viene controllato in base a un'istanza autonoma per Pacemaker. Inoltre, nome di rete virtuale è specifico al cluster WSFC, è disponibile un equivalente dello stesso in Pacemaker. È previsto che @@servername e Sys. Servers per restituire il nome del nodo, mentre il DM os_cluster_nodes viste a gestione dinamica di cluster e DM os_cluster_properties non sarà alcun record. Per usare una stringa di connessione che punta al nome di un server di stringa e non usare l'indirizzo IP, dovranno registrare i server DNS dell'indirizzo IP usato per creare la risorsa IP virtuale (come illustrato nelle sezioni seguenti) con il nome del server scelto.

## <a name="number-of-instances-and-nodes"></a>Numero di istanze e i nodi

Una differenza fondamentale con SQL Server in Linux è che può essere presente solo un'installazione di SQL Server per ogni server Linux. L'installazione viene chiamata un'istanza. Ciò significa che a differenza di Windows Server che supporta fino a 25 istanze FCI per ogni cluster di failover di Windows Server (WSFC), un'istanza cluster di failover basato su Linux avrà solo una singola istanza. Un'istanza di questo è anche un'istanza predefinita; non è previsto di un'istanza denominata in Linux. 

Un cluster Pacemaker può avere solo un massimo di 16 nodi quando è coinvolto Corosync, in modo che una singola istanza del cluster di failover possa estendersi fino a 16 server. Un'istanza FCI implementata con di SQL Server Standard Edition supporta fino a due nodi di un cluster anche se il cluster Pacemaker è il numero massimo di 16 nodi.

In un failover di SQL Server, l'istanza di SQL Server è attivo in un nodo o l'altro.

## <a name="ip-address-and-name"></a>Nome e indirizzo IP
In un cluster Pacemaker di Linux, ogni failover di SQL Server richiede un proprio indirizzo IP univoco e il nome. Se la configurazione di FCI si estende su più subnet, un indirizzo IP sarà richiesto per ogni subnet. Il nome univoco e indirizzi IP vengono utilizzati per accedere l'istanza FCI in modo che le applicazioni e gli utenti finali non è necessario sapere in quale server sottostante del cluster Pacemaker.

Il nome dell'istanza FCI in DNS deve essere identico al nome della risorsa istanza cluster di failover che viene creato nel cluster Pacemaker.
Il nome e indirizzo IP deve essere registrati in DNS.

## <a name="shared-storage"></a>Archiviazione condivisa
Tutte le istanze FCI, siano essi in Linux o Windows Server, richiedono un tipo di archiviazione condiviso. Questa risorsa di archiviazione viene presentato a tutti i server che possono essere ospitati eventualmente l'infrastruttura di classificazione file, ma solo un singolo server può usare lo spazio di archiviazione per l'istanza FCI in qualsiasi momento. Le opzioni disponibili per l'archiviazione condivisa in Linux sono:

- iSCSI
- Network File System (NFS)
- Server Message Block (SMB) in Windows Server, sono disponibili opzioni leggermente diverse. Un'opzione non è attualmente supportata per le istanze FCI basato su Linux è la possibilità di usare un disco locale per il nodo per il database TempDB, ovvero l'area di lavoro temporanea di SQL Server.

In una configurazione che si estende su più posizioni, che viene archiviato in un data center deve essere sincronizzato con l'altro. In caso di failover, l'istanza FCI sarà in grado di portare in linea e lo spazio di archiviazione viene considerato come lo stesso. Raggiungere questo obiettivo richiederanno un metodo esterno per la replica di archiviazione, se avviene tramite un'utilità basata su software o hardware di archiviazione sottostante. 

>[!NOTE]
>Per SQL Server, le distribuzioni basate su Linux usano dischi presentati direttamente a un server di questo tipo devono essere formattate con XFS o EXT4. Altri sistemi di file non sono attualmente supportati. Tutte le modifiche si rifletteranno qui.

Il processo per la presentazione di spazio di archiviazione condiviso è lo stesso per i diversi metodi supportati:

- Configurare l'archiviazione condivisa
- Montare la risorsa di archiviazione come una cartella per i server che fungono da nodi del cluster Pacemaker per l'istanza FCI
- Se necessario, spostare i database di sistema di SQL Server all'archiviazione condivisa
- Test di SQL Server funziona da ogni server connessi all'archiviazione condivisa

Una differenza principale con SQL Server in Linux è che sebbene sia possibile configurare il percorso di file predefinito log e dati dell'utente, i database di sistema devono essere sempre presente in `/var/opt/mssql/data`. In Windows Server, è presente la possibilità di spostare i database di sistema, incluso TempDB. Questo fatto viene riprodotto in archiviazione condivisa come è configurato per un'istanza FCI.

I percorsi predefiniti per i database di sistema non possono essere modificati utilizzando la `mssql-conf` utilità. Per informazioni su come modificare le impostazioni predefinite [modificare il percorso della directory predefinita dati o di log](sql-server-linux-configure-mssql-conf.md#datadir). È anche possibile archiviare i dati di SQL Server e delle transazioni in altre posizioni, purché hanno la sicurezza appropriata, anche se non è un percorso predefinito; il percorso dovrebbe essere indicato.

Gli argomenti seguenti illustrano come configurare i tipi di archiviazione supportati per Linux basate su SQL Server FCI:

- [Configurare l'istanza del cluster di failover SQL Server in Linux - iSCSI:](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Configurare cluster di failover - NFS - SQL Server in Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Configurare cluster di failover - SMB - SQL Server in Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
