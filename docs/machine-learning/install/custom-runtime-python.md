---
title: Installare il runtime personalizzato di Python
description: Informazioni su come installare un runtime personalizzato di Python per SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/20/2020
ms.topic: how-to
author: cawrites
ms.author: chadam
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4a625684b3196fc246b2753fc7b7e38b3e603f6e
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155062"
---
# <a name="install-a-python-custom-runtime-for-sql-server"></a>Installare un runtime personalizzato di Python per SQL Server
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Questo articolo descrive come installare un runtime personalizzato per l'esecuzione di script Python con SQL Server. Il runtime personalizzato usa la tecnologia di estensione del linguaggio basata su un framework di estendibilità per l'esecuzione di codice esterno. Il runtime personalizzato per Python può essere usato negli scenari seguenti:

+ Un'installazione di SQL Server con framework di estendibilità.

+ Un'installazione di Machine Learning Services con SQL Server 2019. L'estensione del linguaggio può essere usata con [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) dopo aver completato alcuni passaggi di configurazione aggiuntivi.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> Questo articolo descrive come installare un runtime personalizzato per Python in Windows. Per eseguire l'installazione in Linux, vedere [Installare un runtime personalizzato di Python per SQL Server in Linux](custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true).



## <a name="pre-install-checklist"></a>Elenco di controllo preliminare all'installazione

Prima di installare un runtime personalizzato di Python, installare quanto segue:

+ [SQL Server 2019 per Windows CU3 o versioni successive](../../database-engine/install-windows/install-sql-server.md).

  > [!NOTE]
  > Il runtime personalizzato di Python richiede l'aggiornamento cumulativo (CU) 3 o versione successiva per SQL Server 2019.

+ [Estensioni del linguaggio di SQL Server in Windows con il framework di estendibilità](../../language-extensions/install/windows-java.md).

+ [Python 3.7]( https://www.python.org/downloads/release/python-379/).

## <a name="add-sql-server-language-extensions-for-windows"></a>Aggiungere le estensioni del linguaggio di SQL Server per Windows

> [!NOTE]
> Se Machine Learning Services è installato in SQL Server 2019, il framework di estendibilità è già installato ed è possibile ignorare questo passaggio.

Le estensioni del linguaggio usano il framework di estendibilità per l'esecuzione di codice esterno. L'esecuzione del codice è isolata dai processi del motore di base, ma completamente integrata con l'esecuzione delle query di SQL Server.

1. Avviare l'Installazione guidata di SQL Server 2019.
  
1. Nella scheda **Installazione** selezionare **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.
    
    ![Installazione di SQL Server 2019 CU3 o versione successiva](../install/media/2019setup-installation-page-mlsvcs.png) 

1. Nella pagina **Selezione funzionalità** selezionare queste opzioni:
  
    - **Servizi motore di database**
  
        Per usare le estensioni del linguaggio con SQL Server, è necessario installare un'istanza del motore di database. È possibile usare un'istanza predefinita oppure un'istanza denominata.
  
    - **Machine Learning Services ed estensioni del linguaggio**
   
       Selezionare **Machine Learning Services ed estensioni del linguaggio**. Non è necessario selezionare Python.

    ![Funzionalità di installazione di SQL Server 2019 CU3 o versioni successive](../install/media/sql-feature-selection.png) 

1. Nella pagina **Inizio installazione** verificare che le opzioni selezionate siano incluse e selezionare **Installa**.
  
    + Servizi motore di database
    + Machine Learning Services ed estensioni del linguaggio

1. Dopo che l'installazione è completata, riavviare il computer, se richiesto. È importante leggere il messaggio visualizzato nell'Installazione guidata al termine dell'installazione. Per altre informazioni, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).


## <a name="install-python-37"></a>Installare Python 3.7 

Installare [Python 3.7]( https://www.python.org/downloads/release/python-379/) e aggiungerlo a PATH.

![Aggiungere Python 3.7 al percorso.](../install/media/python-379.png) 


#### <a name="install-pandas"></a>Installare pandas

Installare il pacchetto [pandas](https://pandas.pydata.org/) per Python da un prompt dei comandi con *privilegi elevati*:

```bash
python.exe -m pip install pandas
```

## <a name="update-the-system-environment-variables"></a>Aggiornare le variabili di ambiente del sistema

Aggiungere o modificare PYTHONHOME come variabile di ambiente del sistema.

+ Nella casella di ricerca di Windows digitare "ambiente" e selezionare **Modifica le variabili di ambiente relative al sistema**.
+ Nella scheda **Avanzate** selezionare **Variabili di ambiente**.
+ In **Variabili di sistema** selezionare **Nuova** per creare PYTHONHOME in modo che punti al percorso di installazione di Python 3.7.
Se la variabile PYTHONHOME esiste già, selezionare **Modifica** per puntare al percorso di installazione di Python 3.7.
+ Selezionare **OK** per chiudere le finestre rimanenti.

![Creare la variabile di sistema PYTHONHOME.](../install/media/sys-pythonhome.png)

## <a name="grant-access-to-the-custom-python-installation-folder"></a>Concedere l'accesso alla cartella di installazione personalizzata di Python

Eseguire i seguenti comandi **icacls** da un nuovo prompt dei comandi *con privilegi elevati* per concedere l'accesso in lettura ed esecuzione a PYTHONHOME per il **servizio Launchpad di SQL Server** e il SID **S-1-15-2-1** (**ALL_APPLICATION_PACKAGES**). Il nome utente del servizio Launchpad è nel formato `NT Service\MSSQLLAUNCHPAD$INSTANCENAME* where INSTANCENAME` è il nome dell'istanza di SQL Server. I comandi concederanno l'accesso in modo ricorsivo a tutti i file e le cartelle nel percorso di directory specificato.

Aggiungere il nome dell'istanza a `MSSQLLAUNCHPAD` (`MSSQLLAUNCHPAD$INSTANCENAME`). In questo esempio INSTANCENAME è l'istanza predefinita `MSSQLSERVER`.

1. Concedere le autorizzazioni a **nome utente del servizio Launchpad di SQL Server**.

    ```cmd
    icacls "%PYTHONHOME%" /grant "NT Service\MSSQLLAUNCHPAD$MSSQLSERVER":(OI)(CI)RX /T

2. Give permissions to **SID S-1-15-2-1**.
    ```cmd
    icacls "%PYTHONHOME%" /grant *S-1-15-2-1:(OI)(CI)RX /T

>[!NOTE]
>The preceding command grants permissions to the computer **SID S-1-15-2-1**, which is equivalent to ALL APPLICATION PACKAGES on an English version of Windows. Alternatively, you can use `icacls "%R_HOME%" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` on an English version of Windows.

## Restart SQL Server Launchpad service

From an *elevated* command prompt, run the following commands. Replace "MSSQLSERVER" with the name of your SQL Server instance.

```CMD
net stop MSSQLLAUNCHPAD$MSSQLSERVER
net start MSSQLLAUNCHPAD$MSSQLSERVER
```

In alternativa, fare clic con il pulsante destro del mouse sul servizio Launchpad di SQL Server nell'app **Servizi** del sistema e scegliere il comando **Riavvia**. Oppure usare [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md) per riavviare il servizio.

## <a name="download-python-language-extension"></a>Scaricare l'estensione del linguaggio Python

Scaricare il [file ZIP contenente l'estensione del linguaggio Python per Windows](https://github.com/microsoft/sql-server-language-extensions/releases). È consigliabile usare la versione di rilascio in ambiente di produzione. Usare la versione di debug in ambiente di sviluppo o test poiché offre informazioni dettagliate sulla registrazione per esaminare eventuali errori.

## <a name="register-external-language"></a>Registrare il linguaggio esterno

Registrare questa estensione del linguaggio Python con [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) per ogni database in cui si vuole usarla. Usare [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) per connettersi a SQL Server ed eseguire il comando T-SQL seguente. Modificare il percorso in questa istruzione in modo che corrisponda al percorso del file ZIP dell'estensione del linguaggio scaricato (python-lang-extension.zip).

> [!NOTE]
> Python è una parola riservata. Usare un nome diverso per il linguaggio esterno, ad esempio "mioPython".

```sql
CREATE EXTERNAL LANGUAGE [myPython]
FROM (CONTENT = N'/path/to/python-lang-extension.zip', FILE_NAME = 'pythonextension.dll');
GO
```

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

È possibile installare SQL Server in Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) e Ubuntu. Per altre informazioni, vedere [la sezione delle piattaforme supportate nelle linee guida per l'installazione di SQL Server in Linux](../../linux/sql-server-linux-setup.md).

> [!NOTE]
> Questo articolo descrive come installare un runtime personalizzato per Python in Linux. Per eseguire l'installazione in Windows, vedere [Installare un runtime personalizzato di Python per SQL Server in Windows](custom-runtime-python.md?view=sql-server-ver15&preserve-view=true).

## <a name="pre-install-checklist"></a>Elenco di controllo preliminare all'installazione

Prima di installare un runtime personalizzato di Python, installare quanto segue:

+ [SQL Server 2019 per Linux (aggiornamento cumulativo 3 o versione successiva)](../../linux/sql-server-linux-setup.md).
Quando si installa SQL Server in Linux, è necessario configurare un repository Microsoft. Per altre informazioni, vedere [Configurazione dei repository](../../linux/sql-server-linux-change-repo.md).

  > [!NOTE]
  > Il runtime personalizzato di Python richiede l'aggiornamento cumulativo (CU) 3 o versione successiva per SQL Server 2019.

+ [Estensioni del linguaggio di SQL Server in Linux con il framework di estendibilità](../../linux/sql-server-linux-setup-language-extensions-java.md).

+ [Python 3.7](https://www.python.org/downloads/release/python-379/).

## <a name="add-sql-server-language-extensions-for-linux"></a>Aggiungere le estensioni del linguaggio di SQL Server per Linux

> [!NOTE]
> Se Machine Learning Services è installato in SQL Server 2019, il pacchetto **mssql-server-extensibility** per le estensioni del linguaggio è già installato ed è possibile ignorare questo passaggio.

Le estensioni del linguaggio usano il framework di estendibilità per l'esecuzione di codice esterno. L'esecuzione del codice è isolata dai processi del motore di base, ma completamente integrata con l'esecuzione delle query di SQL Server.

Usare i comandi seguenti per installare le estensioni del linguaggio, a seconda della versione di Linux.

### <a name="ubuntu"></a>Ubuntu
> [!TIP]
> Se possibile, eseguire `update` per aggiornare i pacchetti nel sistema prima dell'installazione. Ubuntu potrebbe non avere l'opzione di trasporto https apt. Per installarla, usare `apt-get install apt-transport-https`.

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility
```

### <a name="red-hat"></a>Red Hat
```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility
```

### <a name="suse"></a>SUSE
```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility
```

## <a name="install-python-37-and-pandas"></a>Installare Python 3.7 e pandas

Installare Python 3.7, la libreria libpython3.7 e il pacchetto pandas. 

Di seguito sono riportati alcuni comandi di esempio per Ubuntu:

```bash
# Install python3.7 and the corresponding library:
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.7 python3-pip libpython3.7

# Install pandas to /usr/lib:
sudo python3.7 -m pip install pandas -t /usr/lib/python3.7/dist-packages
```

## <a name="using-a-custom-installation-of-python-37"></a>Uso di un'installazione personalizzata di Python 3.7

> [!NOTE]
> Se Python è stato installato nel percorso predefinito `/usr/lib/python3.7`, è possibile passare alla [sezione successiva](#download-python-linux).

Se è stata creata una versione personalizzata di Python 3.7, usare i comandi seguenti in modo che SQL Server possibile trovare e caricare l'installazione personalizzata.

### <a name="update-the-environment-variables"></a>Aggiornare le variabili di ambiente

1. Modificare il servizio mssql-launchpadd per aggiungere la variabile di ambiente PYTHONHOME al file `/etc/systemd/system/mssql-launchpadd.service.d/override.conf`

      ```bash
      sudo systemctl edit mssql-launchpadd
      ```

    + Inserire il testo seguente nel file `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` che si apre. Impostare il valore di PYTHONHOME sul percorso di installazione personalizzato di Python.

      ```vi
      [Service]
      Environment="PYTHONHOME=/path/to/installation/of/python3.7"
      ```

    + Salvare e chiudere.

2. Verificare che `libpython3.7m.so.1.0` possa essere caricato.

    + Creare un file python.conf personalizzato in `/etc/ld.so.conf.d`.

      ```bash
      sudo vi /etc/ld.so.conf.d/custom-python.conf
      ```

    + Nel file che si apre aggiungere il percorso **libpython3.7m.so.1.0** dall'installazione personalizzata di Python.

      ```vi
      /path/to/installation/of/python3.7/lib
      ```

    + Salvare e chiudere il nuovo file.

    + Eseguire `ldconfig` e verificare che sia possibile caricare `libpython3.7m.so.1.0` eseguendo i comandi seguenti e verificando che tutte le librerie dipendenti siano disponibili.

      ```bash
      sudo ldconfig
      ldd /path/to/installation/of/python3.7/lib/libpython3.7m.so.1.0
      ```

### <a name="grant-access-to-the-custom-python-folder"></a>Concedere l'accesso alla cartella personalizzata di Python

Impostare l'opzione `datadirectories` nella sezione extensibility del file /var/opt/mssql/mssql.conf sull'installazione personalizzata di Python.

```bash
sudo /opt/mssql/bin/mssql-conf set extensibility.datadirectories /path/to/installation/of/python3.7
```

### <a name="restart-the-mssql-launchpadd-service"></a>Riavviare il servizio mssql-launchpadd

```bash
sudo systemctl restart mssql-launchpadd
```
## <a name="download-python-language-extension"></a><a name="download-python-linux"></a> Scaricare l'estensione del linguaggio Python

Scaricare il [file ZIP contenente l'estensione del linguaggio Python per Linux](https://github.com/microsoft/sql-server-language-extensions/releases). È consigliabile usare la versione di rilascio in ambiente di produzione. Usare la versione di debug in ambiente di sviluppo o test poiché offre informazioni dettagliate sulla registrazione per esaminare eventuali errori.

## <a name="register-external-language"></a>Registrare il linguaggio esterno

Registrare questa estensione del linguaggio Python con [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) per ogni database in cui si vuole usarla. Usare [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) per connettersi a SQL Server ed eseguire il comando T-SQL seguente. 
Modificare il percorso in questa istruzione in modo che corrisponda al percorso del file ZIP dell'estensione del linguaggio scaricato (python-lang-extension.zip).

> [!NOTE]
>Python è una parola riservata. Usare un nome diverso per il linguaggio esterno, ad esempio "mioPython".

```sql
CREATE EXTERNAL LANGUAGE myPython 
FROM (CONTENT = N'/PATH/TO/python-lang-extension.zip', FILE_NAME = 'libPythonExtension.so.1.0');
GO
```

::: moniker-end

## <a name="enable-external-script-execution-in-sql-server"></a>Abilitare l'esecuzione di script esterni in SQL Server

Uno script esterno in Python può essere eseguito tramite la stored procedure [sp_execute_external script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) eseguita su SQL Server. 

Per abilitare gli script esterni, eseguire i comandi SQL seguenti usando [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) connesso a SQL Server.

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

## <a name="verify-language-extension-installation"></a>Verificare l'installazione dell'estensione del linguaggio

Questo script SQL verifica la funzionalità dell'estensione del linguaggio installata.

```sql
EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
import sys
print(sys.path)
print(sys.version)
print(sys.executable)'
```

## <a name="verify-parameters-and-datasets-of-different-data-types"></a>Verificare i parametri e i set di dati di tipi di dati diversi

Questo script verifica diversi tipi di dati per i set di dati e i parametri di input/output.

```sql
DECLARE @sumVal int = 12;
DECLARE @charVal VARCHAR(30) = N'Hello'

EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
print(sumVal)
print(charVal)
sumVal = sumVal + 300
OutputDataSet = InputDataSet'
,@input_data_1 = N'SELECT 1, CAST(1.4 as real), ''Hi'', CAST(''1'' as bit)'
,@params = N'@sumVal int OUTPUT, @charVal VARCHAR(30)'
,@sumVal = @sumVal OUTPUT
,@charVal = @charVal
WITH RESULT SETS ((intCol int, doubleCol real, charCol char(2), logicalCol bit));

PRINT @sumVal
```

## <a name="next-steps"></a>Passaggi successivi

+ [Framework di estendibilità in SQL Server](../concepts/extensibility-framework.md)
+ [Panoramica delle estensioni del linguaggio](../../language-extensions/language-extensions-overview.md)