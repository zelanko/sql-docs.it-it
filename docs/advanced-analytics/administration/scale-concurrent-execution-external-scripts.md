---
title: Ridimensionare l'esecuzione simultanea di script esterni
description: Configurare l'esecuzione di script R e Python paralleli o simultanei in un pool di account utente per la scalabilità SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 262810be3ad1fd246c6f60383e28d456c6b79e08
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714335"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>Ridimensionare l'esecuzione simultanea di script esterni in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Informazioni sugli account di lavoro per SQL Server Machine Learning Services e su come modificare la configurazione predefinita per ridimensionare il numero di esecuzioni simultanee di script esterni.

Come parte del processo di installazione per Machine Learning Services, viene creato un nuovo *pool di account utente* di Windows per supportare l'esecuzione delle attività da parte del servizio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]. Lo scopo di questi account di lavoro è isolare l'esecuzione simultanea di script esterni da parte di utenti SQL Server diversi.

> [!Note]
> In SQL Server 2019, **SQLRUserGroup** dispone solo di un membro che è ora il singolo account del servizio launchpad di SQL Server invece di più account di lavoro. Questo articolo descrive gli account di lavoro per SQL Server 2016 e 2017.

## <a name="worker-account-group"></a>Gruppo account di lavoro

Un gruppo di account Windows viene creato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal programma di installazione di per ogni istanza in cui è installato e abilitato Machine Learning.

- In un'istanza predefinita il nome del gruppo è **SQLRUserGroup**. Il nome è lo stesso se si usa Python o R o entrambi.
- In un'istanza denominata il nome predefinito del gruppo ha un suffisso con il nome dell'istanza: ad esempio, **SQLRUserGroupNomeIstanza**.

Per impostazione predefinita, il pool di account utente contiene 20 account utente. Nella maggior parte dei casi 20 è più che adeguato per supportare le attività di Machine Learning, ma è possibile modificare il numero di account. Il numero massimo di account è 100.

- In un'istanza predefinita i singoli account sono denominati da **MSSQLSERVER01** a **MSSQLSERVER20**.
- Per un'istanza denominata il nome dei singoli account dipende dal nome dell'istanza: ad esempio da **NomeIstanza01** a **NomeIstanza20**.

Se più di un'istanza USA Machine Learning, il computer avrà più gruppi di utenti. Un gruppo non può essere condiviso tra più istanze.

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>Numero di account di lavoro

Per modificare il numero di utenti nel pool di account, è necessario modificare le proprietà del servizio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], come descritto di seguito.

Le password associate a ciascun account utente vengono generate in modo casuale, ma è possibile modificarle in un secondo momento, dopo la creazione degli account.

1. Aprire Gestione configurazione SQL Server e selezionare **Servizi di SQL Server**.
2. Fare doppio clic sul servizio Launchpad di SQL Server e arrestare il servizio, se è in esecuzione.
3.  Nella scheda **Servizio** verificare che la modalità di avvio sia impostata come automatica. Gli script esterni non possono essere avviati quando la finestra di avvio non è in esecuzione.
4.  Fare clic sulla scheda **Avanzate** e modificare il valore di **Conteggio degli utenti esterni**, se necessario. Questa impostazione controlla il numero di utenti SQL diversi che possono eseguire simultaneamente sessioni di script esterni. Il valore predefinito è 20 account. Il numero massimo di utenti è 100.
5. Facoltativamente, è possibile impostare l'opzione **Reimposta password utenti esterni** su _Sì_ se l'organizzazione ha criteri che richiedono la modifica delle password a intervalli regolari. In questo modo, le password crittografate gestite da Launchpad per gli account utente verranno rigenerate. Per altre informazioni, vedere [Applicazione dei criteri delle password](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy).
6.  Riavviare il servizio launchpad.

## <a name="managing-workloads"></a>Gestione dei carichi di lavoro

Il numero di account in questo pool determina il numero di sessioni di script esterni che possono essere attive contemporaneamente.  Per impostazione predefinita, vengono creati 20 account, vale a dire che 20 utenti diversi possono disporre di sessioni attive di Python o R alla volta. È possibile aumentare il numero di account di lavoro se si prevede di eseguire più di 20 script simultanei.

Quando lo stesso utente esegue più script esterni simultaneamente, tutte le sessioni eseguite da tale utente utilizzeranno lo stesso account di lavoro. Ad esempio, un singolo utente potrebbe avere 100 script Python o R diversi in esecuzione contemporaneamente, purché le risorse lo consentano, ma tutti gli script vengono eseguiti usando un unico account di lavoro.

Il numero di account di lavoro che è possibile supportare e il numero di sessioni simultanee che possono essere eseguite da un singolo utente sono limitati solo dalle risorse del server. In genere, la memoria è il primo collo di bottiglia che si verificherà quando si usa il runtime Python o R.

Le risorse che possono essere usate dagli script Python o R sono regolate dal SQL Server. È consigliabile monitorare l'utilizzo delle risorse mediante DMV di SQL Server o esaminare i contatori delle prestazioni sull'oggetto processo di Windows associato e modificare di conseguenza l'utilizzo della memoria del server. Se si dispone di SQL Server Enterprise edizione, è possibile allocare le risorse usate per l'esecuzione di script esterni configurando un [pool di risorse esterne](how-to-create-a-resource-pool.md).

## <a name="next-steps"></a>Passaggi successivi

- [Monitorare l'esecuzione di script Python e R usando report personalizzati in SQL Server Management Studio](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
- [Monitorare SQL Server Machine Learning Services mediante le viste a gestione dinamica (DMV)](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)