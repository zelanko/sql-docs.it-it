---
title: Utilizzo dei tipi di dati (JDBC) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee1e64794480346b1742b441437db95b8ae41456
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028290"
---
# <a name="working-with-data-types-jdbc"></a>Uso dei tipi di dati (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

La funzione principale di [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] è consentire agli sviluppatori Java di accedere a dati contenuti in database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A tale scopo, il driver JDBC consente di eseguire la conversione tra i tipi di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e i tipi e gli oggetti del linguaggio Java.  
  
> [!NOTE]  
> Per informazioni dettagliate sui tipi di dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e sui tipi di dati del driver JDBC, incluse le relative differenze e in che modo vengono convertiti in tipi di dati del linguaggio Java, vedere [Informazioni sui tipi di dati del driver JDBC](../../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).  
  
Per poter usare i tipi di dati di SQL Server, il driver JDBC offre i metodi get\<Type> e set\<Type> per le classi [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) e i metodi get\<Type> e update\<Type> per la classe [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md). Il metodo da adottare dipende dal tipo di dati che si sta utilizzando e dall'eventuale utilizzo di set di risultati o query.  
  
Negli argomenti di questa sezione viene descritto come usare i tipi di dati del driver JDBC per accedere ai dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nelle applicazioni Java.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
| Argomento                                                                         | Descrizione                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Esempio di tipi di dati di base](../../../connect/jdbc/code-samples/basic-data-types-sample.md)   | Viene descritto come usare i metodi di richiamo del set di risultati per recuperare i valori dei tipi di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e in che modo usare i metodi di aggiornamento del set di risultati per aggiornare tali valori.                                             |
| [Esempio di tipo di dati SQLXML](../../../connect/jdbc/code-samples/sqlxml-data-type-sample.md)   | Viene descritto come archiviare dati XML in un database relazionale, come recuperare i dati XML da un database e come analizzare i dati XML con il tipo di dati Java **SQLXML**.                                                                                   |
| [Esempio di tipi di dati spaziali](../../../connect/jdbc/code-samples/spatial-data-types-sample.md) | Viene descritto come archiviare i tipi di dati spaziali in SQL Server e come recuperare questi tipi da SQL Server. Viene inoltre illustrato come utilizzare le classi appena definite **Geometry** e **geography** dal driver, per la gestione dei riferimenti Java di questi tipi di oggetto. |
  
## <a name="see-also"></a>Vedere anche

[Applicazioni di esempio del driver JDBC](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
