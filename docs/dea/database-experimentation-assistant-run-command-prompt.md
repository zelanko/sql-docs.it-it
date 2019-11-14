---
title: Esegui Database Experimentation Assistant al prompt dei comandi
description: Esegui Database Experimentation Assistant al prompt dei comandi
ms.custom: seo-lt-2019
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: c3b87eafa460cfef69666a3837f56626dab81d47
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056567"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt-sql-server"></a>Esegui Database Experimentation Assistant al prompt dei comandi (SQL Server)

Questo articolo descrive come usare la finestra del prompt dei comandi per acquisire una traccia in Database Experimentation Assistant (DEA), quindi analizzare i risultati. 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>Avviare una nuova acquisizione del carico di lavoro tramite il comando DEA

Per avviare una nuova acquisizione del carico di lavoro, eseguire il comando seguente:

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**Esempio**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>Riprodurre un carico di lavoro

1.  Accedere al computer del controller di Riesecuzione distribuita.
2.  Convertire la traccia del carico di lavoro acquisita usando il comando DEA in un file IRF:

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  Avviare un'acquisizione di traccia nel computer di destinazione che esegue SQL Server utilizzando StartReplayCaptureTrace. SQL.
       
    A.  In SQL Server Management Studio (SSMS) aprire < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql.
    
    b.  Eseguire `Set @durationInMins=0` in modo che l'acquisizione della traccia non venga arrestata automaticamente dopo un periodo di tempo specificato.
    
    c.  Per impostare le dimensioni massime del file per ogni file di traccia, eseguire `Set @maxfilesize`. La dimensione consigliata è 200 (in MB).
    
    d.  Modificare `@Tracefile` per impostare un nome univoco per il file di traccia.
    
    e.  Modificare `@dbname` per specificare un nome di database se il carico di lavoro deve essere acquisito solo in un database specifico. Per impostazione predefinita, il carico di lavoro sull'intero server viene acquisito. 
4.  Riprodurre il file IRF nell'istanza di SQL Server di destinazione:

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    A.  Per monitorare lo stato, aprire una finestra del prompt dei comandi ed eseguire `DReplay status -f 1`.
        
    b.  Per arrestare la riproduzione, ad esempio se si nota che il superamento% è inferiore al previsto, aprire una finestra del prompt dei comandi ed eseguire `DReplay cancel`.

5.  Arrestare l'acquisizione di traccia nell'istanza di SQL Server di destinazione.
6.  In SSMS aprire `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`.
7.  Modificare `@Tracefile` in modo che corrisponda al percorso del file di traccia nel computer di destinazione che esegue SQL Server.
8.  Eseguire lo script nel computer di destinazione che esegue SQL Server.

## <a name="analyze-traces-by-using-the-dea-command"></a>Analizzare le tracce tramite il comando DEA

Per avviare una nuova analisi della traccia, eseguire il comando seguente:

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**Esempio**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>Passaggi successivi

Per un'introduzione di 19 minuti a DEA e dimostrazione, Guarda il video seguente:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
