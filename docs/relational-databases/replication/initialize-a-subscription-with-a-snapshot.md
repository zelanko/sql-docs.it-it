---
title: Inizializzare una sottoscrizione con snapshot
ms.custom: ''
ms.date: 03/23/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cb69f5c2033a515676587ddbef0cb3d14e3bc3d6
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396134"
---
# <a name="initialize-a-subscription-with-a-snapshot-for-a-new-publication"></a>Inizializzare una sottoscrizione con uno snapshot per una nuova pubblicazione

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

Questo articolo descrive i processi che si verificano durante l'inizializzazione della pubblicazione di una replica. Uno snapshot iniziale viene applicato ai sottoscrittori.

## <a name="snapshot-for-a-new-publication"></a>Snapshot per una nuova pubblicazione

Per impostazione predefinita, dopo la creazione di una pubblicazione viene acquisito uno snapshot.
Lo snapshot viene copiato nella cartella degli snapshot. Questo comportamento predefinito si verifica per le pubblicazioni di tipo merge create usando la Creazione guidata nuova pubblicazione.

### <a name="snapshot-is-applied-to-subscriber"></a>Lo snapshot viene applicato al sottoscrittore

Il nuovo snapshot viene applicato al sottoscrittore da un agente. L'applicazione si verifica durante la sincronizzazione iniziale della sottoscrizione. L'agente che esegue l'applicazione dipende dal tipo di pubblicazione:

- Per le pubblicazioni _transazionali_ e _snapshot_:
  - Agente di distribuzione.

- Per le pubblicazioni di tipo _merge_:
  - Agente di merge.

### <a name="type-of-publication"></a>Tipo di pubblicazione

La tabella seguente visualizza il contenuto dello snapshot, per ogni tipo di pubblicazione.

&nbsp;

| Tipo di pubblicazione dello snapshot | Contenuto dello snapshot |
| :---------------------------------------- | :----------------------- |
| <ul> <li>Pubblicazione snapshot</li> <li>Pubblicazione transazionale</li> <li>Pubblicazione di tipo merge che non usa filtri con parametri</li> </ul> | <ul> <li>SCHEMA</li> <li>Dati, in file per il programma per la copia bulk (BCP)</li> <li>Vincoli</li> <li>Proprietà estese</li> <li>Indici</li> <li>Trigger</li> <li>Tabelle di sistema necessarie per la replica</li> </ul> <br/>Vedere [Creare e applicare lo snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md). |
| <ul> <li>Pubblicazione di tipo merge che usa filtri con parametri</li> </ul> | <ul> <li>Snapshot dello schema (script di replica, oggetti pubblicati, ma nessun dato)</li> <li>Dati appartenenti alla partizione della sottoscrizione</li> </ul> <br/>Vedere [Snapshot per pubblicazioni di tipo merge con filtri con parametri](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). |
| | |

#### <a name="two-part-process-with-merge-publication-that-uses-parameterized-filters"></a>Processo a due fasi con pubblicazione di tipo merge che usa filtri con parametri

Per una pubblicazione di tipo merge che usa filtri con parametri, lo snapshot viene creato usando il processo a due fasi seguente:

1. Viene creato uno snapshot dello schema contenente gli elementi seguenti:
   - Script di replica.
   - Schema degli oggetti pubblicati.
   - _Nessun dato._

2. Ogni sottoscrizione viene quindi inizializzata con uno snapshot. Lo snapshot include gli elementi seguenti:
   - Script e schema, copiati dallo snapshot dello schema.
   - Dati appartenenti alla partizione della sottoscrizione.

## <a name="type-of-replication"></a>Tipo di replica

I tipi di file contenuti nello snapshot dipendono dal tipo di replica e dagli articoli della pubblicazione.

&nbsp;

| Tipo di replica | File di snapshot comuni |
| :------------------ | :-------------------- |
| Replica snapshot o<br/>Replica transazionale | &bullet; Schema (sch) <br/>&bullet; Dati (bcp) <br/>&bullet; Vincoli e indici (dri) <br/>&bullet; File di snapshot compressi (cab) <br/>&bullet; Trigger (tag), solo per l'aggiornamento di un sottoscrittore <br/><br/>&bullet; Vincoli (idx) |
| Replica di tipo merge                                      | &bullet; Schema (sch) <br/>&bullet; Dati (bcp) <br/>&bullet; Vincoli e indici (dri) <br/>&bullet; File di snapshot compressi (cab) <br/>&bullet; Trigger (trg) <br/><br/>&bullet; Dati di tabelle di sistema (sys) <br/>&bullet; Tabelle dei conflitti (cft) |
| | |

### <a name="snapshot-folder"></a>Cartella snapshot

I file vengono trasferiti tramite copia nella _cartella degli snapshot_ predefinita o nella _cartella alternativa_ per gli snapshot.

La cartella degli snapshot viene specificata quando viene configurato il database di distribuzione. La cartella alternativa viene specificata quando viene creata la pubblicazione.

### <a name="resume-transfer-after-interruption"></a>Riprendere il trasferimento dopo un'interruzione

Il trasferimento di file in una cartella degli snapshot riprende automaticamente se il trasferimento viene interrotto da una connessione non affidabile.

Per una maggiore efficienza, i file già trasferiti completamente prima dell'interruzione non vengono inviati nuovamente con la ripresa.

## <a name="snapshot-options"></a>Opzioni per gli snapshot

Quando si inizializza una sottoscrizione con uno snapshot, sono disponibili diverse opzioni. È possibile:

- Specificare una posizione alternativa per la cartella snapshot in aggiunta a quella predefinita o al posto di questa. Per altre informazioni, vedere [Modificare le opzioni snapshot](../../relational-databases/replication/snapshot-options.md).

- Comprimere gli snapshot per l'archiviazione sui supporti rimovibili o il trasferimento su una rete lenta. Per altre informazioni, vedere [Compressed Snapshots](../../relational-databases/replication/snapshot-options.md#compressed-snapshots).

- Eseguire gli script Transact-SQL prima o dopo aver applicato lo snapshot. Per altre informazioni, vedere [Eseguire gli script prima e dopo l'applicazione dello snapshot](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).

- Trasferire i file di snapshot mediante il protocollo FTP (File Transfer Protocol). Per altre informazioni, vedere [Trasferire snapshot tramite FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).

## <a name="see-also"></a>Vedere anche

[Inizializzare una sottoscrizione](../../relational-databases/replication/initialize-a-subscription.md)

[Proteggere la cartella snapshot](../../relational-databases/replication/security/secure-the-snapshot-folder.md)
