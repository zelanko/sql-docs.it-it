---
title: Esegui Database Experimentation Assistant al prompt dei comandi
description: Esegui Database Experimentation Assistant al prompt dei comandi
ms.custom: seo-lt-2019
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: f5a0f7441dd17aec2587c772a678a3681fd3b423
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74317724"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>Esegui Database Experimentation Assistant al prompt dei comandi

Questo articolo descrive come acquisire una traccia in Database Experimentation Assistant (DEA) e quindi analizzare i risultati, tutto da un prompt dei comandi.

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>Avviare una nuova acquisizione del carico di lavoro tramite il comando DEA

Per avviare una nuova acquisizione del carico di lavoro, al prompt dei comandi eseguire il comando seguente:

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**Esempio**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload-capture"></a>Riprodurre un'acquisizione del carico di lavoro

1. Accedere al computer del controller di Riesecuzione distribuita.
2. Per convertire la traccia del carico di lavoro acquisita usando il comando DEA in un file IRF, al prompt dei comandi eseguire il comando seguente:

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3. Avviare un'acquisizione di traccia nel computer di destinazione che esegue SQL Server utilizzando StartReplayCaptureTrace. SQL.

    a.  In SQL Server Management Studio (SSMS) aprire <Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.SQL.

    b.  Eseguire `Set @durationInMins=0` in modo che l'acquisizione della traccia non venga arrestata automaticamente dopo un periodo di tempo specificato.

    c.  Per impostare le dimensioni massime del file per ogni file `Set @maxfilesize`di traccia, eseguire. La dimensione consigliata è 200 (in MB).

    d.  Modificare `@Tracefile` per impostare un nome univoco per il file di traccia.

    e.  Modificare `@dbname` per specificare un nome di database se il carico di lavoro deve essere acquisito solo in un database specifico. Per impostazione predefinita, il carico di lavoro sull'intero server viene acquisito.

4. Per riprodurre il file IRF nell'istanza di SQL Server di destinazione, al prompt dei comandi eseguire il comando seguente:

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`

    a.  Per monitorare lo stato, al prompt dei comandi eseguire `DReplay status -f 1`.

    b.  Per arrestare la riproduzione, ad esempio se si nota che il passaggio% è inferiore al previsto, al prompt dei comandi eseguire `DReplay cancel`.

5. Arrestare l'acquisizione di traccia nell'istanza di SQL Server di destinazione.
6. In SSMS aprire `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`.
7. Modificare `@Tracefile` in modo che corrisponda al percorso del file di traccia nel computer di destinazione che esegue SQL Server.
8. Eseguire lo script nel computer di destinazione che esegue SQL Server.

## <a name="analyze-traces-using-the-dea-command"></a>Analizzare le tracce tramite il comando DEA

Per avviare una nuova analisi della traccia, al prompt dei comandi eseguire il comando seguente:

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**Esempio**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="see-also"></a>Vedere anche

- Per ulteriori informazioni sull'utilizzo di DEA, vedere [Panoramica di database Experimentation Assistant](database-experimentation-assistant-overview.md).
