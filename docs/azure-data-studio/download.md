---
title: Scaricare e installare
titleSuffix: Azure Data Studio
description: Scaricare e installare Studio dati Azure per Windows, macOS o Linux
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.custom: seodec18
ms.date: 07/11/2019
ms.reviewer: alayu; sstein
ms.openlocfilehash: a2a4d4e755908d544e79b751d64ee99cad6fc96c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959697"
---
# <a name="download-and-install-azure-data-studio"></a>Scaricare e installare Data Studio di Azure

[!INCLUDE[name-sos](../includes/name-sos.md)] è supportato in Windows, macOS e Linux.


Scaricare e installare la versione più recente, il *luglio*:

> [!NOTE]
> Se si esegue l'aggiornamento da SQL Operations Studio e si desidera mantenere le impostazioni, tasti di scelta rapida o frammenti di codice, vedere [spostare le impostazioni utente](#move-user-settings).

|Piattaforma|Scarica|Data di rilascio| Versione |
|:---|:---|:---|:---|
|Windows|[Programma di installazione di utente (scelta consigliata)](https://go.microsoft.com/fwlink/?linkid=2098449)<br>[Programma di installazione sistema](https://go.microsoft.com/fwlink/?linkid=2098450)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2098500)|11 luglio 2019 |1.9.0|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2098501)|11 luglio 2019 |1.9.0|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2098279)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2098280)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2098197)|11 luglio 2019 |1.9.0|

Per informazioni dettagliate sulla versione più recente, vedere le [note sulla versione](release-notes.md).

## <a name="get-azure-data-studio-for-windows"></a>Ottenere dati di Azure Studio per Windows

Questa versione di [!INCLUDE[name-sos](../includes/name-sos-short.md)] include un'esperienza di installazione di Windows standard e un file con estensione zip.

Il *programma di installazione utente* è consigliato perché non richiede privilegi di amministratore, che semplifica le installazioni e aggiornamenti. Il programma di installazione di utente non richiede privilegi di amministratore la posizione si trova nella cartella AppData locale (LOCALAPPDATA) utente. Il programma di installazione utente fornisce inoltre un'esperienza più uniforme di aggiornamento in background. Per altre informazioni, vedere [configurazione utente per Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows).


**Programma di installazione utente** (scelta consigliata)

1. Scaricare ed eseguire la [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *utente* programma di installazione per Windows](https://go.microsoft.com/fwlink/?linkid=2098449).
2. Avviare l'app [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**Programma di installazione sistema**

1. Scaricare ed eseguire la [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *system* programma di installazione per Windows](https://go.microsoft.com/fwlink/?linkid=2098450 ).
2. Avviare l'app [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].


**.zip file**

1. Scaricare lo [ZIP di [!INCLUDE[name-sos](../includes/name-sos-short.md)] per Windows](https://go.microsoft.com/fwlink/?linkid=2098500).
2. Individuare il file scaricato e decomprimerlo.
3. Eseguire `\azuredatastudio-windows\azuredatastudio.exe`


## <a name="get-azure-data-studio-for-macos"></a>Ottenere Data Studio di Azure per macOS

1. Scaricare [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] per macOS](https://go.microsoft.com/fwlink/?linkid=2098501).
2. Per espandere il contenuto del file zip, fare doppio clic.
3. Per rendere [!INCLUDE[name-sos](../includes/name-sos-short.md)] disponibile nel *Launchpad*, trascinare */Applications i dati di Azure* per i *applicazioni* cartella.


## <a name="get-azure-data-studio-for-linux"></a>Ottenere Studio dei dati di Azure per Linux

1. Scaricare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per Linux usando uno dei programmi di installazione o l'archivio GZ:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2098279)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2098280)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2098197)
1. Per estrarre il file e avviare [!INCLUDE[name-sos](../includes/name-sos-short.md)], aprire una nuova finestra del terminale e digitare i comandi seguenti:

   **Installazione di Debian:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **Installazione di RPM:**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **GZ installazione:**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > In Debian, Redhat e Ubuntu, potrebbero mancare alcune dipendenze. Per installarle, a seconda della versione di Linux, utilizzare i comandi seguenti:
   

   **Debian:** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **RedHat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```
## <a name="download-insiders-build-of-azure-data-studio"></a>Scaricare la build Insider di Studio dei dati di Azure
In generale, gli utenti devono scaricare la versione stabile di Studio di dati di Azure precedente. Tuttavia, se si vuole provare la funzionalità beta e fornire commenti e suggerimenti, è possibile scaricare un [build insiders di Studio dei dati di Azure.](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)

## <a name="uninstall-azure-data-studio"></a>Disinstallare Studio dei dati di Azure

Se [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] è stato installato utilizzando il programma di installazione di Windows, disinstallare nel modo comune a tutte le applicazioni di Windows.

Se[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] è stato installato con un file ZIP o altro archivio, eliminare i file.

## <a name="supported-operating-systems"></a>Sistemi operativi supportati

[!INCLUDE[name-sos](../includes/name-sos-short.md)] è supportato in Windows, macOS e Linux, sulle piattaforme seguenti:

### <a name="windows"></a>Windows
- Windows 10 (64 bit)
- Windows 8.1 (64 bit)
- Windows 8 (64 bit)
- Richiede Windows 7 (SP1) (64 bit) - [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2016
- Windows Server 2012 R2 (64 bit)
- Windows Server 2012 (64 bit)
- Windows Server 2008 R2 (64 bit)

### <a name="macos"></a>macOS
- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="recommended-system-requirements"></a>I requisiti di sistema consigliati
Per un'esperienza ottimale, usare i requisiti di sistema consigliati.
[Need aggiornamento qui quantificare memoria]

|             | Core CPU | Memoria/memoria RAM |
|:-----------|:---------|:----------|
| Consigliato |     4     |      8 GB    |
|   Minimo   |     2     |      4 GB     |
|             |           |            |

## <a name="check-for-updates"></a>Verificare gli aggiornamenti
Per verificare gli aggiornamenti più recenti, fare clic sull'icona a forma di ingranaggio nell'angolo inferiore sinistro della finestra e fare clic su **Controlla aggiornamenti**

## <a name="supported-sql-offerings"></a>Offerte di SQL supportate

* Questa versione di Studio dei dati di Azure funziona con tutte le [le versioni supportate di SQL Server 2014 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] ](https://support.microsoft.com/lifecycle?C2=1044) e fornisce il supporto per l'utilizzo con le funzionalità cloud più recenti nel Database SQL di Azure e Azure SQL Data Warehouse. Azure Data Studio fornisce anche supporto in anteprima per istanza gestita SQL di Azure.

## <a name="upgrade-from-sql-operations-studio"></a>Eseguire l'aggiornamento da SQL Operations Studio

Se si sta ancora usando SQL Operations Studio, è necessario eseguire l'aggiornamento a Azure Data Studio. SQL Operations Studio è il nome di anteprima e una versione di anteprima di Azure Data Studio. Nel mese di settembre 2018, abbiamo [modificato il nome in Azure Data Studio](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/) e rilasciato la versione GA (General Availability). Poiché SQL Operations Studio è non è più aggiornato o supportato, verrà richiesto di tutti gli utenti di SQL Operations Studio per scaricare la versione più recente di Studio di dati di Azure per ottenere le funzionalità più recenti, gli aggiornamenti della sicurezza e correzioni.
 
Durante l'aggiornamento dalla versione di anteprima precedente ad Azure Data Studio più recente, si perderanno le impostazioni correnti e le estensioni. Per spostare le impostazioni, seguire le istruzioni riportate di seguito *spostare le impostazioni utente* sezione:


## <a name="move-user-settings"></a>Spostare le impostazioni utente

Se si desidera spostare che le impostazioni personalizzate, tasti di scelta rapida o frammenti di codice, attenersi alla procedura seguente. Questo è importante se si esegue l'aggiornamento dalla versione di SQL Operations Studio ad Azure Data Studio.

*Se si dispone già di Studio dei dati di Azure o è stato mai installato o personalizzato di SQL Operations Studio, è possibile ignorare questa sezione.*


1. Aprire le impostazioni, scegliere l'icona dell'ingranaggio nella parte inferiore sinistra e scegliere **impostazioni.**

   ![Open-impostazioni](./media/download/open-settings.png)

2. Fare doppio clic il **delle impostazioni utente** scheda nella parte superiore e fare clic su **Visualizza in Esplora risorse**

   ![rivela-in-explorer](./media/download/reveal-in-explorer.png)

3. Copiare tutti i file in questa cartella e salvarlo in un modo facile trovare percorso nell'unità locale, come la cartella documenti.

   ![Copia-impostazioni](./media/download/copy-settings.png)

4. Nella versione nuova di Azure Data Studio, seguire i passaggi 1 e 2, quindi per passaggio 3 incollare il contenuto che è stato salvato nella cartella. È inoltre possibile copiare manualmente tramite le impostazioni, i tasti di scelta rapida o frammenti di codice nelle rispettive posizioni.

5. Se si esegue l'override di un'installazione esistente, eliminare la vecchia directory di installazione prima dell'installazione per evitare errori di connessione all'account di Azure per Esplora risorse.

## <a name="next-steps"></a>Passaggi successivi

Seguire una delle guide rapide qui sotto per iniziare:
- [Connettersi ed eseguire query in SQL Server](quickstart-sql-server.md)
- [Connettersi ed eseguire query in Database SQL di Azure](quickstart-sql-database.md)
- [Connettersi ed eseguire query in Azure Data Warehouse](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Informativa sulla Privacy Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) e [raccolta dati di utilizzo](usage-data-collection.md).