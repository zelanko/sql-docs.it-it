---
title: Uso del driver JDBC per il miglioramento di prestazioni e affidabilità | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e1592499-b87b-45ee-bab8-beaba8fde841
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c71763fcd3d51138ac35cabd207cc39c268ceed
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027999"
---
# <a name="improving-performance-and-reliability-with-the-jdbc-driver"></a>Uso del driver JDBC per il miglioramento di prestazioni e affidabilità

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Uno degli aspetti dello sviluppo di applicazioni comune a tutte le applicazioni è l'esigenza costante di migliorare prestazioni e affidabilità. Le tecniche per raggiungere questo obiettivo con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sono numerose.  
  
Negli argomenti di questa sezione vengono descritte le varie tecniche per il miglioramento di prestazioni e affidabilità quando si utilizza il driver JDBC.  

## <a name="in-this-section"></a>Contenuto della sezione

|Argomento|Descrizione|  
|-----------|-----------------|  
|[Chiusura di oggetti quando non sono in uso](../../connect/jdbc/closing-objects-when-not-in-use.md)|Descrive l'importanza di chiudere gli oggetti del driver JDBC quando non sono più necessari.|  
|[Gestione delle dimensioni delle transazioni](../../connect/jdbc/managing-transaction-size.md)|Descrive le tecniche per migliorare le prestazioni delle transazioni.|  
|[Uso delle istruzioni e dei set di risultati](../../connect/jdbc/working-with-statements-and-result-sets.md)|Vengono descritte le tecniche per migliorare le prestazioni quando si utilizzano gli oggetti istruzione o ResultSet.|  
|[Uso del buffer adattivo](../../connect/jdbc/using-adaptive-buffering.md)|Viene descritta una caratteristica di buffer adattivo, progettata per recuperare qualsiasi tipo di dati con valori di grandi dimensioni senza l'overhead dei cursori server.|  
|[Colonne di tipo sparse](../../connect/jdbc/sparse-columns.md)|Viene illustrato il supporto delle colonne di tipo sparse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da parte del driver JDBC.|  
|[Memorizzazione nella cache dei metadati delle istruzioni preparate per il driver JDBC](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|Vengono illustrate le tecniche per migliorare le prestazioni con le query di istruzioni preparate.|
|[Uso dell'API di copia bulk per un'operazione di inserimento batch](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)|Viene descritto come abilitare l'API per la copia bulk per le operazioni di inserimento in batch e i relativi vantaggi.|

## <a name="see-also"></a>Vedere anche

[Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
