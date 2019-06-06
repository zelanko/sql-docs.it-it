---
title: Pianificare i pacchetti SSIS in Linux con cron | Microsoft Docs
description: Questo articolo descrive come pianificare i pacchetti di SQL Server Integration Services (SSIS) in Linux con il servizio cron.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 6d78190f5c6acf1f5dc8bfaccbf072a290faa908
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705320"
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>Esecuzione in Linux con cron pacchetti pianificazione SQL Server Integration Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Quando si esegue SQL Server Integration Services (SSIS) e SQL Server in Windows, è possibile automatizzare l'esecuzione di pacchetti SSIS utilizzando SQL Server Agent. Quando si esegue SQL Server e SSIS in Linux, tuttavia, l'utilità di SQL Server Agent non è disponibile per pianificare i processi in Linux. È invece possibile utilizzare il servizio cron, che è ampiamente usato nelle piattaforme Linux per automatizzare l'esecuzione del pacchetto.

Questo articolo fornisce esempi che illustrano come automatizzare l'esecuzione di pacchetti SSIS. Gli esempi sono scritti per l'esecuzione su Red Hat Enterprise. Il codice è simile per le altre distribuzioni Linux, ad esempio Ubuntu.

## <a name="prerequisites"></a>Prerequisiti

Prima di usare il servizio cron per eseguire i processi, verificare se è in esecuzione nel computer.

Per controllare lo stato del servizio cron, usare il comando seguente: `systemctl status crond.service`.

Se il servizio non è attivo (vale a dire, non è già in esecuzione), contattare l'amministratore per installare e configurare correttamente il servizio cron.

## <a name="create-jobs"></a>Creare i processi

Un processo cron è un'attività che è possibile configurare per eseguire regolarmente un intervallo specificato. Il processo può essere semplice quanto un comando che è in genere digitare direttamente nella console o eseguire come script della shell.

Per semplificare la gestione e scopi di manutenzione, è consigliabile inserire i comandi di esecuzione del pacchetto in uno script che contiene un nome descrittivo.

Ecco un esempio di uno script della shell semplice per l'esecuzione di un pacchetto. Contiene solo un singolo comando, ma è possibile aggiungere ulteriori comandi in base alle esigenze.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Pianificare processi con il servizio cron

Dopo aver definito i processi, è possibile pianificare per l'esecuzione automatica mediante il servizio cron.

Per aggiungere il processo per cron per l'esecuzione, aggiungere il processo nel file crontab. Per aprire il file crontab in un editor in cui è possibile aggiungere o aggiornare il processo, usare il comando seguente: `crontab -e`.

Per pianificare il processo descritto in precedenza per l'esecuzione ogni giorno alle 2.00: 10, aggiungere la riga seguente al file crontab:

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Salvare il file di crontab e quindi chiudere l'editor.

Per comprendere il formato del comando di esempio, esaminare le informazioni nella sezione seguente.
 
## <a name="format-of-a-crontab-file"></a>Formato di un file crontab

L'immagine seguente mostra il formato di descrizione della riga di processo che viene aggiunto al file crontab.

![Formato di descrizione per la voce nel file crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

Per ottenere una descrizione più dettagliata del formato di file crontab, usare il comando seguente: `man 5 crontab`.

Ecco un esempio parziale dell'output che aiuta a spiegare l'esempio in questo articolo:

![Descrizione parziale dettagliata del formato crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>Contenuto correlato su SSIS in Linux
-   [Estrarre, trasformare e caricare i dati in Linux con SSIS](sql-server-linux-migrate-ssis.md)
-   [Installare SQL Server Integration Services (SSIS) in Linux](sql-server-linux-setup-ssis.md)
-   [Configurare SQL Server Integration Services in Linux con ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitazioni e problemi noti per SSIS in Linux](sql-server-linux-ssis-known-issues.md)
