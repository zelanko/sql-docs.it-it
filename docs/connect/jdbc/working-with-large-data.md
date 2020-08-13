---
title: Uso di dati di grandi dimensioni
description: Informazioni su come usare tipi di dati di grandi dimensioni in JDBC Driver per SQL Server in queste applicazioni di esempio.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09099ca9b8d007b52d47122d7be55d6fbef81301
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923287"
---
# <a name="working-with-large-data"></a>Uso di dati di grandi dimensioni

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Il driver JDBC fornisce supporto per la memorizzazione nel buffer adattiva, che consente di recuperare qualsiasi tipo di dati con valori di grandi dimensioni senza l'overhead dei cursori server. Grazie al buffering adattivo, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] può recuperare i risultati dell'esecuzione di istruzioni da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando questi sono necessari per l'applicazione e non tutti contemporaneamente. Quando l'applicazione non necessita più di accedere ai dati, questi vengono inoltre eliminati dal driver.

In [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] JDBC Driver versione 1.2 la modalità di buffering predefinita era "**full**". Se l'applicazione non impostava la proprietà di connessione "responseBuffering" su "**adaptive**" nelle proprietà di connessione oppure tramite il metodo [setResponseBuffering](reference/setresponsebuffering-method-sqlserverstatement.md) dell'oggetto [SQLServerStatement](reference/sqlserverstatement-class.md), il driver supportava la lettura dell'intero risultato dal server. Per ottenere il comportamento di buffering adattivo, l'applicazione doveva impostare esplicitamente la proprietà di connessione "responseBuffering" su "**adaptive**".

il valore **adaptive** è la modalità di buffering predefinita e il driver JDBC memorizza nel buffer la quantità minima possibile di dati quando necessario. Per altre informazioni sull'uso del buffer adattivo, vedere [Uso del buffer adattivo](using-adaptive-buffering.md).

 Gli argomenti in questa sezione descrivono vari modi per recuperare dati per valori di grandi dimensioni da un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="in-this-section"></a>Contenuto della sezione

| Argomento                                                                                                   | Descrizione                                                              |
| ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [Esempio di lettura di dati di grandi dimensioni](reading-large-data-sample.md)                                               | Descrive come utilizzare un'istruzione SQL per recuperare dati per valori di grandi dimensioni.       |
| [Esempio di lettura di dati di grandi dimensioni con una stored procedure](reading-large-data-with-stored-procedures-sample.md) | Descrive come recuperare un valore del parametro OUT CallableStatement di grandi dimensioni. |
| [Esempio di aggiornamento di dati di grandi dimensioni](updating-large-data-sample.md)                                             | Descrive come aggiornare dati per valori di grandi dimensioni in un database.                |

## <a name="see-also"></a>Vedere anche

[Applicazioni di esempio del driver JDBC](sample-jdbc-driver-applications.md)
