---
title: Esempio di lettura di dati di grandi dimensioni con una stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 58c76635-a117-4661-8781-d6cb231c5809
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cbf339845bd23f1beb4f5cd0f3b3a380689a3120
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956125"
---
# <a name="reading-large-data-with-stored-procedures-sample"></a>Esempio di lettura di dati di grandi dimensioni con una stored procedure

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Con questa applicazione di esempio di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] viene illustrato come recuperare un parametro OUT di grandi dimensioni da un stored procedure.

Il file di codice per questo esempio è denominato ExecuteStoredProcedure.java ed è disponibile nel seguente percorso:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisiti

Per eseguire questa applicazione di esempio, è necessario accedere al database di esempio di [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)], È anche necessario impostare il classpath in modo da includere il file con estensione jar mssql-jdbc. Per ulteriori informazioni su come impostare il classpath, vedere [utilizzo del driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> Con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sono inclusi file di libreria di classi mssql-jdbc da usare a seconda delle impostazioni Java Runtime Environment (JRE) preferite. Per altre informazioni su quale file JAR scegliere, vedere [Requisiti di sistema per il driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

Nell'esempio viene creata la stored procedure obbligatoria nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] di esempio:

## <a name="example"></a>Esempio

Nell'esempio seguente, mediante il codice di esempio viene eseguita una connessione al database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Tramite il codice di esempio vengono quindi creati i dati di esempio e viene aggiornata la tabella Production.Document utilizzando una query con parametri. Viene quindi ottenuta la modalità di buffer adattivo usando il metodo [getResponseBuffering](../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) della classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) e viene eseguita la stored procedure GetLargeDataValue. A partire da Microsoft JDBC Driver versione 2.0, il valore predefinito della proprietà di connessione responseBuffering è "adaptive".

Infine, tramite il codice di esempio vengono visualizzati i dati restituiti con i parametri OUT e viene illustrato come usare i metodi `mark` e `reset` sul flusso per rileggere qualsiasi parte dei dati.

[!code[JDBC#UsingAdaptiveBuffering2](../../connect/jdbc/codesnippet/Java/reading-large-data-with-_1_1.java)]

## <a name="see-also"></a>Vedere anche

[Utilizzo di dati di grandi dimensioni](../../connect/jdbc/working-with-large-data.md)
