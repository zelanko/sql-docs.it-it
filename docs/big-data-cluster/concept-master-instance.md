---
title: Che cos'è l'istanza master?
titleSuffix: SQL Server 2019 big data clusters
description: Questo articolo descrive l'istanza master di SQL Server in un cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 2ea25aeb5c7c39c5b00e545bc39974073132b1b2
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208170"
---
# <a name="what-is-the-master-instance-in-a-sql-server-2019-big-data-cluster"></a>Che cos'è l'istanza master in un cluster di SQL Server 2019 big data?

Questo articolo descrive il ruolo del *istanza master di SQL Server* in un cluster di big data di SQL Server 2019. L'istanza master è un'istanza di SQL Server in esecuzione in un cluster di big data server&#41 [piano di controllo](big-data-cluster-overview.md#controlplane).

L'istanza master di SQL Server offre le funzionalità seguenti:

## <a name="connectivity"></a>Connettività

L'istanza master di SQL Server fornisce un endpoint TDS accessibile dall'esterno per il cluster. È possibile connettere le applicazioni o strumenti di SQL Server, ad esempio Data Studio di Azure o convertito tramite SQL Server Management Studio per questo endpoint come qualsiasi altra istanza di SQL Server.

## <a name="scale-out-query-management"></a>Gestione delle query di tipo scale-out

L'istanza master di SQL Server contiene il motore di query di tipo scale-out che consente di distribuire le query tra istanze di SQL Server in nodi di [pool di calcolo](concept-compute-pool.md). Il motore di query di scalabilità orizzontale fornisce inoltre l'accesso tramite Transact-SQL per tutte le tabelle Hive nel cluster senza alcuna configurazione aggiuntiva. (Supporto per le tabelle hive non è in CTP 2.2)

## <a name="metadata-and-user-databases"></a>I metadati e dei database utente

Oltre ai database di sistema SQL Server standard, l'istanza SQL master contiene inoltre quanto segue:

- Un database dei metadati che contiene i metadati della tabella di HDFS
- Una mappa partizioni di piano dati
- Dettagli delle tabelle esterne che forniscono l'accesso al piano dati del cluster.
- Origini dati esterne PolyBase e tabelle esterne definite nel database utente.

È anche possibile scegliere di aggiungere i proprio database utente per l'istanza master di SQL Server.

## <a name="machine-learning-services"></a>Servizi di Machine learning

SQL Server servizi di machine learning sono una funzionalità aggiuntiva per il motore di database, utilizzato per l'esecuzione di codice Java, R e Python in SQL Server. Questa funzionalità si basa su framework di estendibilità di SQL Server, che consente di isolare i processi esterni dai processi del motore di core, ma si integra completamente con i dati relazionali come stored procedure, script T-SQL contenente le istruzioni di R o Python o Java, R o Codice Python che contiene di T-SQL.

Come parte di un cluster di big data di SQL Server, servizi machine learning saranno disponibili nell'istanza SQL Server master per impostazione predefinita. Ciò significa che dopo l'esecuzione di script esterni è abilitato nell'istanza di master di SQL Server, verrà è possibile eseguire Java, script R e Python con sp_execute_external_script.

### <a name="advantages-of-machine-learning-services-in-a-big-data-cluster"></a>Vantaggi dei servizi di machine learning in un cluster di big data

SQL Server 2019 semplifica per big data da unire ai dati dimensionali in genere archiviati nel database enterprise. Il valore dei big data aumenta notevolmente quando non è sufficiente nelle mani di parti di un'organizzazione, ma è anche incluso nei report, dashboard e le applicazioni. Allo stesso tempo, i data Scientist possono continuare a usare gli strumenti dell'ecosistema di Spark o HDFS e facile, hanno accesso in tempo reale ai dati nell'istanza master di SQL Server e nelle origini dati esterne accessibili _tramite_ il master di SQL Server istanza.

I cluster di SQL Server 2019 dei big data, è possibile eseguire altre con i data Lake enterprise. Gli analisti e sviluppatori di SQL Server è possibile:

* Compilare applicazioni che utilizzano i dati da data Lake enterprise.
* Motivo su tutti i dati con la query Transact-SQL.
* Utilizzare l'ecosistema di strumenti di SQL Server e applicazioni esistente per accedere e analizzare i dati aziendali.
* Ridurre la necessità per lo spostamento dei dati tramite la virtualizzazione dei dati e data mart.
* Continuare a usare Spark per scenari di big data.
* Compilare applicazioni aziendali intelligenti tramite Spark o SQL Server per il training dei modelli su data Lake.
* Rendere operativi i modelli nei database di produzione per ottenere prestazioni ottimali.
* Dati Stream direttamente in enterprise data mart per analitica in tempo reale.
* Esplorare i dati visivamente tramite un'analisi interattiva e strumenti di Business Intelligence.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere Panoramica riportata di seguito:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
