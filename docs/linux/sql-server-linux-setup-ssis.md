---
title: Installare SQL Server Integration Services in Linux | Microsoft Docs
description: Questo articolo descrive come installare SQL Server Integration Services (SSIS) in Linux.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: craigg
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4e85755cd794f5c7f61f63579b65ed294ee4d893
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705083"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Installare SQL Server Integration Services (SSIS) in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Seguire i passaggi descritti in questo articolo per installare SQL Server Integration Services (`mssql-server-is`) in Linux. Per informazioni sulle funzionalità supportate in questa versione di servizi di intergrazione per Linux, vedere la [note sulla versione](sql-server-linux-release-notes.md).

Installare i server di integrazione di SQL Server per la piattaforma:

- [Ubuntu 16.04](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> Installare SSIS in Ubuntu
Per installare il `mssql-server-is` del pacchetto in Ubuntu, seguire questa procedura:

1. Importare le chiavi GPG repository pubblico.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registrare il repository di Microsoft SQL Server Ubuntu.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

3. Eseguire i comandi seguenti per installare SQL Server Integration Services.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. Dopo l'installazione di Integration Services, eseguire `ssis-conf`. Per altre informazioni, vedi [configurare SSIS in Linux con ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. Al termine della configurazione, impostare il percorso.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Aggiornamento di SSIS
Se hai già `mssql-server-is` installato, è possibile aggiornare alla versione più recente con il comando seguente:

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>Rimuovere SSIS
Per rimuovere `mssql-server-is`, è possibile eseguire il comando seguente:
```bash
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> Installare SSIS in RHEL
Per installare il `mssql-server-is` del pacchetto in RHEL, seguire questa procedura:

1. Scaricare il file di configurazione del repository di Microsoft SQL Server Red Hat.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. Eseguire i comandi seguenti per installare SQL Server Integration Services.

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. Dopo l'installazione, eseguire `ssis-conf`. Per altre informazioni, vedi [configurare SSIS in Linux con ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. Al termine della configurazione, impostare percorso.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Aggiornamento di SSIS
Se hai già `mssql-server-is` installato, è possibile aggiornare alla versione più recente con il comando seguente:

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
1.  Specificare il `-n` (senza richiesta) opzione.
2.  Fornire i valori richiesti impostando le variabili di ambiente.

Nell'esempio seguente esegue le operazioni seguenti:
-   Consente di installare SSIS.
-   Specifica l'edizione Developer, fornendo un valore per il `SSIS_PID` variabile di ambiente.
-   Accetta il contratto di licenza, fornendo un valore per il `ACCEPT_EULA` variabile di ambiente.
-   Esegue un'installazione automatica, specificando il `-n` (senza richiesta) opzione.

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>Variabili di ambiente per l'installazione automatica

| Variabile di ambiente | Descrizione |
|---|---|
| **ACCEPT_EULA** | Accetta il contratto di licenza di SQL Server quando è impostato su qualsiasi valore (ad esempio, `Y`).|
| **SSIS_PID** | Imposta la chiave di prodotto o edizione di SQL Server. Di seguito sono i valori possibili:<br/>Copia di valutazione<br/>Sviluppatore<br/>Express <br/>Web <br/>Standard<br/>Enterprise <br/>Un codice product key<br/><br/>Se si specifica un codice product key, il codice product key deve essere nel formato `#####-#####-#####-#####-#####`, dove `#` è una lettera o un numero.  |
| | |

## <a name="next-steps"></a>Passaggi successivi

Per eseguire pacchetti SSIS in Linux, vedere [estrazione, trasformazione e caricamento dei dati per SQL Server in Linux con SSIS](sql-server-linux-migrate-ssis.md).

Per configurare altre impostazioni di SSIS in Linux, vedere [configurare SQL Server Integration Services in Linux con ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="related-content-about-ssis-on-linux"></a>Contenuto correlato su SSIS in Linux
-   [Estrarre, trasformare e caricare i dati in Linux con SSIS](sql-server-linux-migrate-ssis.md)
-   [Configurare SQL Server Integration Services in Linux con ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitazioni e problemi noti per SSIS in Linux](sql-server-linux-ssis-known-issues.md)
-   [Esecuzione in Linux con cron pacchetti pianificazione SQL Server Integration Services](sql-server-linux-schedule-ssis-packages.md)
