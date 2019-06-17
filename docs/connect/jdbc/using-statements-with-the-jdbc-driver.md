---
title: Uso di istruzioni con il Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 12258f95bd08d4fa196557efa7a6acf4feaa0d8f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798542"
---
# <a name="using-statements-with-the-jdbc-driver"></a>Utilizzo delle istruzioni con il driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

È possibile usare [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] per operare con i dati in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in diversi modi. Il driver JDBC può essere utilizzato per eseguire istruzioni SQL nel database o per chiamare le stored procedure nel database, utilizzando sia parametri di input che di output. Il driver JDBC supporta inoltre le sequenze di escape SQL, i conteggi di aggiornamento, le chiavi generate automaticamente e l'esecuzione degli aggiornamenti in un'operazione batch.  
  
Il driver JDBC offre tre classi per il recupero dei dati da un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1. [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md): usata per l'esecuzione di istruzioni SQL senza parametri.  
  
2. [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md): (ereditata da SQLServerStatement), usata per l'esecuzione di istruzioni SQL compilate che possono contenere parametri IN.  
  
3. [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md): (ereditata da SQLServerPreparedStatement), usata per l'esecuzione di stored procedure che possono contenere parametri IN, parametri OUT o entrambi.  
  
 Negli argomenti di questa sezione viene illustrato come usare ciascuna delle tre classi di istruzioni per operare con i dati in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Contenuto della sezione  

| Argomento                                                                                                    | Descrizione                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Uso di istruzioni con SQL](../../connect/jdbc/using-statements-with-sql.md)                             | Viene descritto come usare le istruzioni SQL con il driver JDBC per operare con i dati in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    |
| [USo di istruzioni con stored procedure](../../connect/jdbc/using-statements-with-stored-procedures.md) | Viene descritto come usare le stored procedure con il driver JDBC per operare con i dati in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. |
| [Uso di più set di risultati](../../connect/jdbc/using-multiple-result-sets.md)                           | Viene descritto come utilizzare il driver JDBC per recuperare i dati da più set di risultati.                                                                       |
| [Uso delle sequenze di escape SQL](../../connect/jdbc/using-sql-escape-sequences.md)                           | Viene descritto come utilizzare le sequenze di escape SQL, quali i valori letterali di data e ora e le funzioni.                                                               |
| [Uso delle chiavi generate automaticamente](../../connect/jdbc/using-auto-generated-keys.md)                             | Viene descritto come utilizzare le chiavi generate automaticamente.                                                                                                     |
| [Esecuzione di operazioni batch](../../connect/jdbc/performing-batch-operations.md)                         | Viene descritto come utilizzare il driver JDBC per eseguire operazioni batch.                                                                                      |
| [Gestione delle istruzioni complesse](../../connect/jdbc/handling-complex-statements.md)                         | Viene descritto come utilizzare il driver JDBC per eseguire istruzioni complesse che consentono di eseguire varie attività e possono restituire diversi tipi di dati.               |
  
## <a name="see-also"></a>Vedere anche

[Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
