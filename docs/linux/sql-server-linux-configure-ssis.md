---
title: Configurare SSIS in Linux con ssis-conf
description: Questo articolo descrive come configurare SQL Server Integration Services (SSIS) in Linux con l'utilità di ssis-conf.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 51dc2ba27e346dea75f1bd347491d4932695fd43
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077530"
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>Configurare SQL Server Integration Services in Linux con ssis-conf

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Eseguire il `ssis-conf` script di configurazione quando si installa SQL Server Integration Services (SSIS) per Red Hat Enterprise Linux e Ubuntu. Per altre informazioni sull'installazione di SSIS, vedere [installare SQL Server Integration Services (SSIS) in Linux](sql-server-linux-setup-ssis.md).

È anche possibile usare il `ssis-conf` utilità per configurare le proprietà seguenti:

| Comando | Descrizione |
|-------------|---------------------------------------------------------------------|
| set-edition | Impostare l'edizione di SQL Server                                       |
| dati di telemetria   | Abilitare o disabilitare il servizio di telemetria di SQL Server Integration Services |
| installazione       | Inizializzare e configurare Microsoft SQL Server Integration Services      |
|||

## <a name="run-ssis-conf"></a>Esecuzione di ssis-conf

Gli esempi in questo articolo eseguiti `ssis-conf` specificando il percorso completo: `/opt/ssis/bin/ssis-conf`. Se si passa a tale percorso prima di eseguire `ssis-conf`, è possibile eseguire l'utilità nel contesto della directory corrente: `./ssis-conf`.

Assicurarsi di eseguire i comandi descritti in questo articolo con i privilegi root. Ad esempio, eseguire `sudo /opt/ssis/bin/ssis-conf setup` e non `/opt/ssis/bin/ssis-conf setup`.

Per eseguire i comandi seguenti con istruzioni nel linguaggio che si preferisce, è possibile specificare le impostazioni locali. Ad esempio, per ricevere richieste in cinese, eseguire il comando seguente: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>Usare set-edition per impostare l'edizione di SQL Server Integration Services

L'edizione di SSIS è allineata con l'edizione di SQL Server.

Immettere il comando seguente: `$ sudo /opt/ssis/bin/ssis-conf set-edition`.

Dopo aver immesso il comando, si riceverà il messaggio seguente:

```
Choose an edition of SQL Server:

1) Evaluation (free, no production use rights, 180-day limit)

2) Developer (free, no production use rights)

3) Express (free)

4) Web (PAID)

5) Standard (PAID)

6) Enterprise (PAID)

7) Enterprise Core (PAID)

8) I bought a license through a retail sales channel and have a product key to enter.

Details about editions can be found at https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409.

Use of PAID editions of this software requires separate licensing through a Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate number of licenses in place to install and run this software.

Enter your edition (1-8):
```

Se si immette un valore da 1 a 7, il sistema consente di configurare un'edizione gratuita o a pagamento. Se si immette 8, l'utilità viene richiesto di immettere il codice product key che è stato acquistato:

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>Usare la telemetria per configurare i suggerimenti dei clienti

Il `telemetry` comando determina se SSIS Invia commenti e suggerimenti a Microsoft.

Per le edizioni gratuite (ovvero, edizioni Evaluation, Developer ed Express), il servizio di telemetria è sempre abilitato. Se si dispone di un'edizione gratuita, è possibile usare il `telemetry` comando per disabilitare la telemetria.

Immettere il comando seguente: `$ sudo /opt/ssis/bin/ssis-conf telemetry`.

Per le edizioni a pagamento, dopo aver immesso il comando, verrà visualizzato il messaggio seguente:

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

Se si seleziona **Sì**, il servizio di telemetria è abilitato e avvia l'esecuzione. Il servizio venga avviato automaticamente dopo ogni avvio. Se si seleziona **No**, il servizio dati di telemetria viene interrotta ed è disabilitata.

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>Usare il programma di installazione per inizializzare e configurare Microsoft SQL Server Integration Services

Usare il `setup` comando ogni volta che si installa SSIS.

Immettere il comando seguente: `sudo /opt/ssis/bin/ssis-conf setup`.

L'utilità viene richiesto di confermare o fornire valori per gli elementi seguenti:
-   Licenza del prodotto
-   Contratto EULA
-   Servizio di telemetria
-   La lingua utilizzata da Integration Services

Per eseguire il `setup` il comando con istruzioni nel linguaggio che si preferisce, è possibile specificare le impostazioni locali. Ad esempio, per ricevere richieste in cinese, eseguire il comando seguente: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="ssisconf-format"></a>formato SSIS.conf

Nell'esempio `/var/opt/ssis/ssis.conf` file fornisce un esempio per ogni impostazione.

Per SQL Server, è possibile modificare le impostazioni di sistema sostituendo i valori nel `mssql.conf` file. Per SSIS, si *Impossibile* modificare le impostazioni di sistema sostituendo i valori nel `ssis.conf` file. Il `ssis.conf` file Mostra solo i risultati dell'installazione. Se si desidera modificare le impostazioni per SSIS, è possibile eliminare il `ssis.conf` del file ed eseguire il `setup` nuovo il comando.

Di seguito è riportato un esempio `ssis.conf` file. Ogni campo corrispondente al risultato di un passaggio di installazione.

```
[LICENSE]
                       
registered = Y        
                       
pid = enterprisecore  
                       
[EULA]
                       
accepteula = Y        
                       
[TELEMETRY]
                       
enabled = Y           
                       
[language]
                       
lcid = 2052
```

## <a name="related-content-about-ssis-on-linux"></a>Contenuto correlato su SSIS in Linux
-   [Estrarre, trasformare e caricare i dati in Linux con SSIS](sql-server-linux-migrate-ssis.md)
-   [Installare SQL Server Integration Services (SSIS) in Linux](sql-server-linux-setup-ssis.md)
-   [Limitazioni e problemi noti per SSIS in Linux](sql-server-linux-ssis-known-issues.md)
-   [Esecuzione in Linux con cron pacchetti pianificazione SQL Server Integration Services](sql-server-linux-schedule-ssis-packages.md)
