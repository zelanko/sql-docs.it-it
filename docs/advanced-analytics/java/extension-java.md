---
title: Estensione del linguaggio Java in SQL Server 2019 - estensioni del linguaggio SQL Server
description: Installare, configurare e convalidare l'estensione del linguaggio Java su SQL Server 2019 per i sistemi Linux e Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: db57689227445b0f50d6ff59fbf81e1d84ecacdb
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775493"
---
# <a name="java-language-extension-in-sql-server-2019"></a>Estensione del linguaggio Java in SQL Server 2019 

A partire da SQL Server 2019 anteprima sia Windows che Linux, è possibile eseguire codice Java personalizzato usando il [framework di estendibilità](../concepts/extensibility-framework.md) come componente aggiuntivo per l'istanza del motore di database.

Il framework di estendibilità è un'architettura per l'esecuzione di codice esterno: Java (a partire in SQL Server 2019), [Python (a partire da SQL Server 2017)](../concepts/extension-python.md), e [R (a partire da SQL Server 2016)](../concepts/extension-r.md). L'esecuzione di codice è isolata dai processi del motore di base, ma completamente integrato con l'esecuzione di query di SQL Server. Ciò significa che è possibile inserire i dati da qualsiasi query di SQL Server per il runtime esterno (Java) e utilizzare o rendere persistenti i risultati in SQL Server.

Come con qualsiasi estensione del linguaggio di programmazione, stored procedure di sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) è l'interfaccia per l'esecuzione di codice Java pre-compilato.

<a name="prerequisites"></a>

## <a name="prerequisites"></a>Prerequisiti

È necessaria un'istanza di anteprima di SQL Server 2019. Le versioni precedenti non è l'integrazione di Java.

Java 8 è attualmente la versione supportata. Le versioni più recenti, come Java, 11, dovrebbe con l'estensione del linguaggio, ma non è attualmente supportata. Java Runtime Environment (JRE) è il requisito minimo, ma è utile se è necessario il compilatore Java e i pacchetti di sviluppo. Poiché il pacchetto JDK è tutto incluso, se si installa il pacchetto JDK, JRE non è più necessario.

È possibile usare la distribuzione preferita di Java 8. Di seguito sono due distribuzioni suggerite:

| Distribuzione | Versione di Java | Sistemi operativi | JDK | JRE |
|-|-|-|-|-|
| [Oracle Java SE](https://www.oracle.com/technetwork/java/javase/downloads/index.html) | 8 | Windows e Linux | Yes | Yes |
| [Zulu OpenJDK](https://www.azul.com/downloads/zulu/) | 8 | Windows e Linux | Yes | No |

In Linux, attualmente le **mssql-server-extensibility-java** pacchetto viene installato automaticamente JRE 8 se non è già installato. Gli script di installazione, inoltre, aggiungere il percorso JVM per una variabile di ambiente denominata riportato.

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

Quando si installa **mssql-server-extensibility-java**, il pacchetto viene installato automaticamente JRE 8 se non è già installato. Aggiungerà anche il percorso JVM per una variabile di ambiente denominata riportato.

Dopo aver completato l'installazione, il passaggio successivo consiste [configurare l'esecuzione di script esterni](#configure-script-execution).

> [!Note]
> In un dispositivo connesso a internet, le dipendenze dei pacchetti vengono scaricate e installate come parte dell'installazione del pacchetto principale. Per altre informazioni, tra cui il programma di installazione offline, vedere [installare SQL Server Machine Learning in Linux](../../linux/sql-server-linux-setup-machine-learning.md).

### <a name="grant-permissions-on-linux"></a>Concedere le autorizzazioni in Linux

Non è necessario eseguire questo passaggio se si utilizzano librerie esterne. Il modo consigliato di utilizza librerie esterne. Per informazioni sulla creazione di una libreria esterna dal file con estensione jar, vedere [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)

Se non si Usa librerie esterne, è necessario fornire a SQL Server le autorizzazioni per eseguire le classi Java in un file jar.

Per concedono autorizzazioni di lettura ed eseguire l'accesso a un file con estensione jar, eseguire il comando seguente **chmod** comando sul file con estensione jar. È consigliabile inserire sempre i file di classe in un file jar quando si lavora con SQL Server. Per informazioni sulla creazione di un file jar, vedere [come creare un file con estensione jar](#create-jar).

```cmd
chmod ug+rx <MyJarFile.jar>
```

È inoltre necessario concedere le autorizzazioni mssql_satellite il file jar in lettura/esecuzione.

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

### <a name="add-the-jrehome-variable"></a>Aggiungere la variabile riportato

Riportato è una variabile di ambiente di sistema che specifica il percorso dell'interprete Java. In questo passaggio, creare una variabile di ambiente di sistema per tale su Windows.

1. Trovare e copiare il percorso della home directory JRE (ad esempio, `C:\Program Files\Zulu\zulu-8\jre\`).

    A seconda della distribuzione Java preferita, il percorso del JDK o JRE potrebbe essere diverso da quello nel percorso di esempio precedente.
    Anche se si dispone di un pacchetto JDK installato, è spesso tempi verrà ottenere una sottocartella JRE come parte dell'installazione, quindi puntare alla cartella jre in questo caso.
    Java extension tenterà di caricare il jvm.dll dal percorso % JRE_HOME%\bin\server.

2. Nel Pannello di controllo, aprire **sistema e sicurezza**aprire **System**, fare clic su **delle proprietà di sistema avanzate**.

3. Fare clic su **variabili di ambiente**.

4. Creare una nuova variabile di sistema per `JRE_HOME` con il valore del percorso del JDK/JRE (trovato nel passaggio 1).

5. Riavviare [Launchpad](../concepts/extensibility-framework.md#launchpad).

    1. Aprire [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md).

    2. In servizi di SQL Server, fare doppio clic su Launchpad di SQL Server e selezionare **riavviare**.

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jre-folder-windows-only"></a>Concedere l'accesso alla cartella JRE non predefinito (solo Windows)

Se nel file di programma non è stato installato il pacchetto JDK o JRE, è necessario eseguire la procedura seguente. Eseguire la **icacls** comandi da un *con privilegi elevati* riga per concedere l'accesso per il **SQLRUsergroup** e account del servizio SQL Server (in **ALL_APPLICATION_ PACCHETTI**) per l'accesso a JRE. I comandi verranno in modo ricorsivo concedere l'accesso a tutti i file e cartelle nel percorso di directory specificato.

#### <a name="sqlrusergroup-permissions"></a>SQLRUserGroup autorizzazioni

Per un'istanza denominata, aggiungere il nome dell'istanza per SQLRUsergroup (ad esempio, `SQLRUsergroupINSTANCENAME`).

```cmd
icacls "<PATH to JRE>" /grant "SQLRUsergroup":(OI)(CI)RX /T
```

È possibile ignorare questo passaggio se è installato JDK/JRE nella cartella predefinita nella cartella programmi in Windows.

#### <a name="appcontainer-permissions"></a>Autorizzazioni di AppContainer

```cmd
icacls "PATH to JRE" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T
```

<a name="configure-script-execution"></a>

## <a name="configure-script-execution"></a>Configurare l'esecuzione di script

A questo punto, si è quasi pronti per eseguire codice Java su Linux o Windows. Come ultimo passaggio, passare a SQL Server Management Studio, Azure data studio, CMD SQL o un altro strumento che consente di eseguire script Transact-SQL per consentire l'esecuzione di script esterni.

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="verify-installation"></a>Verificare l'installazione

Per verificare l'installazione è operativo, creare ed eseguire un' [applicazione di esempio](java-first-sample.md) tramite il Runtime di Java appena installato e aggiunto a riportato.

## <a name="differences-in-ctp-25"></a>Differenze nella versione CTP 2.5

Se si ha già familiarità con i servizi di Machine Learning, il modello di autorizzazione e isolamento per le estensioni è stato modificato in questa versione. Per altre informazioni, vedere [differenze in un'installazione di servizi di SQL Server Machine 2019 Learning](../install/sql-machine-learning-services-ver15.md).

## <a name="limitations-in-ctp-25"></a>Limitazioni nella versione CTP 2.5

* Non può superare il numero di valori nei buffer di input e output `MAX_INT (2^31-1)` perché è questo il numero massimo di elementi che possono essere allocati in una matrice nel linguaggio.

* I parametri in di output [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) non sono supportati in questa versione.

* Lo streaming tramite il parametro sp_execute_external_script @r_rowsPerRead non è supportata in questa versione CTP.

* Partizionamento utilizzando il parametro sp_execute_external_script @input_data_1_partition_by_columns non è supportata in questa versione CTP.

<a name="create-jar"></a>

## <a name="how-to-create-a-jar-file-from-class-files"></a>Come creare un file con estensione jar dal file di classe

È consigliabile riunire sempre i file di classe in un file jar durante l'esecuzione da SQL Server.
Per creare un file jar dal file di classe, passare alla cartella contenente il file di classe ed eseguire questo comando:

```cmd
jar -cf <MyJar.jar> *.class
```

Assicurarsi che il percorso **jar.exe** fa parte di una variabile di sistema path. In alternativa, specificare il percorso completo con estensione jar che può trovarsi sotto /bin nella cartella JDK: `C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class`

## <a name="next-steps"></a>Passaggi successivi

+ [Come chiamare Java in SQL Server](howto-call-java-from-sql.md)
+ [Esempio di Java in SQL Server](java-first-sample.md)
+ [Estendibilità di Microsoft SDK per Java per Microsoft SQL Server](java-sdk.md)
+ [Tipi di dati Java e SQL Server](java-sql-datatypes.md)
