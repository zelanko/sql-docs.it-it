---
title: Applicazioni di esempio del driver JDBC
description: Le applicazioni di esempio del driver JDBC per SQL Server illustrano varie funzionalità e procedure di programmazione valide eseguibili quando si usa il driver JDBC.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17479d32cd752650b4bfb1d03f5bc36ab52d8ca4
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915917"
---
# <a name="sample-jdbc-driver-applications"></a>Applicazioni di esempio del driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Con le applicazioni di esempio [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] vengono illustrate diverse funzionalità del driver JDBC. Illustrano inoltre le buone regole di programmazione a cui attenersi quando si usa il driver JDBC con un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Tutte le applicazioni di esempio sono contenute nei file di codice *.java che è possibile compilare ed eseguire nel computer locale e che si trovano in varie sottocartelle nel seguente percorso:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples
```

Negli argomenti di questa sezione viene descritto come configurare ed eseguire le applicazioni di esempio ed è inclusa una trattazione su ciò che è stato illustrato nelle applicazioni di esempio.

## <a name="in-this-section"></a>Contenuto della sezione

| Argomento                                                                            | Descrizione                                                                                                                                                                                                                                                             |
| -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Connessione e recupero dei dati](connecting-and-retrieving-data.md)              | Queste applicazioni di esempio illustrano come connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Vengono inoltre descritte le diverse modalità di recupero dei dati da un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. |
| [Uso dei tipi di dati &#40;JDBC&#41;](working-with-data-types-jdbc.md)        | Queste applicazioni di esempio illustrano come usare i metodi del tipo di dati del driver JDBC per utilizzare i dati in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                           |
| [Utilizzo dei set di risultati](working-with-result-sets.md)                          | Queste applicazioni di esempio illustrano come usare i set di risultati per elaborare i dati contenuti in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                         |
| [Utilizzo di dati di grandi dimensioni](working-with-large-data.md)                            | Queste applicazioni di esempio illustrano come usare il buffer adattivo per recuperare dati con valori di grandi dimensioni da un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senza l'overhead dei cursori server.                                                      |
| [Individuazione dati e classificazione SQL](data-discovery-classification-sample.md) | Questa applicazione di esempio dimostra come recuperare le informazioni di Individuazione dati e classificazione contenute in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un oggetto ResultSet usando il driver JDBC.                                         |

## <a name="see-also"></a>Vedere anche

[Panoramica del driver JDBC](overview-of-the-jdbc-driver.md)
