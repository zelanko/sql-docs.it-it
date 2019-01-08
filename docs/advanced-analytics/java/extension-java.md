---
title: Estensione del linguaggio Java in SQL Server 2019 - servizi di SQL Server Machine Learning
description: Installare, configurare e convalidare l'estensione del linguaggio Java su SQL Server 2019 per i sistemi Linux e Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/07/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a258573ff7506f2533c2f91edb5751cfd1121dc8
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431715"
---
# <a name="java-language-extension-in-sql-server-2019"></a>Estensione del linguaggio Java in SQL Server 2019 

A partire da SQL Server 2019 anteprima sia Windows che Linux, è possibile eseguire codice Java personalizzato nel [framework di estendibilità](../concepts/extensibility-framework.md) come componente aggiuntivo per l'istanza del motore di database. 

Il framework di estendibilità è un'architettura per l'esecuzione di codice esterno: Java (a partire in SQL Server 2019), [Python (a partire da SQL Server 2017)](../concepts/extension-python.md), e [R (a partire da SQL Server 2016)](../concepts/extension-r.md). L'esecuzione di codice è isolato da processi del motore di base, ma completamente integrato con l'esecuzione di query di SQL Server. Ciò significa che è possibile inserire i dati da qualsiasi query di SQL Server per il runtime esterno e utilizzare o rendere persistenti i risultati in SQL Server.

Come con qualsiasi estensione del linguaggio di programmazione, stored procedure di sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) è l'interfaccia per l'esecuzione di codice Java pre-compilato.

## <a name="prerequisites"></a>Prerequisiti

È necessaria un'istanza di anteprima di SQL Server 2019. Le versioni precedenti sono privi di integrazione di Java. 

Requisiti relativi alla versione Java variano tra Windows e Linux. Java Runtime Environment (JRE) è il requisito minimo, ma sono utili se è necessario il compilatore Java o i pacchetti di sviluppo JDK. Poiché il pacchetto JDK è tutto incluso, se si installa il pacchetto JDK, JRE non è più necessario.

| Sistema operativo | Versione di Java | Download JRE | Download di JDK |
|------------------|--------------|--------------|--------------|
| WINDOWS          | 1.10         | [JRE 10](https://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html) | [JDK 10](https://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)  |
| Linux            | 1.8          |  [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) | [JDK 8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  |  

In Linux, il **mssql-server-extensibility-java** pacchetto installa automaticamente questa versione 1.8 di JRE non è già installato. Gli script di installazione anche aggiungono il percorso JVM per una variabile di ambiente JAVA_HOME chiamata.

In Windows, si consiglia di installare il pacchetto JDK sotto l'impostazione predefinita /Program file / cartella se possibile. Configurazione aggiuntiva in caso contrario, è necessario concedere le autorizzazioni per file eseguibili. Per altre informazioni, vedere la [concedere le autorizzazioni (Windows)](#perms-nonwindows) sezione in questo documento.

> [!Note]
> Dato che Java è compatibile con le versioni precedenti, le versioni precedenti potrebbero funzionare, ma le versioni testate e supportate per questa versione CTP iniziale sono elencate nella tabella.

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>Installare in Linux

È possibile installare il [dal database e Java extension insieme](../../linux/sql-server-linux-setup-machine-learning.md#install-all), o aggiungere il supporto di Java a un'istanza esistente. Negli esempi seguenti aggiungere l'estensione di Java a un'installazione esistente.  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# USE install commands
sudo zypper install mssql-server-extensibility-java
```

Quando si installa **mssql-server-extensibility-java**, il pacchetto viene installato automaticamente 1.8 JRE se non è già installato. Aggiungerà anche il percorso della JVM a una variabile di ambiente JAVA_HOME chiamata.

Dopo aver completato l'installazione, il passaggio successivo consiste [configurare l'esecuzione di script esterni](#configure-script-execution).

> [!Note]
> In un dispositivo connesso a internet, le dipendenze dei pacchetti vengono scaricate e installate come parte dell'installazione del pacchetto principale. Per altre informazioni, tra cui il programma di installazione offline, vedere [installare SQL Server Machine Learning in Linux](../../linux/sql-server-linux-setup-machine-learning.md).

### <a name="grant-permissions-on-linux"></a>Concedere le autorizzazioni in Linux

Per fornire SQL Server con le autorizzazioni per eseguire le classi Java, è necessario impostare le autorizzazioni.

Per concedono autorizzazioni di lettura ed eseguire l'accesso per file jar di file o file di classe, eseguire il comando seguente **chmod** comando in ogni file di classe o con estensione jar. È consigliabile inserire i file di classe in un file jar quando si lavora con SQL Server. Per informazioni sulla creazione di un file jar, vedere [come creare un file con estensione jar](#create-jar).

```cmd
chmod ug+rx <MyJarFile.jar>
```
È inoltre necessario concedere le autorizzazioni mssql_satellite per il file con estensione jar o directory in lettura/esecuzione.

* Se si chiama il file di classe da SQL Server, mssql_satellite necessario leggere/eseguirà le autorizzazioni sul *ogni* directory nella gerarchia di cartelle, dalla radice fino all'elemento padre diretto.

* Se si chiama un file con estensione jar da SQL Server, è sufficiente per eseguire il comando sul file con estensione jar.

```cmd
chown mssql_satellite:mssql_satellite <directory>
```

```cmd
chown mssql_satellite:mssql_satellite <MyJarFile.jar>
```

<a name="install-on-windows"></a>

## <a name="install-on-windows"></a>Installare in Windows

1. [Eseguire il programma di installazione](../install/sql-machine-learning-services-windows-install.md) per installare SQL Server 2019.

2. Quando si arriva alla caratteristica di selezione, scegliere **Machine Learning Services (in-database)**. 

   Anche se l'integrazione di Java non viene fornito con librerie di machine learning, questa è l'opzione nel programma di installazione che fornisce il framework di estendibilità. Se si vuole, è possibile omettere R e Python.

3. Completamento installazione guidata e quindi continuare con le due attività.

### <a name="add-the-javahome-variable"></a>Aggiungere la variabile JAVA_HOME

JAVA_HOME è una variabile di ambiente che specifica il percorso dell'interprete Java. In questo passaggio, creare una variabile di ambiente di sistema per tale su Windows.

1. Trovare e copiare il percorso di installazione di JDK/JRE (ad esempio, c:\Programmi\Microsoft Files\Java\jdk-10.0.2).

  Nella versione CTP 2.0, impostare JAVA_HOME alla cartella base jdk funziona solo per Java 1.10. 

  Per Java 1.8, estendere il percorso per raggiungere il jvm.dll su Windows in JDK (ad esempio, "c:\Programmi\Microsoft Files\Java\jdk1.8.0_181\bin\server". In alternativa, è possibile puntare a una cartella di base di JRE: "C:\Programmi\Microsoft Files\Java\jre1.8.0_181".

2. Nel Pannello di controllo, aprire **sistema e sicurezza**aprire **System**, fare clic su **delle proprietà di sistema avanzate**.

3. Fare clic su **variabili di ambiente**.

4. Creare una nuova variabile di sistema per JAVA_HOME.

   ![Variabile di ambiente Java domestico](../media/java/env-variable-java-home.png "di installazione per Java")

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jdk-folder-windows-only"></a>Concedere l'accesso alla cartella JDK diverso (solo Windows)

È possibile ignorare questo passaggio se è installato JDK/JRE nella cartella predefinita. 

Per un'installazione di cartella diverso, eseguire la **icacls** comandi da un' *con privilegi elevati* riga per concedere l'accesso per il **SQLRUsergroup** e account del servizio SQL Server (in  **ALL_APPLICATION_PACKAGES**) per l'accesso a JVM e il classpath Java. I comandi verranno in modo ricorsivo concedere l'accesso a tutti i file e cartelle nel percorso di directory specificato.

#### <a name="sqlrusergroup-permissions"></a>SQLRUserGroup autorizzazioni

Per un'istanza denominata, aggiungere il nome dell'istanza per SQLRUsergroup (ad esempio, `SQLRUsergroupINSTANCENAME`).

```cmd
icacls "<PATH TO CLASS or JAR FILES>" /grant "SQLRUsergroup":(OI)(CI)RX /T
```

#### <a name="appcontainer-permissions"></a>Autorizzazioni di AppContainer

```cmd
icacls "PATH to JDK/JRE" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T
```

### <a name="add-the-jre-path-to-javahome"></a>Aggiungere il percorso JRE JAVA_HOME
È anche necessario aggiungere il percorso per l'ambiente JRE nella variabile di ambiente JAVA_HOME sistema. Se si dispone solo di un ambiente JRE installato, è possibile fornire il percorso della cartella JRE. Tuttavia, se si dispone di un pacchetto JDK installato, è necessario specificare il percorso completo alla JVM, nella cartella nel pacchetto JDK, JRE simile al seguente: "C:\Programmi\Microsoft Files\Java\jdk1.8.0_191\jre\bin\server".

Per creare una variabile di sistema, utilizzare Pannello di controllo > sistema e sicurezza > sistema per accedere **delle proprietà di sistema avanzate**. Fare clic su **variabili di ambiente** e quindi creare una nuova variabile di sistema per JAVA_HOME.

![Variabile di ambiente Java domestico](../media/java/env-variable-java-home.png "di installazione per Java")

<a name="configure-script-execution"></a>

## <a name="configure-script-execution"></a>Configurare l'esecuzione di script

A questo punto, si è quasi pronti per eseguire codice Java su Linux o Windows. Come ultimo passaggio, passare a SQL Server Management Studio o un altro strumento che esegue script Transact-SQL per consentire l'esecuzione di script esterni.

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="verify-installation"></a>Verificare l'installazione

Per verificare l'installazione è operativo, creare ed eseguire un' [applicazione di esempio](java-first-sample.md) usando il pacchetto JDK installato, il posizionamento dei file in classpath è configurato in precedenza.

## <a name="differences-in-ctp-20"></a>Differenze nella versione CTP 2.0

Se si ha già familiarità con i servizi di Machine Learning, il modello di autorizzazione e isolamento per le estensioni è stato modificato in questa versione. Per altre informazioni, vedere [differenze in un'installazione di servizi di SQL Server Machine 2019 Learning](../install/sql-machine-learning-services-ver15.md).

## <a name="limitations-in-ctp-20"></a>Limitazioni nella versione CTP 2.0

* Non può superare il numero di valori nei buffer di input e output `MAX_INT (2^31-1)` perché è questo il numero massimo di elementi che possono essere allocati in una matrice nel linguaggio.

* I parametri in di output [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) non sono supportati in questa versione.

* Nessun tipo di dati LOB supporto per i set di dati di input e output in questa versione. Visualizzare [tipi di dati di SQL Server e Java](java-sql-datatypes.md) per informazioni dettagliate su quali dati sono supportati in questa versione CTP.

* Lo streaming tramite il parametro sp_execute_external_script @r_rowsPerRead non è supportata in questa versione CTP.

* Partizionamento utilizzando il parametro sp_execute_external_script @input_data_1_partition_by_columns non è supportata in questa versione CTP.

<a name="create-jar"></a>

## <a name="how-to-create-a-jar-file-from-class-files"></a>Come creare un file con estensione jar dal file di classe

Passare alla cartella contenente il file di classe ed eseguire questo comando:

```cmd
jar -cf <MyJar.jar> *.class
```

Assicurarsi che il percorso **jar.exe** fa parte di una variabile di sistema path. In alternativa, specificare il percorso completo con estensione jar che può trovarsi sotto /bin nella cartella JDK: `C:\Users\MyUser\Desktop\jdk-10.0.2\bin\jar -cf <MyJar.jar> *.class`

## <a name="next-steps"></a>Passaggi successivi

+ [Come chiamare Java in SQL Server](howto-call-java-from-sql.md)
+ [Esempio di Java in SQL Server](java-first-sample.md)
+ [Tipi di dati Java e SQL Server](java-sql-datatypes.md)