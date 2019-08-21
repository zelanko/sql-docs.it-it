---
title: Applicazioni di esempio del driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ef5c2d71d398be52ebed2b69020e87d54818176
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028312"
---
# <a name="sample-jdbc-driver-applications"></a>Applicazioni di esempio del driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Con le applicazioni di esempio [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] vengono illustrate diverse funzionalità del driver JDBC. Illustrano inoltre le buone regole di programmazione a cui attenersi quando si usa il driver JDBC con un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
Tutte le applicazioni di esempio sono contenute nei file di codice *.java che è possibile compilare ed eseguire nel computer locale e che si trovano in varie sottocartelle nel seguente percorso:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples  
```

 Negli argomenti di questa sezione viene descritto come configurare ed eseguire le applicazioni di esempio ed è inclusa una trattazione su ciò che è stato illustrato nelle applicazioni di esempio.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
| Argomento                                                                                                                  | Descrizione                                                                                                                                                                                                                                                                   |
| ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Connessione e recupero dei dati](../../../connect/jdbc/code-samples/connecting-and-retrieving-data.md)                              | Queste applicazioni di esempio illustrano come connettersi a un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Vengono inoltre descritte le diverse modalità di recupero dei dati da un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. |
| [Uso dei tipi di dati &#40;JDBC&#41;](../../../connect/jdbc/code-samples/working-with-data-types-jdbc.md)                        | Queste applicazioni di esempio illustrano come usare i metodi del tipo di dati del driver JDBC per utilizzare i dati in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].                                                                                              |
| [Utilizzo dei set di risultati](../../../connect/jdbc/code-samples/working-with-result-sets.md)                                          | Queste applicazioni di esempio illustrano come usare i set di risultati per elaborare i dati contenuti in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].                                                                                                            |
| [Utilizzo di dati di grandi dimensioni](../../../connect/jdbc/code-samples/working-with-large-data.md)                                            | Queste applicazioni di esempio illustrano come usare il buffer adattivo per recuperare dati con valori di grandi dimensioni da un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] senza l'overhead dei cursori server.                                                         |
| [Individuazione dati e classificazione SQL](../../jdbc/code-samples/data-discovery-and-classification-sample.md) | In questa applicazione di esempio viene illustrato come recuperare le informazioni di individuazione e classificazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dei dati contenute in un database da un oggetto ResultSet utilizzando il driver JDBC.                                            |
  
## <a name="see-also"></a>Vedere anche

[Panoramica del driver JDBC](../../../connect/jdbc/overview-of-the-jdbc-driver.md)
