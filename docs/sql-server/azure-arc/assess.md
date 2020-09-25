---
title: Configurare Valutazione SQL per SQL Server con abilitazione di Azure Arc
titleSuffix: ''
description: Configurare Valutazione SQL per l'istanza di SQL Server con abilitazione di Azure Arc
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 9412348f0d4e76313557b326c18fcb7b2e7087d8
ms.sourcegitcommit: 658c2e0ad958009ce7f041ba1ec0b4af06887497
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2020
ms.locfileid: "91145360"
---
# <a name="configure-on-demand-sql-assessment-for-azure-arc-enabled-sql-server-instance"></a>Configurare Valutazione SQL su richiesta per l'istanza di SQL Server con abilitazione di Azure Arc

È possibile abilitare Valutazione SQL per le istanze di SQL Server attenendosi alla seguente procedura.

## <a name="prerequisites"></a>Prerequisiti

* L'istanza di SQL Server è connessa ad Azure Arc. Seguire queste istruzioni per [caricare l'istanza di SQL Server in SQL Server con abilitazione di Arc](connect.md).

* L'estensione MMA viene installata e configurata nel computer. Seguire queste istruzioni per [installare Microsoft Monitoring Agent (MMA)](configure-advanced-data-security.md#install-microsoft-monitoring-agent-mma). Per altre informazioni, vedere [Agente di Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent).

* Il [protocollo TCP/IP è abilitato](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) per l'istanza di SQL Server.

* [SQL Server Browser](../../tools/configuration-manager/sql-server-browser-service.md) viene eseguito se si usa un'istanza denominata di SQL Server.

* Il documento di SQL Server è stato esaminato nei [prerequisiti per le valutazioni su richiesta dell'hub Servizi](https://docs.microsoft.com/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents).

## <a name="enable-on-demand-sql-assessment"></a>Abilitare Valutazione SQL su richiesta

1. Aprire la risorsa SQL Server - Azure Arc e selezionare __Environment Health__ (Integrità dell'ambiente) nel menu a sinistra.

   ![Selezione di Valutazione SQL](media/assess/sql-assessment-heading-sql-server-arc.png)

1. Specificare una directory di lavoro nel computer di raccolta dati. Durante la raccolta e l'analisi, i dati vengono archiviati temporaneamente in tale cartella. Se la cartella non esiste, viene creata automaticamente.

1. Fare clic su __Scarica script di configurazione del dispositivo__ e copiare lo script scaricato nel computer di destinazione.

1. Avviare un'istanza di amministrazione di __powershell.exe__ ed eseguire una delle operazioni seguenti: 
   * Se si usa un account di dominio, eseguire i comandi seguenti. Verrà richiesto di specificare account utente e password. 

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1'
      ```

    * Se si usa un account MSA, eseguire i comandi seguenti.

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1' -ManagedServiceAccountName <MSA account name>
      ```

   > [!NOTE]
   > Lo script pianifica un'attività denominata *SQLAssessment* da eseguire entro un'ora dall'esecuzione dello script precedente e poi ogni 7 giorni. L'attività può essere modificata in modo da eseguirla in una data e ora diverse o addirittura forzarne l'esecuzione immediata dalla libreria dell'utilità di pianificazione > Microsoft > Operations Management Suite > AOI*** > Valutazioni > SQLAssessment. Questa attività attiva la raccolta dei dati.

## <a name="view-the-assessment-results"></a>Visualizzare i risultati della valutazione

Il pulsante di __visualizzazione dei risultati di Valutazione SQL__ nel pannello _Environment Health_ (Integrità dell'ambiente) è disabilitato finché i risultati non sono pronti in Log Analytics. Dopo aver attivato il pulsante, è possibile fare clic su di esso per visualizzare i risultati. Potrebbero trascorrere fino a 2 ore prima che i risultati vengano visualizzati in Log Analytics dopo l'elaborazione dei file di dati nel computer di destinazione.

![SQL: risultati della valutazione](media/assess/sql-assessment-results.png)

È possibile visualizzare lo stato di elaborazione dei dati nel computer della raccolta controllando i file nella cartella di lavoro. Al termine dell'attività pianificata, verranno visualizzati diversi file con il prefisso _new._ nella directory di lavoro:

![File di dati pronti](media/assess/sql-assessment-data-files-ready.png)

Microsoft Monitoring Agent analizza la cartella di lavoro ogni 15 minuti cercando i file _new.*_ e invia i dati all'area di lavoro di Log Analytics. Caricato il file, il prefisso cambierà da _new._ a _processed._ :

![File di dati elaborati](media/assess/sql-assessment-data-files-processed.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere il documento di SQL Server nei [prerequisiti per le valutazioni su richiesta dell'hub Servizi](https://docs.microsoft.com/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents).

Per ottenere il supporto completo di Valutazione SQL su richiesta, è necessaria la sottoscrizione a un contratto di supporto Premier o Unified. Per informazioni dettagliate, vedere [Supporto tecnico Premier di Microsoft Azure](https://azure.microsoft.com/support/plans/premier).
