---
title: Esempio di grandi quantità di dati di lettura | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 658c9f61829f2ba979f2d3e877d17905040dee97
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66772491"
---
# <a name="reading-large-data-sample"></a>Esempio di lettura di dati di grandi dimensioni

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questa applicazione [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] di esempio illustra come recuperare il valore di una singola colonna di grandi dimensioni da un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando il metodo [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md).

Il file di codice per questo esempio, ReadLargeData.java, è disponibile nel percorso seguente:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisiti

Per eseguire questa applicazione di esempio, è necessario accedere al database di esempio di [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)], È anche necessario impostare il classpath in modo da includere il file con estensione jar mssql-jdbc. Per altre informazioni su come impostare il classpath, vedere [utilizza il Driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> Con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sono inclusi file di libreria di classi mssql-jdbc da usare a seconda delle impostazioni Java Runtime Environment (JRE) preferite. Per altre informazioni su quale file JAR scegliere, vedere [Requisiti di sistema per il driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Esempio

Nell'esempio seguente, mediante il codice di esempio viene eseguita una connessione al database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Tramite il codice di esempio vengono quindi creati i dati di esempio e viene aggiornata la tabella Production.Document utilizzando una query con parametri.

Viene anche illustrato come ottenere la modalità di buffer adattivo usando il metodo [getResponseBuffering](../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) della classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). A partire da Microsoft JDBC Driver versione 2.0, il valore predefinito della proprietà di connessione responseBuffering è "adaptive".

Quindi tramite un'istruzione SQL con l'oggetto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) il codice di esempio esegue l'istruzione SQL e posiziona i dati restituiti in un oggetto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).

Viene infine eseguita un'iterazione nelle righe di dati presenti nel set di risultati e viene usato il metodo [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) per accedere a una parte dei dati.

[!code[JDBC#UsingAdaptiveBuffering1](../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]

## <a name="see-also"></a>Vedere anche

[Utilizzo di dati di grandi dimensioni](../../connect/jdbc/working-with-large-data.md)
