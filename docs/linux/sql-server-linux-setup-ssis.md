---
title: Installare SQL Server Integration Services in Linux
description: Questo articolo descrive come installare SQL Server Integration Services (SSIS) in Linux.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 68f3497e9f3f47d7e43c2bda0083bc25632d8221
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032430"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Installare SQL Server Integration Services (SSIS) in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Per installare SQL Server Integration Services (`mssql-server-is`) in Linux, seguire la procedura descritta in questo articolo. Per informazioni sulle funzionalità supportate in questa versione di Integration Services per Linux, vedere le [note sulla versione](sql-server-linux-release-notes.md).

Installare SQL Server Integration Services per la piattaforma in uso:

- [Ubuntu 16.04](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> Installare SSIS in Ubuntu
Per installare il pacchetto `mssql-server-is` in Ubuntu, seguire questa procedura:

1. Importare le chiavi GPG del repository pubblico.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registrare il repository Microsoft SQL Server per Ubuntu.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

3. Eseguire i comandi seguenti per installare SQL Server Integration Services.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. Dopo aver installato Integration Services, eseguire `ssis-conf`. Per altre informazioni, vedere [Configurare SSIS in Linux con ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. Al termine della configurazione, impostare il percorso.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Aggiornare SSIS
Se `mssql-server-is` è già installato, è possibile eseguire l'aggiornamento all'ultima versione con il comando seguente:

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>Rimuovere SSIS
Per rimuovere `mssql-server-is`, è possibile eseguire il comando seguente:
```bash
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> Installare SSIS in RHEL
Per installare il pacchetto `mssql-server-is` in RHEL, seguire questa procedura:

1. Scaricare il file di configurazione del repository Microsoft SQL Server per Red Hat.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. Eseguire i comandi seguenti per installare SQL Server Integration Services.

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. Dopo l'installazione, eseguire `ssis-conf`. Per altre informazioni, vedere [Configurare SSIS in Linux con ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. Al termine della configurazione, impostare il percorso.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Aggiornare SSIS
Se `mssql-server-is` è già installato, è possibile eseguire l'aggiornamento all'ultima versione con il comando seguente:

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>Rimuovere SSIS
Per rimuovere `mssql-server-is`, è possibile eseguire il comando seguente:
```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>Installazione automatica
Per eseguire un'installazione automatica quando si esegue `ssis-conf setup`, eseguire le operazioni seguenti:
1.  Specificare l'opzione `-n` (nessun prompt).
2.  Per specificare i valori obbligatori, impostare variabili di ambiente.

L'esempio che segue esegue le operazioni seguenti:
-   Installa SSIS.
-   Indica l'edizione Developer specificando un valore per la variabile di ambiente `SSIS_PID`.
-   Accetta le condizioni di licenza specificando un valore per la variabile di ambiente `ACCEPT_EULA`.
-   Esegue l'installazione automatica specificando l'opzione `-n` (nessun prompt).

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>Variabili di ambiente per l'installazione automatica

| Variabile di ambiente | Descrizione |
|---|---|
| **ACCEPT_EULA** | Se impostata su un qualsiasi valore, ad esempio `Y`, accetta il contratto di licenza di SQL Server.|
| **SSIS_PID** | Imposta l'edizione o il codice Product Key di SQL Server. Ecco i valori possibili:<br/>Copia di valutazione<br/>Developer<br/>Express <br/>Web <br/>Standard<br/>Enterprise <br/>Un codice Product Key<br/><br/>Se si specifica un codice Product Key, questo deve avere il formato `#####-#####-#####-#####-#####`, dove `#` è una lettera o un numero.  |
| | |

## <a name="next-steps"></a>Passaggi successivi

Per eseguire pacchetti SSIS in Linux, vedere [Estrarre, trasformare e caricare i dati per SQL Server in Linux con SSIS](sql-server-linux-migrate-ssis.md).

Per configurare impostazioni SSIS aggiuntive in Linux, vedere [Configurare SQL Server Integration Services in Linux con ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="related-content-about-ssis-on-linux"></a>Contenuto correlato su SSIS in Linux
-   [Estrarre, trasformare e caricare i dati in Linux con SSIS](sql-server-linux-migrate-ssis.md)
-   [Configurare SQL Server Integration Services in Linux con ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitazioni e problemi noti di SSIS in Linux](sql-server-linux-ssis-known-issues.md)
-   [Pianificare l'esecuzione del pacchetto SQL Server Integration Services in Linux con cron](sql-server-linux-schedule-ssis-packages.md)
