---
title: Utilizzo dei set di risultati | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d33dbebaad162feb77a4cbea8de33993fc79f14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956958"
---
# <a name="working-with-result-sets"></a>Utilizzo dei set di risultati

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Quando si usano i dati contenuti in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], un metodo di manipolazione dei dati consiste nell'uso di un set di risultati. [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] supporta l'uso dei set di risultati tramite l'oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md). Usando l'oggetto SQLServerResultSet, è possibile recuperare i dati restituiti da un'istruzione SQL o da una stored procedure, aggiornare i dati secondo le necessità e quindi inviare nuovamente i dati al database.  
  
L'oggetto SQLServerResultSet offre anche metodi per la navigazione nelle righe di dati, per il recupero o l'impostazione dei dati in esso contenuti, per la creazione di vari livelli di sensibilità alle modifiche nel database sottostante.  
  
> [!NOTE]  
> Per ulteriori informazioni sulla gestione dei set di risultati, inclusa la sensibilità alle modifiche, vedere [gestione dei set di risultati con il driver JDBC](../../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md).  
  
Negli argomenti della sezione vengono descritti vari modi di usare un set di risultati per manipolare i dati contenuti in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
| Argomento                                                                                           | Descrizione                                                                                                                                                                                             |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Esempio di recupero dei dati del set di risultati](../../../connect/jdbc/code-samples/retrieving-result-set-data-sample.md) | Descrive come usare un set di risultati per recuperare i dati da un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e visualizzarli.                                                         |
| [Esempio di modifica dei dati dei set di risultati](../../../connect/jdbc/code-samples/modifying-result-set-data-sample.md)   | Descrive come usare un set di risultati per inserire, recuperare e modificare i dati in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].                                                      |
| [Esempio di memorizzazione nella cache dei dati dei set di risultati](../../../connect/jdbc/code-samples/caching-result-set-data-sample.md)       | Descrive come usare il set di risultati per recuperare grandi quantità di dati da un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e per controllare come vengono memorizzati i dati nel client. |
  
## <a name="see-also"></a>Vedere anche  

[Applicazioni di esempio del driver JDBC](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
  
