---
title: Informazioni sui tipi di dati del driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7802328d-4d23-4775-9573-4169b127d258
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8daea8b477be13dd7b267a17ddf5f960868f579
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027268"
---
# <a name="understanding-the-jdbc-driver-data-types"></a>Informazioni sui tipi di dati del driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] supporta l'uso di tipi di dati JDBC di base e avanzati in un'applicazione Java che usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come database.  
  
Il sistema dei tipi di JDBC consente di eseguire la conversione tra i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i tipi e gli oggetti del linguaggio Java. I tipi JDBC sono basati sui tipi SQL-92 e SQL-99. Il driver JDBC è conforme alla specifica JDBC ed è progettato per fornire il giusto equilibrio tra prevedibilità e flessibilità.  
  
Negli argomenti di questa sezione viene descritto come utilizzare i tipi di dati di base e avanzati e viene illustrato in che modo i tipi di dati possono essere convertiti in altri tipi di dati.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
| Argomento                                                                                                                                            | Descrizione                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Uso di tipi di dati di base](../../connect/jdbc/using-basic-data-types.md)                                                                           | Vengono descritti i tipi di dati JDBC di base. Sono inclusi esempi su come gestire i tipi di dati utilizzando set di risultati, query con parametri e stored procedure.                                                                                                        |
| [Configurazione della modalità di invio dei valori java.sql.Time al server](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md) | Viene descritto come il driver JDBC genera le date.                                                                                                                                                                                                                       |
| [Uso di tipi di dati avanzati](../../connect/jdbc/using-advanced-data-types.md)                                                                     | Vengono descritti i tipi di dati JDBC avanzati.                                                                                                                                                                                                                              |
| [Informazioni sulle differenze tra i tipi di dati](../../connect/jdbc/understanding-data-type-differences.md)                                                 | Vengono descritte le differenze tra i vari tipi di dati del driver JDBC.                                                                                                                                                                                                    |
| [Informazioni sulle conversioni dei tipi di dati](../../connect/jdbc/understanding-data-type-conversions.md)                                                 | Viene descritto in che modo viene gestita la conversione dei tipi di dati quando si utilizzano i metodi di richiamo e impostazione.                                                                                                                                                                                  |
| [Supporto per set di caratteri nazionali](../../connect/jdbc/national-character-set-support.md)                                                           | Viene descritto il supporto per i tipi di set di caratteri nazionali.                                                                                                                                                                                                          |
| [Supporto dei dati XML](../../connect/jdbc/supporting-xml-data.md)                                                                                 | Viene descritta l'interfaccia SQLXML. Descrive anche come leggere e scrivere dati XML da e in un database relazionale con il tipo di dati Java **SQLXML**.                                                                                                             |
| [Wrapper e interfacce](../../connect/jdbc/wrappers-and-interfaces.md)                                                                         | Tratta le interfacce che includono le costanti e i metodi specifici di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] che consentono a un server applicazioni di creare un proxy della classe. Tratta anche il supporto per l'interfaccia `java.sql.Wrapper`. |
  
## <a name="see-also"></a>Vedere anche

[Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
