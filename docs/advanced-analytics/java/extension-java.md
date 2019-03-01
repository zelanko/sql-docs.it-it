---
title: Estensione del linguaggio Java in SQL Server 2019 - servizi di SQL Server Machine Learning
description: Installare, configurare e convalidare l'estensione del linguaggio Java su SQL Server 2019 per i sistemi Linux e Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a18886ea4daff3fb87853a556b67ad0562c2efd3
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017837"
---
# <a name="java-language-extension-in-sql-server-2019"></a>Estensione del linguaggio Java in SQL Server 2019 

A partire da SQL Server 2019 anteprima sia Windows che Linux, è possibile eseguire codice Java personalizzato nel [framework di estendibilità](../concepts/extensibility-framework.md) come componente aggiuntivo per l'istanza del motore di database. 

Il framework di estendibilità è un'architettura per l'esecuzione di codice esterno: Java (a partire in SQL Server 2019), [Python (a partire da SQL Server 2017)](../concepts/extension-python.md), e [R (a partire da SQL Server 2016)](../concepts/extension-r.md). L'esecuzione di codice è isolato da processi del motore di base, ma completamente integrato con l'esecuzione di query di SQL Server. Ciò significa che è possibile inserire i dati da qualsiasi query di SQL Server per il runtime esterno e utilizzare o rendere persistenti i risultati in SQL Server.

Come con qualsiasi estensione del linguaggio di programmazione, stored procedure di sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) è l'interfaccia per l'esecuzione di codice Java pre-compilato.

<a name="prerequisites"></a>

## <a name="prerequisites"></a>Prerequisiti

È necessaria un'istanza di anteprima di SQL Server 2019. Le versioni precedenti sono privi di integrazione di Java.

Java 8 è supportato. Java Runtime Environment (JRE) è il requisito minimo, ma sono utili se è necessario il compilatore Java o i pacchetti di sviluppo JDK. Poiché il pacchetto JDK è tutto incluso, se si installa il pacchetto JDK, JRE non è più necessario.

È possibile usare la distribuzione preferita di Java 8. Di seguito sono due distribuzioni suggerite:

| Distribuzione | Versione di Java | Sistemi operativi | JDK | JRE |
|-|-|-|-|-|
| [Oracle Java SE](https://www.oracle.com/technetwork/java/javase/downloads/index.html) | 8 | Windows e Linux | Yes | Yes |
| [Zulu OpenJDK](https://www.azul.com/downloads/zulu/) | 8 | Windows e Linux | Yes | No |

In Linux, il **mssql-server-extensibility-java** pacchetto viene installato automaticamente JRE 8 se non è già installato. Gli script di installazione anche aggiungono il percorso JVM per una variabile di ambiente JAVA_HOME chiamata.

In Windows, si consiglia di installare il pacchetto JDK sotto l'impostazione predefinita `/Program Files/` cartella se possibile. Configurazione aggiuntiva in caso contrario, è necessario concedere le autorizzazioni per file eseguibili. Per altre informazioni, vedere la [concedere le autorizzazioni (Windows)](#perms-nonwindows) sezione in questo documento.

> [!Note]
> Dato che Java è compatibile con le versioni precedenti, le versioni precedenti potrebbero funzionare, ma la versione supportata e testata per questa versione CTP iniziale è Java 8. 

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>Installare in Linux

È possibile installare il [dal database e Java extension insieme](../../linux/sql-server-linux-setup-machine-learning.md#install-all), o aggiungere il supporto di Java a un'istanza esistente. Negli esempi seguenti aggiungere l'estensione di Java a un'installazione esistente.  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# SUSE install commands
sudo zypper install mssql-server-extensibility-java
```

Quando si installa **mssql-server-extensibility-java**, il pacchetto viene installato automaticamente JRE 8 se non è già installato. Aggiungerà anche il percorso della JVM a una variabile di ambiente JAVA_HOME chiamata.

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

1. Verificare che sia installata una versione supportata di Java. Per altre informazioni, vedere la [prerequisiti](#prerequisites).

2. [Eseguire il programma di installazione](../install/sql-machine-learning-services-windows-install.md) per installare SQL Server 2019.

3. Quando si arriva alla caratteristica di selezione, scegliere **Machine Learning Services (in-database)**. 

   Anche se l'integrazione di Java non viene fornito con librerie di machine learning, questa è l'opzione nel programma di installazione che fornisce il framework di estendibilità. Se si vuole, è possibile omettere R e Python.

4. Completamento installazione guidata e quindi continuare con le due attività.

### <a name="add-the-javahome-variable"></a>Aggiungere la variabile JAVA_HOME

JAVA_HOME è una variabile di ambiente che specifica il percorso dell'interprete Java. In questo passaggio, creare una variabile di ambiente di sistema per tale su Windows.

1. Trovare e copiare il percorso del JDK/JRE (ad esempio, `C:\Program Files\Java\jdk1.8.0_201`).

    A seconda della distribuzione Java preferita, il percorso del JDK o JRE potrebbe essere diverso da quello nel percorso di esempio precedente.

2. Nel Pannello di controllo, aprire **sistema e sicurezza**aprire **System**, fare clic su **delle proprietà di sistema avanzate**.

3. Fare clic su **variabili di ambiente**.

4. Creare una nuova variabile di sistema per `JAVA_HOME` con il valore del percorso del JDK/JRE (trovato nel passaggio 1).

5. Riavviare [Launchpad](../concepts/extensibility-framework.md#launchpad).

    1. Aprire [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md).

    2. In servizi di SQL Server, fare doppio clic su Launchpad di SQL Server e selezionare **riavviare**.

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

## <a name="differences-in-ctp-23"></a>Differenze nella versione CTP 2.3

Se si ha già familiarità con i servizi di Machine Learning, il modello di autorizzazione e isolamento per le estensioni è stato modificato in questa versione. Per altre informazioni, vedere [differenze in un'installazione di servizi di SQL Server Machine 2019 Learning](../install/sql-machine-learning-services-ver15.md).

## <a name="limitations-in-ctp-23"></a>Limitazioni nella versione CTP 2.3

* Non può superare il numero di valori nei buffer di input e output `MAX_INT (2^31-1)` perché è questo il numero massimo di elementi che possono essere allocati in una matrice nel linguaggio.

* I parametri in di output [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) non sono supportati in questa versione.

* Lo streaming tramite il parametro sp_execute_external_script @r_rowsPerRead non è supportata in questa versione CTP.

* Partizionamento utilizzando il parametro sp_execute_external_script @input_data_1_partition_by_columns non è supportata in questa versione CTP.

<a name="create-jar"></a>

## <a name="how-to-create-a-jar-file-from-class-files"></a>Come creare un file con estensione jar dal file di classe

Passare alla cartella contenente il file di classe ed eseguire questo comando:

```cmd
jar -cf <MyJar.jar> *.class
```

Assicurarsi che il percorso **jar.exe** fa parte di una variabile di sistema path. In alternativa, specificare il percorso completo con estensione jar che può trovarsi sotto /bin nella cartella JDK: `C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class`

## <a name="next-steps"></a>Passaggi successivi

+ [Come chiamare Java in SQL Server](howto-call-java-from-sql.md)
+ [Esempio di Java in SQL Server](java-first-sample.md)
+ [Tipi di dati Java e SQL Server](java-sql-datatypes.md)