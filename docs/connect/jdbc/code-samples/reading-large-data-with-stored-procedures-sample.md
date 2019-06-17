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
manager: jroth
ms.openlocfilehash: eebd7b1b56f0c6b4dd1d9187be2393368d91bc24
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66769916"
---
# <a name="reading-large-data-with-stored-procedures-sample"></a>Esempio di lettura di dati di grandi dimensioni con una stored procedure

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Con questa applicazione di esempio di [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] viene illustrato come recuperare un parametro OUT di grandi dimensioni da un stored procedure.

Il file di codice per questo esempio è denominato ExecuteStoredProcedure.java ed è disponibile nel seguente percorso:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisiti

Per eseguire questa applicazione di esempio, è necessario accedere al database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)], Impostare anche il classpath in modo da includere il file con estensione mssql-jdbc jar. Per altre informazioni su come impostare il classpath, vedere [utilizza il Driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> Con [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sono inclusi file di libreria di classi mssql-jdbc da usare a seconda delle impostazioni Java Runtime Environment (JRE) preferite. Per altre informazioni su quale file JAR scegliere, vedere [Requisiti di sistema per il driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

Creare la stored procedure seguente nel database di esempio [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]:

```sql
CREATE PROCEDURE GetLargeDataValue
  (@Document_ID int,
   @Document_ID_out int OUTPUT,
   @Document_Title varchar(50) OUTPUT,  
   @Document_Summary nvarchar(max) OUTPUT)  

AS
BEGIN
   SELECT @Document_ID_out = DocumentID,
          @Document_Title = Title,  
          @Document_Summary = DocumentSummary
    FROM  Production.Document  
    WHERE DocumentID = @Document_ID  
END  
```

## <a name="example"></a>Esempio

Nell'esempio seguente, mediante il codice di esempio viene eseguita una connessione al database [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Tramite il codice di esempio vengono quindi creati i dati di esempio e viene aggiornata la tabella Production.Document utilizzando una query con parametri. Viene quindi ottenuta la modalità di buffer adattivo usando il metodo [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) della classe [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) e viene eseguita la stored procedure GetLargeDataValue. A partire da Microsoft JDBC Driver versione 2.0, il valore predefinito della proprietà di connessione responseBuffering è "adaptive".

Infine, tramite il codice di esempio vengono visualizzati i dati restituiti con i parametri OUT e viene illustrato come usare i metodi `mark` e `reset` sul flusso per rileggere qualsiasi parte dei dati.

[!code[JDBC#UsingAdaptiveBuffering2](../../../connect/jdbc/codesnippet/Java/reading-large-data-with-_1_1.java)]

## <a name="see-also"></a>Vedere anche

[Utilizzo di dati di grandi dimensioni](../../../connect/jdbc/code-samples/working-with-large-data.md)
