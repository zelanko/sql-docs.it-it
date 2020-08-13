---
title: Uso dei tipi di dati (JDBC)
description: Informazioni su come usare i tipi di dati in JDBC Driver per SQL Server tramite queste applicazioni di esempio.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6994e7ce587cf72d7879c79604cbe3c68873ddf0
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923284"
---
# <a name="working-with-data-types-jdbc"></a>Uso dei tipi di dati (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

La funzione principale di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è consentire agli sviluppatori Java di accedere a dati contenuti in database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A tale scopo, il driver JDBC consente di eseguire la conversione tra i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i tipi e gli oggetti del linguaggio Java.

> [!NOTE]
> Per informazioni dettagliate sui tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sui tipi di dati del driver JDBC, incluse le relative differenze e in che modo vengono convertiti in tipi di dati del linguaggio Java, vedere [Informazioni sui tipi di dati del driver JDBC](understanding-the-jdbc-driver-data-types.md).

Per usare i tipi di dati di SQL Server, JDBC Driver fornisce metodi get\<Type> e set\<Type> per le classi [SQLServerPreparedStatement](reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](reference/sqlservercallablestatement-class.md) e metodi get\<Type> e update\<Type> per la classe [SQLServerResultSet](reference/sqlserverresultset-class.md). Il metodo da adottare dipende dal tipo di dati che si sta utilizzando e dall'eventuale utilizzo di set di risultati o query.

Negli argomenti di questa sezione viene descritto come usare i tipi di dati del driver JDBC per accedere ai dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nelle applicazioni Java.

## <a name="in-this-section"></a>Contenuto della sezione

|Argomento|Descrizione|
|-----------|-----------------|
|[Esempio di tipi di dati di base](basic-data-types-sample.md)|Viene descritto come usare i metodi di richiamo del set di risultati per recuperare i valori dei tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e in che modo usare i metodi di aggiornamento del set di risultati per aggiornare tali valori.|
|[Esempio di tipo di dati SQLXML](sqlxml-data-type-sample.md)|Viene descritto come archiviare dati XML in un database relazionale, come recuperare i dati XML da un database e come analizzare i dati XML con il tipo di dati Java **SQLXML**.|
|[Esempio di tipi di dati spaziali](spatial-data-types-sample.md)|Viene descritto come archiviare e recuperare dati con i tipi di dati spaziali 'Geometry' e 'Geography' del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con i tipi Java **Geometry** e **Geography** definiti dal driver Microsoft JDBC.|

## <a name="see-also"></a>Vedere anche

[Applicazioni di esempio del driver JDBC](sample-jdbc-driver-applications.md)
