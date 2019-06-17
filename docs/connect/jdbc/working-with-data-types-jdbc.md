---
title: Utilizzo di tipi di dati (JDBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 76af99170edeaca8f600d12955a6de2b09897548
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66783265"
---
# <a name="working-with-data-types-jdbc"></a>Utilizzo dei tipi di dati (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

La funzione principale di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è consentire agli sviluppatori Java di accedere a dati contenuti in database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A tale scopo, il driver JDBC consente di eseguire la conversione tra i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i tipi e gli oggetti del linguaggio Java.  
  
> [!NOTE]  
> Per informazioni dettagliate sui tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sui tipi di dati del driver JDBC, incluse le relative differenze e in che modo vengono convertiti in tipi di dati del linguaggio Java, vedere [Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).  
  
Per poter usare i tipi di dati di SQL Server, il driver JDBC offre i metodi get\<Type> e set\<Type> per le classi [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) e i metodi get\<Type> e update\<Type> per la classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md). Il metodo da adottare dipende dal tipo di dati che si sta utilizzando e dall'eventuale utilizzo di set di risultati o query.  
  
Negli argomenti di questa sezione viene descritto come usare i tipi di dati del driver JDBC per accedere ai dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nelle applicazioni Java.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Esempio di tipi di dati di base](../../connect/jdbc/basic-data-types-sample.md)|Viene descritto come usare i metodi di richiamo del set di risultati per recuperare i valori dei tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e in che modo usare i metodi di aggiornamento del set di risultati per aggiornare tali valori.|  
|[Esempio di tipo di dati SQLXML](../../connect/jdbc/sqlxml-data-type-sample.md)|Viene descritto come archiviare dati XML in un database relazionale, come recuperare i dati XML da un database e come analizzare i dati XML con il tipo di dati Java **SQLXML**.|  
|[Esempio di tipi di dati spaziali](../../connect/jdbc/spatial-data-types-sample.md)|Viene descritto come archiviare e recuperare i dati con tipi di dati spaziali 'Geometry' e 'Geography' di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del database con **Geometry** e **Geography** i tipi Java definiti dal Driver JDBC per Microsoft.|

## <a name="see-also"></a>Vedere anche

[Applicazioni di esempio del driver JDBC](../../connect/jdbc/sample-jdbc-driver-applications.md)  
