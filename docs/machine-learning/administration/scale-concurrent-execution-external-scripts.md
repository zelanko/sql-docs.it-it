---
title: Ridimensionare il numero di script simultanei
description: Configurare l'esecuzione di script R e Python paralleli o simultanei in un pool di account utente per ridimensionare Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 430af4eb1127ab5b924b2429e166f68e2dffa334
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "81118804"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>Ridimensionare l'esecuzione simultanea di script esterni in Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Informazioni sugli account di lavoro per Machine Learning Services per SQL Server e su come modificare la configurazione predefinita per ridimensionare il numero di esecuzioni simultanee di script esterni.

Come parte del processo di installazione per Machine Learning Services, viene creato un nuovo *pool di account utente* Windows per supportare l'esecuzione di attività da parte del servizio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]. Lo scopo di questi account di lavoro consiste nell'isolare l'esecuzione simultanea di script esterni da parte di utenti di SQL Server diversi.

> [!Note]
> In SQL Server 2019 **SQLRUserGroup** include un solo membro, che è ora il singolo account del servizio Launchpad di SQL Server, anziché più account di lavoro. Questo articolo descrive gli account di lavoro per SQL Server 2016 e 2017.

## <a name="worker-account-group"></a>Gruppo di account di lavoro

Il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un gruppo di account Windows per ogni istanza in cui viene installato e abilitato l'apprendimento automatico.

- In un'istanza predefinita il nome del gruppo è **SQLRUserGroup**. Il nome è lo stesso se si usa Python, R o entrambi.
- In un'istanza denominata il nome predefinito del gruppo ha un suffisso con il nome dell'istanza: ad esempio, **SQLRUserGroupNomeIstanza**.

Per impostazione predefinita, il pool di account utente contiene 20 account utente. Nella maggior parte dei casi, 20 account sono più che sufficienti per supportare le attività di apprendimento automatico, ma è possibile modificare il numero di account. Il numero massimo di account è 100.

- In un'istanza predefinita i singoli account sono denominati da **MSSQLSERVER01** a **MSSQLSERVER20**.
- Per un'istanza denominata il nome dei singoli account dipende dal nome dell'istanza: ad esempio da **NomeIstanza01** a **NomeIstanza20**.

Se più di un'istanza usa l'apprendimento automatico, il computer avrà più gruppi di utenti. Un gruppo non può essere condiviso tra istanze.

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>Numero degli account di lavoro

Per modificare il numero di utenti nel pool di account, è necessario modificare le proprietà del servizio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], come descritto di seguito.

Le password associate a ciascun account utente vengono generate in modo casuale, ma è possibile modificarle in un secondo momento, dopo la creazione degli account.

1. Aprire Gestione configurazione SQL Server e selezionare **Servizi di SQL Server**.
2. Fare doppio clic sul servizio Launchpad di SQL Server e arrestare il servizio, se è in esecuzione.
3.  Nella scheda **Servizio** verificare che la modalità di avvio sia impostata come automatica. Non è possibile avviare script esterni se Launchpad non è in esecuzione.
4.  Fare clic sulla scheda **Avanzate** e modificare il valore di **Conteggio degli utenti esterni**, se necessario. Questa impostazione controlla il numero di utenti SQL diversi che possono eseguire sessioni di esecuzione di script esterni simultaneamente. Il numero predefinito è 20 account. Il numero massimo di utenti è 100.
5. Facoltativamente, è possibile impostare l'opzione **Reimposta password utenti esterni** su _Sì_ se l'organizzazione ha criteri che richiedono la modifica delle password a intervalli regolari. In questo modo, le password crittografate gestite da Launchpad per gli account utente verranno rigenerate. Per altre informazioni, vedere [Applicazione dei criteri delle password](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy).
6.  Riavviare il servizio Launchpad.

## <a name="managing-workloads"></a>Gestione dei carichi di lavoro

Il numero di account in questo pool determina il numero di sessioni di esecuzione di script esterni che possono essere attive simultaneamente.  Per impostazione predefinita, vengono creati 20 account, ovvero 20 utenti diversi possono avere sessioni Python o R attive contemporaneamente. È possibile aumentare il numero di account di lavoro se si prevede di eseguire più di 20 script simultanei.

Quando lo stesso utente esegue simultaneamente più script esterni, tutte le sessioni eseguite dall'utente usano lo stesso account di lavoro. Ad esempio, un singolo utente può eseguire 100 script Python o R diversi simultaneamente, purché le risorse lo consentano, ma tutti gli script vengono eseguiti tramite un unico account di lavoro.

Il numero di account di lavoro che è possibile supportare e il numero di sessioni simultanee che un singolo utente può eseguire sono limitati solo dalle risorse del server. In genere, la memoria rappresenta il primo collo di bottiglia riscontrato quando si usa il runtime Python o R.

Le risorse che possono essere usate da script Python o R vengono controllate da SQL Server. È consigliabile monitorare l'utilizzo delle risorse mediante DMV di SQL Server o esaminare i contatori delle prestazioni sull'oggetto processo di Windows associato e modificare di conseguenza l'utilizzo della memoria del server. Con SQL Server Enterprise Edition è possibile allocare le risorse usate per l'esecuzione di script esterni configurando un [pool di risorse esterne](create-external-resource-pool.md).

## <a name="next-steps"></a>Passaggi successivi

- [Monitorare l'esecuzione di script Python ed R tramite report personalizzati in SQL Server Management Studio](../../machine-learning/administration/monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
- [Monitorare Machine Learning Services per SQL Server tramite DMV](../../machine-learning/administration/monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)