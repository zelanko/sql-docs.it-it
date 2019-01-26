---
title: SQL Server Always On modelli distribuzione gruppo di disponibilità | Microsoft Docs
ms.custom: sql-linux
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: linux
ms.topic: conceptual
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a9d09f9f769d195600c8af97b347831340837d91
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044934"
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>Elevata disponibilità e protezione dei dati per le configurazioni di gruppo di disponibilità

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo presenta le configurazioni di distribuzione supportate per i gruppi di disponibilità Always On di SQL Server nei server Linux. Un gruppo di disponibilità supporta la disponibilità elevata e protezione dei dati. Rilevamento degli errori automatico, failover automatico e trasparente riconnessione dopo il failover forniscono disponibilità elevata. Repliche sincronizzate offrono protezione dei dati. 

In un Server Failover Cluster WSFC (Windows), una configurazione comune per la disponibilità elevata utilizza due repliche sincrone e una terzo server o la condivisione file per fornire quorum. La condivisione di file di controllo convalida la configurazione del gruppo di disponibilità - stato di sincronizzazione e il ruolo della replica, ad esempio. Questa configurazione assicura che la replica secondaria scelta come destinazione del failover con i dati più recenti e le modifiche alla configurazione gruppo di disponibilità. 

Il cluster WSFC Sincronizza i metadati di configurazione per l'arbitraggio failover tra le repliche del gruppo di disponibilità e il controllo di condivisione file. Quando un gruppo di disponibilità non è presente in un cluster WSFC, le istanze di SQL Server archiviano i metadati di configurazione nel database master.

Ad esempio, dispone di un gruppo di disponibilità in un cluster Linux `CLUSTER_TYPE = EXTERNAL`. Non è disponibile alcun WSFC in corso il failover. In questo caso i metadati di configurazione vengano gestito e gestiti da istanze di SQL Server. Poiché non è presente alcun server di controllo in questo cluster, è necessaria una terza istanza di SQL Server per archiviare i metadati di configurazione dello stato. Tutte le tre istanze di SQL Server insieme forniscono metadati distribuiti archiviazione per il cluster. 

Cluster manager può eseguire una query di istanze di SQL Server nel gruppo di disponibilità e orchestrare il failover per mantenere la disponibilità elevata. In un cluster Linux Pacemaker è la gestione di cluster. 

SQL Server 2017 CU 1 abilita la disponibilità elevata per un gruppo di disponibilità con `CLUSTER_TYPE = EXTERNAL` per due repliche sincrone oltre a una replica di sola configurazione. La replica di sola configurazione può essere ospitato in qualsiasi edizione di SQL Server 2017 da CU1 o versione successiva - tra cui SQL Server Express edition. La replica di sola configurazione mantiene le informazioni di configurazione relative al gruppo di disponibilità nel database master, ma non contiene i database utente nel gruppo di disponibilità. 

## <a name="how-the-configuration-affects-default-resource-settings"></a>Effetti della configurazione delle impostazioni di risorse predefinito

SQL Server 2017 introduce la `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` impostazione risorse del cluster. Questa impostazione garantisce il numero di repliche secondarie scrittura specificato i dati di transazione per accedere prima che la replica primaria esegue il commit di ogni transazione. Quando si usa un manager di cluster external, questa impostazione riguarda la disponibilità elevata e protezione dei dati. Il valore predefinito per l'impostazione dipende dall'architettura al momento che della creazione della risorsa cluster. Quando si installa l'agente delle risorse SQL Server - `mssql-server-ha` - e creare una risorsa cluster del gruppo di disponibilità, la gestione di cluster rileva la disponibilità di gruppo configurazione e imposta `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` conseguenza. 

Se supportato dalla configurazione, il parametro dell'agente della risorsa `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` è impostata sul valore che fornisce elevata disponibilità e protezione dei dati. Per altre informazioni, vedere [agente delle risorse conoscere SQL Server per pacemaker](#pacemakerNotify).

Le sezioni seguenti illustrano il comportamento predefinito per la risorsa cluster. 

Scegliere una progettazione di gruppo di disponibilità per soddisfare i requisiti aziendali specifici per la disponibilità elevata, la protezione dei dati e scalabilità in lettura.

Le configurazioni seguenti vengono descritti i modelli di progettazione di gruppo di disponibilità e le funzionalità di ogni modello. Questi schemi progettuali applicano ai gruppi di disponibilità con `CLUSTER_TYPE = EXTERNAL` per soluzioni a disponibilità elevata. 

- **Tre repliche sincrone**
- **Due repliche sincrone**
- **Una replica di sola configurazione e due repliche sincrone**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>Tre repliche sincrone

Questa configurazione è costituita da tre repliche sincrone. Per impostazione predefinita, fornisce elevata disponibilità e protezione dei dati. Fornisce anche la scalabilità in lettura.

![Tre repliche][3]

Un gruppo di disponibilità con tre repliche sincrone può fornire la protezione dei dati, la disponibilità elevata e scalabilità in lettura. La tabella seguente descrive il comportamento di disponibilità. 

| |read-scale|Disponibilità elevata & </br> protezione dei dati | Protezione dei dati|
|:---|---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>\*</sup>|2|
|Interruzione primaria | Failover manuale. Potrebbe verificarsi la perdita di dati. Nuova replica primaria è R / w. |Failover automatico. Nuova replica primaria è R / w. |Failover automatico. Nuovo database primario non è disponibile per le transazioni utente fino a quando i database primario viene ripristinato e join di gruppo di disponibilità secondario. |
|Interruzione di una replica secondaria  | La replica primaria è R / w. Nessun failover automatico se l'area primaria non riesce. |La replica primaria è R / w. Nessun failover automatico se l'area primaria non riesce anche. | Database primario non è disponibile per le transazioni utente. |

<sup>\*</sup> Default

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>Due repliche sincrone

Questa configurazione abilita la protezione dei dati. Come le altre configurazioni gruppo disponibilità, è possibile abilitare con scalabilità in lettura. La configurazione di due repliche sincrone non fornisce la disponibilità elevata automatica. 

![Due repliche sincrone][1]

Un gruppo di disponibilità con due repliche sincrone fornisce scalabilità in lettura e la protezione dati. La tabella seguente descrive il comportamento di disponibilità. 

| |read-scale |Protezione dei dati|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|Interruzione primaria | Failover manuale. Potrebbe verificarsi la perdita di dati. Nuova replica primaria è R / w.| Failover automatico. Nuovo database primario non è disponibile per le transazioni utente fino a quando i database primario viene ripristinato e join di gruppo di disponibilità secondario.|
|Interruzione di una replica secondaria  |La replica primaria è L/S, esecuzione esposta alla perdita di dati. |Database primario non è disponibile per le transazioni utente fino al recupero della replica secondaria.|

<sup>\*</sup> Default

> [!NOTE]
> Lo scenario precedente è il comportamento prima dell'aggiornamento Cumulativo 1 di SQL Server 2017. 

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>Una replica di sola configurazione e due repliche sincrone

Un gruppo di disponibilità con repliche sincrone due (o più) e una replica di sola configurazione fornisce la protezione dei dati e può anche fornire la disponibilità elevata. Il diagramma seguente rappresenta questa architettura:

![Gruppo di disponibilità solo di configurazione][2]

1. Replica dei dati utente per la replica secondaria sincrona. Include anche i metadati di configurazione gruppo di disponibilità.
2. Replica sincrona dei metadati di configurazione gruppo di disponibilità. Non include dati utente.

Nel diagramma gruppo di disponibilità, una replica primaria esegue il push dei dati di configurazione per la replica secondaria e la replica di sola configurazione. La replica secondaria riceve anche i dati dell'utente. La replica di sola configurazione non riceve i dati dell'utente. La replica secondaria è in modalità di disponibilità sincroni. La replica di sola configurazione non contiene i database nel gruppo di disponibilità - solo i metadati sul gruppo di disponibilità. I dati di configurazione di replica di sola configurazione viene eseguito il commit in modo sincrono.

> [!NOTE]
> Un gruppo di availabilility con replica di sola configurazione è nuovo per SQL Server 2017 da CU1. Tutte le istanze di SQL Server nel gruppo di disponibilità devono essere SQL Server 2017 da CU1 o versione successiva. 

Il valore predefinito per `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` è 0. La tabella seguente descrive il comportamento di disponibilità. 

| |Disponibilità elevata & </br> protezione dei dati | Protezione dei dati|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|Interruzione primaria | Failover automatico. Nuova replica primaria è R / w. | Failover automatico. Nuovo database primario non è disponibile per le transazioni utente. |
|Interruzione di servizio di replica secondaria | Replica primaria è L/S, esecuzione esposta alla perdita di dati (se primario ha esito negativo e non può essere ripristinato). Nessun failover automatico se l'area primaria non riesce anche. | Database primario non è disponibile per le transazioni utente. Nessuna replica per eseguire il failover se l'area primaria non riesce. |
|Interruzione di servizio di configurazione solo replica | La replica primaria è R / w. Nessun failover automatico se l'area primaria non riesce anche. | La replica primaria è R / w. Nessun failover automatico se l'area primaria non riesce anche. |
|Database secondario sincrono + configurazione solo un'interruzione di replica| Database primario non è disponibile per le transazioni utente. Nessun failover automatico. | Database primario non è disponibile per le transazioni utente. Per eseguire il failover se nessuna replica primario si verifica un errore anche. |

<sup>\*</sup> Default

> [!NOTE]
> L'istanza di SQL Server che ospita la replica di sola configurazione può ospitare anche altri database. Anche possibile partecipare come un database di sola configurazione per più di un gruppo di disponibilità. 

## <a name="requirements"></a>Requisiti

- Tutte le repliche in un gruppo di disponibilità con una replica di sola configurazione devono essere SQL Server 2017 CU 1 o versione successiva.
- Qualsiasi edizione di SQL Server può ospitare una replica di sola configurazione, incluso SQL Server Express. 
- Il gruppo di disponibilità richiede almeno una replica secondaria - oltre alla replica primaria.
- Le repliche di sola configurazione non vengono conteggiati per il numero massimo di repliche per ogni istanza di SQL Server. SQL Server standard edition consente fino a tre repliche, SQL Server Enterprise Edition consente fino a 9.

## <a name="considerations"></a>Considerazioni

- Replica di sola configurazione non più di uno per ogni gruppo di disponibilità. 
- Una replica di sola configurazione non può essere una replica primaria.
- Non è possibile modificare la modalità di disponibilità di una replica di sola configurazione. Per passare da una replica di sola configurazione a una replica secondaria sincrona o asincrona, rimuovere la replica di sola configurazione e aggiungere una replica secondaria con la modalità di disponibilità necessari. 
- Una replica di sola configurazione è sincrona con i metadati del gruppo di disponibilità. Non sono presenti dati utente. 
- Un gruppo di disponibilità con una replica primaria e replica solo di una configurazione, ma nessuna replica secondaria non è valido. 
- È possibile creare un gruppo di disponibilità in un'istanza di SQL Server Express edition. 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>Comprendere l'agente delle risorse SQL Server per pacemaker

Aggiunta di SQL Server 2017 CTP 1.4 `sequence_number` a `sys.availability_groups` per consentire a Pacemaker identificare il livello di aggiornamento secondario delle repliche sono con la replica primaria. `sequence_number` è un valore BIGINT a incremento progressivo costante che rappresenta il livello di aggiornamento di replica del gruppo di disponibilità locale. Gli aggiornamenti di pacemaker il `sequence_number` a ogni modifica di configurazione gruppo di disponibilità. Il failover, aggiunta di replica o la rimozione sono esempi di modifiche di configurazione. Il numero viene aggiornato nella replica primaria e quindi replicato nelle repliche secondarie. In questo modo una replica secondaria con configurazione aggiornata ha lo stesso numero di sequenza della replica primaria. 

Quando Pacemaker decide di alzare di livello una replica primaria, invia prima di tutto una *pre-innalzamento* notifica a tutte le repliche. Le repliche di restituiscono il numero di sequenza. Successivamente, quando Pacemaker Cerca effettivamente di alzare di livello una replica primaria, la replica viene eseguita solo se stessa se il numero di sequenza è il più alto di tutti i numeri di sequenza. Se il proprio numero di sequenza non corrisponde il numero di sequenza più alto, la replica rifiuta l'operazione Alza di livello. In questo modo, solo la replica con il numero di sequenza più alto può essere alzata di livello e impostata come primaria e non si verifica alcuna perdita dei dati. 

Questo processo richiede almeno una replica di disponibilità per la promozione con lo stesso numero di sequenza della replica primaria precedente. I set di agenti di risorse Pacemaker `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` in modo che almeno una replica secondaria sincrona sia aggiornata e disponibile per essere la destinazione di un failover automatico per impostazione predefinita. Con ogni azione di monitoraggio, il valore di `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` è calcolato (e aggiornato se necessario). Il `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` valore è 'numero di repliche sincrone' diviso 2. In fase di failover, è necessario l'agente delle risorse (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` repliche) a cui rispondere la notifica pre-innalzamento. La replica con il valore massimo `sequence_number` viene promosso alla replica primaria. 

Ad esempio, un gruppo di disponibilità con tre repliche sincrone: una replica primaria e due repliche secondarie sincrone.

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` is 1; (3 / 2 -> 1).

- Il numero necessario di repliche a cui rispondere per pre-innalzamento azione è 2. (3 - 1 = 2). 

In questo scenario, è necessario rispondere per il failover venga attivato due repliche. Per il failover automatico ha esito positivo dopo un'interruzione della replica primaria, sia nelle repliche secondarie desidera essere aggiornate e rispondere per la notifica pre-innalzamento. Se sono online e sincrona, hanno lo stesso numero di sequenza. Il gruppo di disponibilità Alza di livello uno di essi. Se solo una delle repliche secondarie risponde per la pre-innalzamento azione, l'agente delle risorse non può garantire che il database secondario che ha risposto ha il sequence_number più elevato, e non viene attivato un failover.

> [!IMPORTANT]
> Quando `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` è 0 esiste il rischio di perdita dei dati. Durante un'interruzione della replica primaria, l'agente delle risorse non attiva automaticamente il failover. È possibile attendere per il database primario per il ripristino o eseguire manualmente il failover usando `FORCE_FAILOVER_ALLOW_DATA_LOSS`.

È possibile scegliere di eseguire l'override del comportamento predefinito e impedire la risorsa del gruppo di disponibilità di impostazione `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` automaticamente.

Lo script seguente imposta `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` su 0 in un gruppo di disponibilità denominato `<**ag1**>`. Prima di eseguire lo script, sostituire `<**ag1**>` con il nome del gruppo di disponibilità.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

Per ripristinare il valore predefinito, in base alla configurazione di gruppo di disponibilità eseguire:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

> [!NOTE]
> Quando si eseguono i comandi precedenti, il database primario è temporaneamente abbassata di livello a quello secondario, quindi promossa nuovamente. L'aggiornamento della risorsa fa in modo che tutte le repliche arrestare e riavviare. Il nuovo valore per`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` viene impostato solo dopo il riavvio delle repliche, non istantaneamente.

## <a name="see-also"></a>Vedere anche

[Gruppi di disponibilità in Linux](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
