---
title: Esempio di Java e un'esercitazione per SQL Server 2019 - servizi di SQL Server Machine Learning
description: Eseguire il codice di esempio Java in SQL Server 2019 per informazioni sui passaggi per usare l'estensione del linguaggio Java con dati di SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 86a379191033f49ab6a5d06ceda2d1ed7a747c12
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018037"
---
# <a name="sql-server-java-sample-walkthrough"></a>Procedura dettagliata di esempio Java di SQL Server

In questo esempio illustra una classe Java che riceve due colonne (ID e il testo) da SQL Server e restituisce due colonne in SQL Server (ID e ngram). Per una combinazione di stringa e un ID specificato, il codice genera le permutazioni di n-grammi (sottostringhe), restituendo le permutazioni insieme all'ID originale. La lunghezza del ngram è definita da un parametro inviato alla classe Java.

## <a name="prerequisites"></a>Prerequisiti

+ Istanza del motore di Database di SQL Server 2019 con il framework di estendibilità e il linguaggio di programmazione di estensione [in Windows](../install/sql-machine-learning-services-windows-install.md) oppure [in Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup). Per altre informazioni sulla configurazione di sistema, vedere [estensione del linguaggio Java in SQL Server 2019](extension-java.md). Per altre informazioni sui requisiti di codifica, vedere [come chiamare Java in SQL Server](howto-call-java-from-sql.md).

+ SQL Server Management Studio o un altro strumento per l'esecuzione di T-SQL.

+ Java SE Development Kit (JDK) 8 in Windows o Linux.

Compilazione dalla riga di comando usando **javac** è sufficiente per questa esercitazione. 

## <a name="1---load-sample-data"></a>1 - caricare i dati di esempio

In primo luogo, creare e popolare un *esamina* table con **ID** e **testo** colonne. Connettersi a SQL Server ed eseguire lo script seguente per creare una tabella:

```sql
DROP TABLE IF exists reviews;
GO
CREATE TABLE reviews(
    id int NOT NULL,
    "text" nvarchar(30) NOT NULL)

INSERT INTO reviews(id, "text") VALUES (1, 'AAA BBB CCC DDD EEE FFF')
INSERT INTO reviews(id, "text") VALUES (2, 'GGG HHH III JJJ KKK LLL')
INSERT INTO reviews(id, "text") VALUES (3, 'MMM NNN OOO PPP QQQ RRR')
GO
```

## <a name="2---class-ngramjava"></a>2 - classe Ngram.java

Iniziare creando la classe principale. Questo è il primo di tre classi.

In questo passaggio, creare una classe denominata **Ngram.java** e copiare il codice Java seguente nel file. 


```java
//We will package our classes in a package called pkg
//Packages are option in Java-SQL, but required for this sample.
package pkg;

import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Ngram {

    //Required: This is only required if you are passing data in @input_data_1
    //from SQL Server in sp_execute_external_script
    public static int[] inputDataCol1 = new int[1];
    public static String[] inputDataCol2 = new String[1];

    //Required: Input null map. Size just needs to be set to "1"
    public static boolean[][] inputNullMap = new boolean[1][1];

    //Required: Output data columns returned back to SQL Server
    public static int[] outputDataCol1;
    public static String[] outputDataCol2;

    //Required: Output null map. Is populated with true or false values 
    //to indicate nulls
    public static boolean[][] outputNullMap;

    //Optional: This is only required if parameters are passed with @params
    // from SQL Server in sp_execute_external_script
    // n is giving us the size of ngram substrings
    public static int param1;

    //Optional: The number of rows we will be returning
    public static int numberOfRows;

    //Required: Number of output columns returned
    public static short numberOfOutputCols;

    /*Java main method - Only for testing purposes outside of SQL Server
    public static void main(String... args) {
        //getNGrams();
    }*/

    //This is the method we will be calling from SQL Server
    public static void getNGrams() {

        System.out.println("inputDataCol1.length= "+ inputDataCol1.length);
        if (inputDataCol1.length == 0 ) {
            // TODO: Set empty return
            return;
        }
        //Using a stream to "loop" over the input data inputDataCol1.length. You can also use a for loop for this.
        final List<InputRow> inputDataSet = IntStream.range(0, inputDataCol1.length)
                .mapToObj(i -> new InputRow(inputDataCol1[i], inputDataCol2[i]))
                .collect(Collectors.toList());


        //Again, we are using a stream to loop over data
        final List<OutputRow> outputDataSet = inputDataSet.stream()
                // Generate ngrams of size n for each incoming string
                // Each invocation of ngrams returns a list. flatMap flattens
                // the resulting list-of-lists to a flat list.
                .flatMap(inputRow -> ngrams(param1, inputRow.text).stream().map(s -> new OutputRow(inputRow.id, s)))
                .collect(Collectors.toList());

        //Print the outputDataSet
        System.out.println(outputDataSet);

        //Set the number of rows and columns we will be returning
        numberOfOutputCols = 2;
        numberOfRows = outputDataSet.size();
        outputDataCol1 = new int[numberOfRows]; // ID column
        outputDataCol2 = new String[numberOfRows]; //The ngram column
        outputNullMap = new boolean[2][numberOfRows];// output null map

        //Since we don't have any null values, we will populate all values in the outputNullMap to false
        IntStream.range(0, numberOfRows).forEach(i -> {
            final OutputRow outputRow = outputDataSet.get(i);
            outputDataCol1[i] = outputRow.id;
            outputDataCol2[i] = outputRow.ngram;
            outputNullMap[0][i] = false;
            outputNullMap[1][i] = false;
        });
    }

    // Example: ngrams(3, "abcde") = ["abc", "bcd", "cde"].
    private static List<String> ngrams(int n, String text) {
        return IntStream.range(0, text.length() - n + 1)
                .mapToObj(i -> text.substring(i, i + n))
                .collect(Collectors.toList());
    }
}
```

## <a name="3---class-inputrowjava"></a>3 - classe InputRow.java

Creare una seconda classe denominata **InputRow.java**composto il codice seguente e salvato nello stesso percorso **Ngram.java**.

```java
package pkg;

//This object represents one input row
public class InputRow {
    public final int id;
    public final String text;

    public InputRow(final int id, final String text) {
        this.id = id;
        this.text = text;
    }
}
```

## <a name="4---class-outputrowjava"></a>4 - classe OutputRow.java

La terza e ultima classe è detta **OutputRow.java**. Copiare il codice e salvarlo come OutputRow.java nella stessa posizione come gli altri.

```java
package pkg;

//This object represents one output row
public class OutputRow {
    public final int id;
    public final String ngram;

    public OutputRow(final int id, final String ngram) {
        this.id = id;
        this.ngram = ngram;
    }

    @Override
    public String toString() { return id + ":" + ngram; }
}
```

## <a name="5---compile"></a>5 - compilazione

Dopo aver ottenuto le classi pronte, eseguire javac per compilarle in file "Class" (`javac Ngram.java InputRow.java OutputRow.java`). Si dovrebbero ottenere tre file Class per questo esempio (Ngram.class InputRow.class e OutputRow.class).

Inserire il codice compilato in una sottocartella denominata "pkg" nel percorso di classpath. Se si lavora in una workstation di sviluppo, questo passaggio è dove è copiare i file nel computer di SQL Server.

Il classpath è il percorso del codice compilato. Ad esempio, in Linux, se nel classpath è '/ home/myclasspath /', quindi i file Class devono essere in "/ home/myclasspath/pkg". Nello script di esempio nel passaggio 7, il percorso delle classi fornita nella finestra di sp_execute_external_script è ' / home/myclasspath /' (presupponendo che Linux). 

In Windows, è consigliabile usare una cartella relativamente superficiale struttura, una o due livelli, per semplificare le autorizzazioni. Ad esempio, il classpath potrebbe essere simile 'C:\myJavaCode' con una sottocartella denominata '\pkg' che contiene le classi compilate. 

Per altre informazioni sul classpath, vedere [CLASSPATH impostare](howto-call-java-from-sql.md#set-classpath). 

### <a name="using-jar-files"></a>Uso di file con estensione jar

Se si prevede di classi e le dipendenze in file con estensione jar del pacchetto, specificare il percorso completo del file con estensione jar nel parametro CLASSPATH sp_execute_external_script. Ad esempio, se il file jar viene chiamato 'ngram.jar', il CLASSPATH sarà ' / home/myclasspath/ngram.jar' in Linux.

## <a name="6---set-permissions"></a>6: impostare le autorizzazioni

L'esecuzione di script ha esito positivo solo se l'identità del processo ha accesso al codice. 

### <a name="on-linux"></a>In Linux

Concedere le autorizzazioni di lettura/esecuzione per il classpath per il **mssql_satellite** utente.

### <a name="on-windows"></a>In Windows

Concedere le autorizzazioni 'Read ed Execute' per **SQLRUserGroup** e il **tutti i pacchetti di applicazione** SID sulla cartella che contiene il codice Java compilato. 

L'intero albero deve avere le autorizzazioni, dalla radice padre e l'ultimo sottocartella. 
 
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

## <a name="7---call-getngrams"></a>7 - Call *getNgrams()*

Per chiamare il codice da SQL Server, specificare il metodo di Java **getNgrams()** nel parametro "script" di sp_execute_external_script. Questo metodo appartiene a un pacchetto denominato "pkg" e un file di classe denominato **Ngram.java**.

In questo esempio passa il parametro del percorso di classe per fornire il percorso dei file Java. Utilizza anche "params" per passare un parametro per la classe Java. Assicurarsi che tale classpath non superi i 30 caratteri. In caso affermativo, aumentare il valore nello script seguente.

+ In Linux, eseguire il codice seguente in SQL Server Management Studio o un altro strumento utilizzato per l'esecuzione di Transact-SQL. 

+ In Windows, modificare @myClassPath a N'C:\myJavaCode\' (presupponendo che è la cartella padre di \pkg) prima di eseguire la query in SQL Server Management Studio o un altro strumento.

```sql
DECLARE @myClassPath nvarchar(50)
DECLARE @n int 
--This is where you store your classes or jars.
--Update this to your own classpath
SET @myClassPath = N'/home/myclasspath/'
--This is the size of the ngram
SET @n = 3
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.Ngram.getNGrams'
, @input_data_1 = N'SELECT id, text FROM reviews'
, @parallel = 0
, @params = N'@CLASSPATH nvarchar(30), @param1 INT'
, @CLASSPATH = @myClassPath
, @param1 = @n
with result sets ((ID int, ngram varchar(20)))
GO
```

### <a name="results"></a>Risultati

Dopo avere eseguito la chiamata, si dovrebbe ottenere un set di risultati indicate le due colonne:

![Esempio Java è dovuta](../media/java/java-sample-results.png "risultati di esempio")

### <a name="if-you-get-an-error"></a>Se si verifica un errore

Escludere eventuali problemi correlati al classpath. 

+ Classpath deve includere la cartella padre e tutte le relative sottocartelle, ma non nella sottocartella "pkg". Mentre la sottocartella pkg devono essere presenti, lo ha non deve per essere nel classpath valore specificato nella stored procedure.

+ Nella sottocartella "pkg" deve contenere il codice compilato per tutte le tre classi.

+ La lunghezza del percorso di classe non può superare il valore dichiarato (`DECLARE @myClassPath nvarchar(50)`). In questo caso, il percorso risulta troncato per i primi 50 caratteri e non verrà caricato il codice compilato. È possibile eseguire un `SELECT @myClassPath` per controllare il valore. Aumentare la lunghezza, se non è sufficiente 50 caratteri. 

+ Infine, controllare le autorizzazioni *ogni* cartella dalla radice alla sottocartella "pkg", per garantire che le identità di sicurezza che esegue il processo esterno disponga dell'autorizzazione di lettura ed esecuzione del codice.

## <a name="see-also"></a>Vedere anche

+ [Come chiamare Java in SQL Server](howto-call-java-from-sql.md)
+ [Estensioni di linguaggio in SQL Server](extension-java.md)
+ [Tipi di dati Java e SQL Server](java-sql-datatypes.md)
