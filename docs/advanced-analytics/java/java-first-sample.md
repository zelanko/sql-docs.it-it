---
title: Esempio di Java e un'esercitazione per SQL Server 2019 - servizi di SQL Server Machine Learning
description: Eseguire il codice di esempio Java in SQL Server 2019 per informazioni sui passaggi per usare l'estensione del linguaggio Java con dati di SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 000318716b07f58e94bd5c482d9c349e5d4e5481
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473755"
---
# <a name="sql-server-regex-java-sample"></a>Esempio di espressione regolare Java SQL Server

In questo esempio illustra una classe Java che riceve due colonne (ID e il testo) da SQL Server e anche accetta come parametro di input un'espressione regolare. La classe restituisce due colonne in SQL Server (ID e il testo).

Per un testo specificato nella colonna di testo inviato alla classe Java, il codice controlla se l'espressione regolare specificata è soddisfatta e restituisce testo con l'ID originale. 

Questo particolare esempio Usa un'espressione regolare che controlla se un testo contiene la parola "Java" o "java".

## <a name="microsoft-extensibility-sdk-for-java-for-microsoft-sql-server"></a>Estendibilità di Microsoft SDK per Java per Microsoft SQL Server

 Nella versione CTP 2.5, si intende modificare la modalità di che implementazione di codice Java che usa l'estensione del linguaggio Java per comunicare con SQL Server. Ciò fornirà una migliore esperienza per gli sviluppatori durante l'interazione con SQL Server da Java.

È opportuno valutare il SDK come un'interfaccia di supporto, che renderà più facile implementare il codice Java in esecuzione su SQL Server.

> [!NOTE]
> L'introduzione del SDK è un enorme cambiamento da versioni CTP precedenti. Gli esempi precedenti era lavoro dovrà essere aggiornato per usare il SDK.

Per altre informazioni, vedere la [documentazione del SDK](java-sdk.md).

## <a name="prerequisites"></a>Prerequisiti

+ Istanza del motore di Database di SQL Server 2019 con il framework di estendibilità e il linguaggio di programmazione di estensione [in Windows](../install/sql-machine-learning-services-windows-install.md) oppure [in Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup). Per altre informazioni sulla configurazione di sistema, vedere [estensione del linguaggio Java in SQL Server 2019](extension-java.md). Per altre informazioni sui requisiti di codifica, vedere [come chiamare Java in SQL Server](howto-call-java-from-sql.md).

+ SQL Server Management Studio o Azure Data Studio per l'esecuzione di T-SQL.

+ Java SE Development Kit (JDK) 8 or JRE 8 on Windows or Linux.

+ [Estendibilità di Microsoft Java SDK per Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension) mssql-java-lang-extension.jar.

Compilazione dalla riga di comando usando **javac** è sufficiente per questa esercitazione.

## <a name="1---create-sample-data-in-a-sql-server-table"></a>1 - creare dati di esempio in una tabella di SQL Server

In primo luogo, creare e popolare un *testdata* table con **ID** e **testo** colonne. Connettersi a SQL Server ed eseguire lo script seguente per creare una tabella:

```sql
CREATE DATABASE javatest
GO
USE javatest
GO

-- Create table for test data
DROP TABLE IF exists testdata;
GO

CREATE TABLE testdata(
id int NOT NULL,
"text" nvarchar(100) NOT NULL)
GO

TRUNCATE TABLE testdata
GO

-- Insert data into test table
INSERT INTO testdata(id, "text") VALUES (1, 'This sentence contains java')
INSERT INTO testdata(id, "text") VALUES (2, 'This sentence does not')
INSERT INTO testdata(id, "text") VALUES (3, 'I love Java!')
GO
Select * FROM testdata
```

## <a name="2---class-regexsamplejava"></a>2 - classe RegexSample.java

Iniziare creando la classe principale.

In questo passaggio, creare una classe denominata **RegexSample.java** e copiare il codice Java seguente nel file.

Questa classe principale sta importando il SDK, il che significa che il file jar scaricato nel passaggio 1 deve essere individuabile da questa classe.

> [!NOTE]
> Si noti che questa classe Importa il pacchetto SDK di estensione Java.
Vedere l'articolo [estendibilità di Microsoft SDK per Java per Microsoft SQL Server](java-sdk.md) per altri dettagli.

```java
package pkg;

import com.microsoft.sqlserver.javalangextension.PrimitiveDataset;
import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionExecutor;
import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.ListIterator;
import java.util.regex.*;

public class RegexSample extends AbstractSqlServerExtensionExecutor {
    private Pattern expr;

    public RegexSample() {
        // Setup the expected extension version, and class to use for input and output dataset
        executorExtensionVersion = SQLSERVER_JAVA_LANG_EXTENSION_V1;
        executorInputDatasetClassName = PrimitiveDataset.class.getName();
        executorOutputDatasetClassName = PrimitiveDataset.class.getName();
    }
    
    public PrimitiveDataset execute(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Validate the input parameters and input column schema
        validateInput(input, params);

        int[] inIds = input.getIntColumn(0);
        String[] inValues = input.getStringColumn(1);
        int rowCount = inValues.length;

        String regexExpr = (String)params.get("regexExpr");
        expr = Pattern.compile(regexExpr);

        System.out.println("regex expression: " + regexExpr);

        // Lists to store the output data
        LinkedList<Integer> outIds = new LinkedList<Integer>();
        LinkedList<String> outValues = new LinkedList<String>();

        // Evaluate each row
        for(int i = 0; i < rowCount; i++) {
            if (check(inValues[i])) {
                outIds.add(inIds[i]);
                outValues.add(inValues[i]);
            }
        }

        int outputRowCount = outValues.size();

        int[] idOutputCol = new int[outputRowCount];
        String[] valueOutputCol = new String[outputRowCount];

        // Convert the list of output columns to arrays
        outValues.toArray(valueOutputCol);

        ListIterator<Integer> it = outIds.listIterator(0);
        int rowId = 0;

        System.out.println("Output data:");
        while (it.hasNext()) {
            idOutputCol[rowId] = it.next().intValue();

            System.out.println("ID: " + idOutputCol[rowId] + " Value: " + valueOutputCol[rowId]);
            rowId++;
        }

        // Construct the output dataset
        PrimitiveDataset output = new PrimitiveDataset();

        output.addColumnMetadata(0, "ID", java.sql.Types.INTEGER, 0, 0);
        output.addColumnMetadata(1, "Text", java.sql.Types.NVARCHAR, 0, 0);

        output.addIntColumn(0, idOutputCol, null);
        output.addStringColumn(1, valueOutputCol);

        return output;
    }

    private void validateInput(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Check for the regex expression input parameter
        if (params.get("regexExpr") == null) {
            throw new IllegalArgumentException("Input parameter 'regexExpr' is not found");
        }

        // The expected input schema should be at least 2 columns, (INTEGER, STRING)
        if (input.getColumnCount() < 2) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }

        // Check that the input column types are expected
        if (input.getColumnType(0) != java.sql.Types.INTEGER &&
                (input.getColumnType(1) != java.sql.Types.VARCHAR && input.getColumnType(1) == java.sql.Types.NVARCHAR )) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }
    }

    private boolean check(String text) {
        Matcher m = expr.matcher(text);

        return m.find();
    }
}
```

## <a name="3-compile-and-create-jar-file"></a>3 per compilare e creare file con estensione jar

È consigliabile che creerai classi e le dipendenze in file con estensione jar. La maggior parte degli IDE di Java, ad esempio Eclipse o IntelliJ la generazione di supporto file jar quando il progetto di compilazione/compilare. In questo esempio, è stato chiamato il file jar **regex.jar**.

Se si sta creando manualmente un file con estensione jar, è possibile seguire la procedura, vedere [come creare un file con estensione jar](extension-java.md#create-jar).

> [!NOTE]
> In questo esempio Usa i pacchetti, il che significa che il pacchetto "pkg" nella parte superiore della classe assicura che il codice compilato viene salvato in una sottocartella denominata "pkg". Questo viene automaticamente preso in considerazione se si usa un IDE, ma se si esegue manualmente la compilazione usando le classi **javac**, sarà necessario inserire il codice compilato nella cartella sub pkg manualmente.

## <a name="4---create-external-libraries"></a>4 - creare librerie esterne

La creazione di una libreria esterna di SQL Server hanno automaticamente accesso ai file con estensione jar e non è necessario impostare autorizzazioni speciali al classpath.

In questo esempio, è necessario creare due librerie esterne. Uno per il SDK e uno per l'esempio di espressione regolare Java.

1.  Scaricare [estendibilità di Microsoft SDK per Java per Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension) mssql-java-lang-extension.jar.

1. Creare una libreria esterna per il sdk

```sql
-- Create external library for the SDK
CREATE EXTERNAL LIBRARY sdk
FROM (CONTENT = '<path>/mssql-java-lang-extension.jar')
WITH (LANGUAGE = 'Java');
GO
```

3. Creare una libreria esterna per l'esempio di espressione regolare

```sql
-- Create external library for the regex sample
CREATE EXTERNAL LIBRARY regex
FROM (CONTENT = '<path>/regex.jar')
WITH (LANGUAGE = 'Java');
GO
```

## <a name="5---set-permissions-skip-if-you-performed-step-4"></a>5: impostare le autorizzazioni (Ignora se è stato eseguito il passaggio 4)

Questo passaggio non è necessario se si utilizzano librerie esterne. Il modo consigliato di consiste nel creare una libreria esterna da è con estensione jar.

Se non si desidera utilizzare librerie esterne, è necessario impostare le autorizzazioni necessarie. L'esecuzione di script ha esito positivo solo se l'identità del processo ha accesso al codice. È possibile trovare altre informazioni sull'impostazione delle autorizzazioni [qui](extension-java.md).

### <a name="on-linux"></a>In Linux

Concedere le autorizzazioni di lettura/esecuzione per il classpath per il **mssql_satellite** utente.

### <a name="on-windows"></a>In Windows

Concedere le autorizzazioni 'Read ed Execute' per **SQLRUserGroup** e il **tutti i pacchetti di applicazione** SID sulla cartella che contiene il codice Java compilato. 

L'intero albero deve avere le autorizzazioni, dalla radice all'ultima sub cartella padre. 
 
1. Fare clic sulla cartella (ad esempio, ' C:\myJavaCode'), scegliere **delle proprietà** > **sicurezza**.
2. Fare clic su **Modifica**.
3. Scegliere **Aggiungi**.
4. Nelle **selezionare gli utenti, Computer, account del servizio o gruppi**:
   + Fare clic su **tipi di oggetti** e assicurarsi che *principi di sicurezza incorporati* e *gruppi* siano selezionate.
   + Fare clic su **posizioni** per selezionare il nome del computer locale nella parte superiore dell'elenco.
5. Immettere **SQLRUserGroup**, controllare il nome e quindi fare clic su OK per aggiungere il gruppo.
6. Immettere **tutti i pacchetti di applicazione**, controllare il nome e quindi fare clic su OK per aggiungere. Se il nome non viene risolto, visitare di nuovo il passaggio di percorsi. Il SID è locale nel computer.

Assicurarsi che entrambe le identità di sicurezza dispone delle autorizzazioni 'Read ed Execute' per la cartella e una sottocartella "pkg".

<a name="call-method"></a>

## <a name="2---call-the-java-class"></a>2 - chiamare la classe Java

Per chiamare il codice Java da SQL Server, si creerà una stored procedure che chiama sp_execute_external_script. Nel parametro "script", verrà definito quale [pacchetto]. [classe] da chiamare. In questo esempio, la classe appartiene a un pacchetto chiamato **pkg** e un file di classe denominato **RegexSample.java**.

> [!NOTE]
>Il metodo da chiamare non viene definita. Per impostazione predefinita, il **eseguire** metodo verrà chiamato. Ciò significa che è necessario seguire l'interfaccia SDK e implementare un metodo execute della classe Java, se si desidera essere in grado di chiamare la classe da SQL Server.

```sql
/*
This stored procedure takes an input query (input dataset) and a regular expression and returns the rows that fulfilled the given regular expression. This sample uses a regular expression that checks if a text contains the word "Java" or "java" ([Jj]ava) 
*/

CREATE OR ALTER PROCEDURE [dbo].[java_regex] @expr nvarchar(200), @query nvarchar(400)
AS
BEGIN
--Call the Java program by giving the package.className in @script
--The method invoked in the Java code is always the "execute" method
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.RegexSample'
, @input_data_1 = @query
, @params = N'@regexExpr nvarchar(200)'
, @regexExpr = @expr
with result sets ((ID int, text nvarchar(100)));
END
GO

--Now execute the above stored procedure and provide the regular expression and an input query
EXECUTE [dbo].[java_regex] N'[Jj]ava', N'SELECT id, text FROM testdata'
GO
```

### <a name="results"></a>Risultati

Dopo avere eseguito la chiamata, è necessario ottenere un set di risultati con due righe della tabella.

![Esempio Java è dovuta](../media/java/java-sample-results.png "risultati di esempio")

### <a name="if-you-get-an-error"></a>Se si verifica un errore

+ Quando si compilano le classi, la sottocartella "pkg" deve contenere il codice compilato per tutte le tre classi.

+ Infine, se non si Usa librerie esterne, controllare le autorizzazioni sul *ogni* cartella dalla radice alla sottocartella "pkg", per garantire che le identità di sicurezza che esegue il processo esterno disponga dell'autorizzazione di lettura ed esecuzione del codice.

## <a name="next-steps"></a>Passaggi successivi

+ [Estendibilità di Microsoft SDK per Java per Microsoft SQL Server](java-sdk.md)
+ [Come chiamare Java in SQL Server](howto-call-java-from-sql.md)
+ [Estensioni di linguaggio in SQL Server](extension-java.md)
+ [Tipi di dati Java e SQL Server](java-sql-datatypes.md)
