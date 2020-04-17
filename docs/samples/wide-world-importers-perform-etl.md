---
title: WideWorldImportersDW - Flusso di lavoro ETL Documenti Microsoft
description: Utilizzare il pacchetto ETL con SQL Server Integration Services (SSIS) per eseguire periodicamente la migrazione dei dati dal database WideWorldImporters a WideWorldImportersDW.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 98ce2b9aa11b2e1381da1f16455df8a2c0d3f243
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487430"
---
# <a name="wideworldimportersdw-etl-workflow"></a>Flusso di lavoro ETL WideWorldImportersDW
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Utilizzare il pacchetto ETL *WWI_Integration* per eseguire la migrazione dei dati dal database WideWorldImporters al database WideWorldImportersDW quando i dati vengono modificati. Il pacchetto viene eseguito periodicamente (in genere ogni giorno).

Il pacchetto garantisce prestazioni elevate utilizzando SQL Server Integration ServicesIntegration Services per orchestrare le operazioni T-SQL di massa (anziché trasformazioni separate in Integration ServicesIntegration Services).

Le dimensioni vengono caricate prima, quindi le tabelle dei fatti vengono caricate. È possibile eseguire nuovamente il pacchetto in qualsiasi momento dopo un errore.

Il flusso di lavoro è simile al seguente:The workflow looks like this:

 ![Flusso di lavoro ETL WideWorldImporters](media/wide-world-importers/wideworldimporters-etl-workflow.png)

Il flusso di lavoro inizia con un'attività di espressione che determina il tempo limite appropriato. Il tempo limite è l'ora corrente meno pochi minuti. (Questo approccio è più affidabile rispetto alla richiesta di dati direttamente all'ora corrente.) Eventuali millisecondi vengono troncati dall'ora.

L'elaborazione principale inizia compilando la tabella delle dimensioni Data. L'elaborazione garantisce che tutte le date per l'anno corrente siano state inserite nella tabella.

Successivamente, una serie di attività del flusso di dati carica ogni dimensione. Poi, caricano ogni fatto.

## <a name="prerequisites"></a>Prerequisiti

- SQL Server 2016 (o versione successiva) con i database WideWorldImporters e WideWorldImportersDW (nello stesso caso o in istanze diverse di SQL Server)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Assicurarsi di creare un catalogo di Integration ServicesIntegration Services . Per creare un catalogo di Integration ServicesIntegration Services , in Esplora oggetti di SQL Server Management StudioSQL Server Management Studio fare clic con il pulsante destro del mouse su **Integration ServicesIntegration Services**e quindi scegliere **Aggiungi catalogo**. Lasciare le opzioni predefinite. Viene richiesto di abilitare SQLCLR e fornire una password.


## <a name="download"></a>Download

Per la versione più recente dell'esempio, vedere [wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630). Scaricare il file di pacchetto *Daily ETL.ispac* Integration Services.

Per il codice sorgente per ricreare il database di esempio, vedere [wide-world-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-ssis).

## <a name="install"></a>Installazione

1. Distribuire il pacchetto di Integration ServicesIntegration Services :
   1. In Esplora risorse aprire il pacchetto *Daily ETL.ispac.* Verrà avviata la Distribuzione guidata di SQL Server Integration Services.
   2. In **Seleziona origine**, seguire le impostazioni predefinite per Distribuzione progetto, con il percorso che punta al pacchetto Daily *ETL.ispac.*
   3. In **Seleziona destinazione**immettere il nome del server che ospita il catalogo di Integration ServicesIntegration Services .
   4. Selezionare un percorso nel catalogo di Integration ServicesIntegration Services , ad esempio, in una nuova cartella denominata *WideWorldImporters*.
   5. Selezionare **Distribuisci** per completare la procedura guidata.

2. Creare un processo di SQL Server Agent per il processo ETL:Create a SQL Server Agent job for the ETL process:
   1. In Management StudioManagement Studio fare clic con il pulsante destro del mouse su **Agente SQL Server**, quindi scegliere **Nuovo** > **processo**.
   2. Immettere un nome, ad esempio *WideWorldImporters ETL*.
   3. Aggiungere un **passaggio di** processo di tipo **Pacchetto di SQL Server Integration Services**.
   4. Selezionare il server con il catalogo di Integration ServicesIntegration Services e quindi selezionare il pacchetto *ETL giornaliero.*
   5. In**Gestioni connessioni**di **configurazione** > verificare che le connessioni all'origine e alla destinazione siano configurate correttamente. L'impostazione predefinita prevede la connessione all'istanza locale.
   6. Selezionare **OK** per creare il processo.

3. Eseguire o pianificare il processo.
