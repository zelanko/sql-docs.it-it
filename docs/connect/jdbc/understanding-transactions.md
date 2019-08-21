---
title: Informazioni sulle transazioni | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d5a6caa9c9bf1766b59aa813719d1461b6ef1aa
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027345"
---
# <a name="understanding-transactions"></a>Informazioni sulle transazioni

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Le transazioni sono gruppi di operazioni combinate in unità di lavoro logiche. Vengono utilizzate per controllare e mantenere la consistenza e l'integrità di ogni azione di una transazione, nonostante gli errori che possono verificarsi nel sistema.

Con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], le transazioni possono essere locali o distribuite. Nelle transazioni possono inoltre essere utilizzati livelli di isolamento. Per ulteriori informazioni sui livelli di isolamento supportati dal driver JDBC per, vedere [informazioni sui livelli di isolamento](../../connect/jdbc/understanding-isolation-levels.md).

Le applicazioni devono controllare le transazioni tramite istruzioni Transact-SQL o i metodi forniti dal driver JDBC, ma non entrambi. L'utilizzo simultaneo di istruzioni Transact-SQL e dei metodi dell'API di JDBC nella stessa transazione potrebbe comportare problemi, tra cui l'impossibilità di eseguire il commit di una transazione quando previsto, oppure l'esecuzione del commit o del rollback di una transazione e l'avvio imprevisto di una nuova transazione oppure il verificarsi di eccezioni di tipo "Impossibile riprendere la transazione".

## <a name="using-local-transactions"></a>Uso delle transazioni locali

Una transazione viene considerata locale se è a fase singola e viene gestita direttamente dal database. Il driver JDBC supporta le transazioni locali usando vari metodi della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md), inclusi [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md), [commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) e [rollback](../../connect/jdbc/reference/rollback-method.md). Le transazioni locali vengono in genere gestite in modo esplicito dall'applicazione o in modo automatico dal server applicazioni Java Platform, Enterprise Edition (Java EE).

Nell'esempio seguente viene eseguita una transazione locale costituita da due istruzioni separate nel blocco `try`. Le istruzioni vengono eseguite sulla tabella Production.ScrapReason nel database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] e, se non vengono generate eccezioni, vengono sottoposte a commit. Il codice nel blocco `catch` esegue il rollback della transazione se viene generata un'eccezione.

[!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]

## <a name="using-distributed-transactions"></a>Uso di transazioni distribuite

Una transazione distribuita aggiorna dati su due o più database in rete conservando al contempo le importanti caratteristiche di atomicità, consistenza, isolamento e durata, ovvero le proprietà ACID, dell'elaborazione delle transazioni. Il supporto delle transazioni distribuite è stato aggiunto all'API JDBC nella specifica JDBC 2.0 Optional API. La gestione delle transazioni distribuite viene in genere eseguita automaticamente dalla gestione transazioni JTS (Java Transaction Service) in un ambiente server applicazioni Java EE. Tuttavia, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] supporta le transazioni distribuite con qualsiasi gestione transazioni conforme a JTA (Java Transaction API).

Il driver JDBC si integra perfettamente con [!INCLUDE[msCoName](../../includes/msconame_md.md)] Distributed Transaction Coordinator (MS DTC) per fornire un reale supporto delle transazioni distribuite con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. MS DTC è una funzionalità di gestione delle transazioni distribuite fornita da [!INCLUDE[msCoName](../../includes/msconame_md.md)] per i sistemi [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows. MS DTC si basa sulla collaudata tecnologia di elaborazione delle transazioni di [!INCLUDE[msCoName](../../includes/msconame_md.md)] per supportare caratteristiche XA quali il protocollo completo di commit distribuito a due fasi e il recupero delle transazioni distribuite.

Per ulteriori informazioni su come utilizzare le transazioni distribuite, vedere [informazioni sulle transazioni XA](../../connect/jdbc/understanding-xa-transactions.md).

## <a name="see-also"></a>Vedere anche

[Esecuzione di transazioni con il driver JDBC](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
