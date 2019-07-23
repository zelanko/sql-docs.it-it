---
title: Supporto dei dati XML | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: af528f507f39cde948ae269d58abb2c0d9dcce46
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004274"
---
# <a name="supporting-xml-data"></a>Supporto dei dati XML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile il tipo di dati **xml**, che consente di archiviare documenti e frammenti XML in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il tipo di dati **xml**,un tipo di dati predefinito di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è simile per alcuni aspetti ad altri tipi predefiniti, quali **int** e **varchar**. Come accade con altri tipi predefiniti, è possibile usare il tipo di dati **xml** come tipo di variabile, come tipo di parametro o come tipo restituito da una funzione oppure come tipo di colonna quando si crea una tabella; oppure nelle funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST e CONVERT. Nel driver JDBC, è possibile eseguire il mapping del tipo di dati **xml** come stringa, matrice di byte, flusso o oggetto CLOB, BLOB o SQLXML. Il mapping predefinito è come stringa.  
  
 Con il driver JDBC viene fornito il supporto per l'API di JDBC 4.0, in cui viene presentata l'interfaccia SQLXML. Tale interfaccia definisce i metodi per interagire e modificare i dati XML. **SQLXML** è un tipo di dati JDBC 4,0 e viene mappato al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo di dati **XML** . Per utilizzare il tipo di dati SQLXML nelle applicazioni, è necessario impostare il classpath in modo da includere il file sqljdbc4.jar. Se l'applicazione tenta di utilizzare il file sqljdbc3.jar durante l'accesso all'oggetto SQLXML o ai relativi metodi, verrà generata un'eccezione.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convalida sempre i dati XML prima di archiviarli nella colonna del database. Le applicazioni possono usare il tipo di dati **SQLXML**, poiché il driver JDBC ne esegue automaticamente il mapping al tipo di dati **xml**. Il supporto per **SQLXML** è disponibile in sqljdbc4.jar. Visualizzare [Requisiti di sistema per il driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) per l'elenco delle versioni JRE supportate da [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Gli argomenti di questa sezione descrivono l'interfaccia SQLXML e illustrano come programmare con il tipo di dati **SQLXML** usando i metodi dell'API JDBC.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Interfaccia SQLXML](../../connect/jdbc/sqlxml-interface.md)|Vengono descritti l'interfaccia SQLXML e i relativi metodi.|  
|[Programmazione con SQLXML](../../connect/jdbc/programming-with-sqlxml.md)|Descrive come usare i metodi dell'API [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] per archiviare e recuperare dati XML in e da un database relazionale con il tipo di dati Java **SQLXML**. Sono inoltre contenute informazioni sui tipi di oggetti SQLXML e vengono elencate importanti linee guida e limitazioni da prendere in considerazione quando si utilizzano oggetti SQLXML.|  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
