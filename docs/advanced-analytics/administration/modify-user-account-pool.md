---
title: Esecuzione simultanea di scalabilità di script esterni - servizi di SQL Server Machine Learning
description: Configurare simultanea o parallela esecuzione dello script R e Python in un pool di account utente per la scalabilità di SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 9f32e51122df8d2d13d6eada726a1a5e9bea82f0
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596812"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>Esecuzione simultanea di scalabilità di script esterni in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Come parte del processo di installazione di [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)], viene creato un nuovo *pool di account utente* Windows per supportare l'esecuzione delle attività tramite il servizio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]. Lo scopo di questi account di lavoro consiste nell'isolare l'esecuzione simultanea di script esterni da utenti SQL diversi.

Questo articolo descrive la configurazione predefinita e la capacità per gli account di lavoro e su come modificare la configurazione predefinita per ridimensionare il numero di esecuzione simultanea di script esterni in SQL Server Machine Learning Services.

## <a name="worker-account-group"></a>Gruppo di account di lavoro

Viene creato un gruppo di account Windows da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il programma di installazione per ogni istanza del computer in cui è installato e abilitato learning.

- In un'istanza predefinita il nome del gruppo è **SQLRUserGroup**. Il nome è lo stesso se si usa R o Python oppure entrambi.
- In un'istanza denominata il nome predefinito del gruppo ha un suffisso con il nome dell'istanza: ad esempio, **SQLRUserGroupNomeIstanza**.

Per impostazione predefinita, il pool di account utente contiene 20 account utente. Nella maggior parte dei casi, 20 è più che sufficienti per supportare attività di machine learning, ma è possibile modificare il numero di account. Il numero massimo di account è 100.

- In un'istanza predefinita i singoli account sono denominati da **MSSQLSERVER01** a **MSSQLSERVER20**.
- Per un'istanza denominata il nome dei singoli account dipende dal nome dell'istanza: ad esempio da **NomeIstanza01** a **NomeIstanza20**.

Se più di un'istanza Usa machine learning, il computer sarà necessario più gruppi di utenti. Un gruppo non possa essere condivisi tra istanze.

> [!Note]
> In SQL Server 2019, **SQLRUserGroup** ha solo un membro che è ora il singolo account di servizio Launchpad di SQL Server invece di più account di lavoro.

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>Numero di account di lavoro

Per modificare il numero di utenti nel pool di account, è necessario modificare le proprietà del servizio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], come descritto di seguito.

Le password associate a ciascun account utente vengono generate in modo casuale, ma è possibile modificarle in un secondo momento, dopo la creazione degli account.

1. Aprire Gestione configurazione SQL Server e selezionare **Servizi di SQL Server**.
2. Fare doppio clic sul servizio Launchpad di SQL Server e arrestare il servizio, se è in esecuzione.
3.  Nella scheda **Servizio** verificare che la modalità di avvio sia impostata come automatica. Impossibile avviare gli script esterni quando la finestra di avvio non è in esecuzione.
4.  Fare clic sulla scheda **Avanzate** e modificare il valore di **Conteggio degli utenti esterni**, se necessario. Questa impostazione controlla il numero di utenti SQL diversi possa eseguire script esterni sessioni contemporaneamente. Il valore predefinito è 20 account. Il numero massimo di utenti è 100.
5. Facoltativamente, è possibile impostare l'opzione **Reimposta password utenti esterni** su _Sì_ se l'organizzazione ha criteri che richiedono la modifica delle password a intervalli regolari. In questo modo, le password crittografate gestite da Launchpad per gli account utente verranno rigenerate. Per altre informazioni, vedere [Applicazione dei criteri delle password](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy).
6.  Riavviare il servizio Launchpad.

## <a name="managing-workloads"></a>Gestione dei carichi di lavoro

Il numero di account in questo pool determina il numero di sessioni di script esterni può essere attivo contemporaneamente.  Per impostazione predefinita, vengono creati 20 account, vale a dire che 20 utenti diversi possono avere R o Python sessioni attive alla volta. È possibile aumentare il numero di account di lavoro, se si prevede di eseguire script simultaneo di più di 20.

Quando lo stesso utente esegue simultaneamente più script esterni, tutte le sessioni vengono eseguite da tale utente utilizzare lo stesso account di lavoro. Un singolo utente, ad esempio, potrebbe essere 100 script R diversi in esecuzione contemporaneamente, purché le risorse lo consentano, ma tutti gli script verranno eseguito usando un singolo account di lavoro.

Il numero di account di lavoro che è possibile supportare e il numero di sessioni simultanee che è possibile eseguire un singolo utente, è limitata solo dalle risorse del server. In genere, la memoria rappresenta il primo collo di bottiglia che si incontra quando si usa il runtime di R.

Le risorse che possono essere utilizzate dagli script di Python o R sono controllate da SQL Server. È consigliabile monitorare l'utilizzo delle risorse mediante DMV di SQL Server o esaminare i contatori delle prestazioni sull'oggetto processo di Windows associato e modificare di conseguenza l'utilizzo della memoria del server. Se si dispone di SQL Server Enterprise Edition, è possibile allocare le risorse usate per l'esecuzione di script esterni tramite la configurazione di un' [pool di risorse esterne](how-to-create-a-resource-pool.md).

## <a name="see-also"></a>Vedere anche

Per altre informazioni sulla configurazione di capacità, vedere questi articoli:

- [Configurazione di SQL Server per R Services](../../advanced-analytics/r/sql-server-configuration-r-services.md)
- [Case study sulle prestazioni per R Services](../../advanced-analytics/r/performance-case-study-r-services.md)