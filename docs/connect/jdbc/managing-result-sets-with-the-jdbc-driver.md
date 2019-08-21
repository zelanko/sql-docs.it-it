---
title: Gestione dei set di risultati con il driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9ed5ad41-22e0-4e4a-8a79-10512db60d50
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 273a03e088036057f6d7b31c98074391138de07e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027915"
---
# <a name="managing-result-sets-with-the-jdbc-driver"></a>Gestione dei set di risultati con il driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Il set di risultati è un oggetto che rappresenta un set di dati restituito da un'origine dati, in genere come risultato di una query. Il set di risultati contiene righe e colonne con gli elementi di dati richiesti e per spostarsi al suo interno viene utilizzato un cursore. Un set di risultati può essere aggiornabile, ovvero può essere modificato e le modifiche inserite nell'origine dati originale. Il set di risultati può inoltre disporre di vari livelli di sensibilità alle modifiche nell'origine dati sottostante.  
  
 Il tipo di set di risultati è determinato al momento della creazione dell'istruzione, ovvero quando viene effettuata una chiamata al metodo [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). La finalità del set di risultati è di fornire alle applicazioni Java una rappresentazione utilizzabile dei dati del database, in genere con i metodi digitati per il richiamo e l'impostazione degli elementi di dati del set di risultati.  
  
 Nell'esempio seguente basato sul database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] viene creato un set di risultati mediante la chiamata al metodo [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) della classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). I dati del set di risultati vengono quindi visualizzati usando il metodo [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
 [!code[JDBC#ManagingResultSets1](../../connect/jdbc/codesnippet/Java/managing-result-sets-with-t_1.java)]  
  
 Negli argomenti di questa sezione vengono descritti i diversi aspetti dell'utilizzo del set di risultati, compresi tipi di cursore, concorrenza e blocchi a livello di riga.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Informazioni sui tipi di cursore](../../connect/jdbc/understanding-cursor-types.md)|Vengono descritti i diversi tipi di cursore supportati da [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].|  
|[Informazioni sul controllo della concorrenza](../../connect/jdbc/understanding-concurrency-control.md)|Viene descritto il supporto fornito dal driver JDBC per il controllo della concorrenza.|  
|[Informazioni sul blocco delle righe](../../connect/jdbc/understanding-row-locking.md)|Viene descritto in che modo il driver JDBC supporta i blocchi a livello di riga.|  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
