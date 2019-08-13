---
title: Scaricare e installare
titleSuffix: Azure Data Studio
description: Scaricare e installare Azure Data Studio per Windows, macOS o Linux
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.custom: seodec18
ms.date: 07/11/2019
ms.reviewer: alayu; sstein
ms.openlocfilehash: ff212d44fc16ad4a8c6366eda88d92fa78f20d84
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811216"
---
# <a name="download-and-install-azure-data-studio"></a>Scaricare e installare Azure Data Studio

[!INCLUDE[name-sos](../includes/name-sos.md)] viene eseguito in Windows, macOS e Linux.


Scaricare e installare la versione più recente, la *versione di luglio*:

> [!NOTE]
> Se si esegue l'aggiornamento da SQL Operations Studio e si vogliono mantenere le impostazioni, le scelte rapide da tastiera o i frammenti di codice, vedere [Spostare le impostazioni utente](#move-user-settings).

|Piattaforma|Scarica|Data di rilascio| Versione |
|:---|:---|:---|:---|
|Windows|[Programma di installazione utente (scelta consigliata)](https://go.microsoft.com/fwlink/?linkid=2098449)<br>[Programma di installazione di sistema](https://go.microsoft.com/fwlink/?linkid=2098450)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2098500)|11 luglio 2019 |1.9.0|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2098501)|11 luglio 2019 |1.9.0|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2098279)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2098280)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2098197)|11 luglio 2019 |1.9.0|

Per informazioni dettagliate sulla versione più recente, vedere le [note sulla versione](release-notes.md).

## <a name="get-azure-data-studio-for-windows"></a>Ottenere Azure Data Studio per Windows

Questa versione di [!INCLUDE[name-sos](../includes/name-sos-short.md)] include un'esperienza di installazione Windows standard e un file ZIP.

Il *programma di installazione utente* è consigliato perché non richiede privilegi di amministratore, il che semplifica sia le installazioni che gli aggiornamenti. Il programma di installazione utente non richiede privilegi di amministratore perché il percorso si trova nella cartella AppData locale (LOCALAPPDATA) dell'utente. Il programma di installazione utente fornisce anche un'esperienza di aggiornamento in background più fluida. Per altre informazioni, vedere l'articolo sulla [Configurazione utente per Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows).

**Programma di installazione utente** (scelta consigliata)

1. Scaricare ed eseguire il [programma di installazione *utente* di [!INCLUDE[name-sos](../includes/name-sos-short.md)] per Windows](https://go.microsoft.com/fwlink/?linkid=2098449).
2. Avviare l'app [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**Programma di installazione di sistema**

1. Scaricare ed eseguire il [programma di installazione *di sistema* di [!INCLUDE[name-sos](../includes/name-sos-short.md)] per Windows](https://go.microsoft.com/fwlink/?linkid=2098450 ).
2. Avviare l'app [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**.zip file**

1. Scaricare lo [ZIP di [!INCLUDE[name-sos](../includes/name-sos-short.md)] per Windows](https://go.microsoft.com/fwlink/?linkid=2098500).
2. Individuare il file scaricato ed estrarlo.
3. Eseguire `\azuredatastudio-windows\azuredatastudio.exe`


## <a name="get-azure-data-studio-for-macos"></a>Ottenere Azure Data Studio per macOS

1. Scaricare [[!INCLUDE[name-sos](../includes/name-sos-short.md)] per macOS](https://go.microsoft.com/fwlink/?linkid=2098501).
2. Per espandere il contenuto del file ZIP, fare doppio clic su di esso.
3. Per rendere [!INCLUDE[name-sos](../includes/name-sos-short.md)] disponibile nel *Launchpad*, trascinare *Azure Data Studio.app* nella cartella *Applicazioni*.


## <a name="get-azure-data-studio-for-linux"></a>Ottenere Azure Data Studio per Linux

1. Scaricare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per Linux usando uno dei programmi di installazione o l'archivio tar.gz:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2098279)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2098280)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2098197)
1. Per estrarre il file e avviare [!INCLUDE[name-sos](../includes/name-sos-short.md)], aprire una nuova finestra del terminale e digitare i comandi seguenti:

   **Installazione Debian:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **Installazione RPM:**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **Installazione tar.gz:**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > In Debian, Red Hat e Ubuntu potrebbero mancare alcune dipendenze. Usare i comandi seguenti per installare queste dipendenze a seconda della versione di Linux:
   

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
## <a name="download-insiders-build-of-azure-data-studio"></a>Scaricare la build Insider di Azure Data Studio
In generale, gli utenti dovrebbero scaricare la versione stabile di Azure Data Studio precedente. Tuttavia, se si vogliono provare le funzionalità beta e inviare feed, è possibile scaricare una [build Insider di Azure Data Studio.](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)

## <a name="uninstall-azure-data-studio"></a>Disinstallare Azure Data Studio

Se [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] è stato installato usando il Windows Installer, disinstallarlo così come si rimuove qualsiasi applicazione Windows.

Se [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] è stato installato con un file ZIP o un altro archivio, è sufficiente eliminare i file.

## <a name="supported-operating-systems"></a>Sistemi operativi supportati

[!INCLUDE[name-sos](../includes/name-sos-short.md)] viene eseguito in Windows, macOS e Linux ed è supportato nelle piattaforme seguenti:

### <a name="windows"></a>Windows
- Windows 10 (64 bit)
- Windows 8.1 (64 bit)
- Windows 8 (64 bit)
- Windows 7 (SP1) (64 bit) - Richiede [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2019
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

## <a name="recommended-system-requirements"></a>Requisiti di sistema consigliati

|             | Core CPU | Memoria/RAM |
|:-----------|:---------|:----------|
| Consigliato |     4     |      8 GB    |
|   Minimo   |     2     |      4 GB     |
|             |           |            |

## <a name="check-for-updates"></a>Verificare gli aggiornamenti
Per verificare la disponibilità di aggiornamenti più recenti, fare clic sull'icona a forma di ingranaggio nella parte inferiore sinistra della finestra e fare clic su **Controlla aggiornamenti**

## <a name="supported-sql-offerings"></a>Offerte di SQL supportate

* Questa versione di Azure Data Studio funziona con tutte le [versioni supportate di SQL Server 2014 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e offre supporto per l'uso con le funzionalità cloud più recenti nel database SQL di Azure e in Azure SQL Data Warehouse. Azure Data Studio fornisce anche il supporto in anteprima per Istanza gestita di SQL di Azure.

## <a name="upgrade-from-sql-operations-studio"></a>Eseguire l'aggiornamento da SQL Operations Studio

Se si usa ancora SQL Operations Studio, è necessario eseguire l'aggiornamento ad Azure Data Studio. SQL Operations Studio è il nome di anteprima e la versione di anteprima di Azure Data Studio. Nel settembre 2018, [il nome è stato modificato in Azure Data Studio](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/) ed è stata rilasciata la versione disponibile a livello generale. Poiché SQL Operations Studio non viene più aggiornato né supportato, si chiede a tutti gli utenti di SQL Operations Studio di scaricare l'ultima versione di Azure Data Studio per ottenere le funzionalità, gli aggiornamenti della sicurezza e le correzioni più recenti.
 
Quando si esegue l'aggiornamento dalla precedente versione di anteprima all'ultima versione di Azure Data Studio, le impostazioni e le estensioni correnti vanno perse. Per spostare le impostazioni, seguire le istruzioni riportate nella sezione *Spostare le impostazioni utente* di seguito:


## <a name="move-user-settings"></a>Spostare le impostazioni utente

Se si vogliono spostare le scelte rapide da tastiera, i frammenti di codice o le impostazioni personalizzate, attenersi alla procedura riportata di seguito. Questa operazione è importante se si esegue l'aggiornamento da SQL Operations Studio ad Azure Data Studio.

*Se si ha già Azure Data Studio o non si è mai installato o personalizzato SQL Operations Studio, è possibile ignorare questa sezione.*


1. Aprire le impostazioni facendo clic sull'icona a forma di ingranaggio in basso a sinistra e quindi su **Impostazioni.**

   ![open-settings](./media/download/open-settings.png)

2. Fare clic con il pulsante destro del mouse sulla scheda **Impostazioni utente** nella parte superiore e scegliere **Visualizza in Esplora risorse**

   ![reveal-in-explorer](./media/download/reveal-in-explorer.png)

3. Copiare tutti i file in questa cartella e salvarli in un percorso facile da trovare nell'unità locale, ad esempio la cartella Documenti.

   ![copy-settings](./media/download/copy-settings.png)

4. Nella nuova versione di Azure Data Studio, seguire i passaggi 1-2, quindi, per il passaggio 3, incollare il contenuto salvato nella cartella. È anche possibile copiare manualmente le impostazioni, i tasti di scelta rapida o i frammenti di codice nelle rispettive posizioni.

5. Se si esegue l'override di un'installazione esistente, eliminare la vecchia directory di installazione prima dell'installazione per evitare errori di connessione all'account Azure per Resource Explorer.

## <a name="next-steps"></a>Next Steps

Per iniziare, vedere uno degli argomenti di avvio rapido seguenti:
- [Connettersi ed eseguire query in SQL Server](quickstart-sql-server.md)
- [Connettersi ed eseguire query nel database SQL di Azure](quickstart-sql-database.md)
- [Connettersi ed eseguire query in Azure SQL Data Warehouse](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Informativa sulla privacy di Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) e [Raccolta dati di utilizzo](usage-data-collection.md).
