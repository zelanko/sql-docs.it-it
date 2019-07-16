---
title: Esecuzione di Assistente di sperimentazione di Database un prompt dei comandi per gli aggiornamenti di SQL Server
description: Eseguire Assistente configurazione sperimentazione Database a un prompt dei comandi
ms.custom: ''
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
ms.openlocfilehash: 475c3dc1366e69dbc164547bbf5dfc8c06515c56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050476"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>Eseguire Assistente configurazione sperimentazione Database a un prompt dei comandi

Questo articolo descrive come usare la finestra del prompt dei comandi per acquisire una traccia nel Database sperimentazione Assistant DEA () e quindi analizzare i risultati. 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>Avviare una nuova acquisizione del carico di lavoro usando il comando DEA

Per avviare un nuovo carico di lavoro di acquisizione, eseguire il comando seguente:

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**Esempio**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>Riprodurre un carico di lavoro

1.  Accedere al computer del controller di riesecuzione distribuita.
2.  Convertire la traccia del carico di lavoro usando il comando DEA in un file IRF acquisita:

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  Avviare un'acquisizione di traccia nel computer di destinazione che esegue SQL Server usando StartReplayCaptureTrace.sql.
       
    a.  In SQL Server Management Studio (SSMS), aprire < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql.
    
    b.  Eseguire `Set @durationInMins=0` in modo che l'acquisizione della traccia non viene interrotta automaticamente dopo un periodo di tempo specificato.
    
    c.  Per impostare la dimensione massima del file per ogni file di traccia, eseguire `Set @maxfilesize`. La dimensione consigliata è 200 (in MB).
    
    d.  Modifica `@Tracefile` per impostare un nome univoco per il file di traccia.
    
    e.  Modifica `@dbname` per specificare un nome di database, se il carico di lavoro deve essere acquisito solo su un database specifico. Per impostazione predefinita, viene acquisito il carico di lavoro dell'intero server. 
4.  Riprodurre il file IRF sull'istanza di SQL Server di destinazione:

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    a.  Per monitorare lo stato, aprire una finestra del prompt dei comandi ed eseguire `DReplay status -f 1`.
        
    b.  Per arrestare la riproduzione, ad esempio come se si nota che il pass è inferiore al previsto, aprire una finestra del prompt dei comandi ed eseguire `DReplay cancel`.

5.  Arrestare l'acquisizione di traccia nell'istanza di SQL Server di destinazione.
6.  In SSMS aprire `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`.
7.  Modifica `@Tracefile` in base al percorso di file di traccia nel computer di destinazione che esegue SQL Server.
8.  Eseguire questo script sul computer di destinazione che esegue SQL Server.

## <a name="analyze-traces-by-using-the-dea-command"></a>Analizzare le tracce utilizzando il comando DEA

Per avviare una nuova analisi della traccia, eseguire il comando seguente:

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**Esempio**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>Passaggi successivi

Per un'introduzione di 19 minuti DEA e dimostrazione, guardare il video seguente:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
