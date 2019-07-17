---
title: WideWorldImportersDW - flusso di lavoro ETL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f33d36cccbbea6f37139410f9d3d6e03f740ee96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067626"
---
# <a name="wideworldimportersdw-etl-workflow"></a>Flusso di lavoro ETL WideWorldImportersDW
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Usare la *WWI_Integration* pacchetto ETL semplice per eseguire la migrazione dei dati dal database WideWorldImporters al database WideWorldImportersDW le modifiche dei dati. Il pacchetto viene eseguito periodicamente (in genere giornaliera).

Il pacchetto garantisce prestazioni elevate usando SQL Server Integration Services per orchestrare le operazioni bulk T-SQL (anziché separate trasformazioni in Integration Services).

Le dimensioni vengono caricate prima di tutto, e quindi vengono caricate le tabelle dei fatti. È possibile eseguire nuovamente il pacchetto in qualsiasi momento dopo un errore.

Il flusso di lavoro è simile alla seguente:

 ![Flusso di lavoro ETL WideWorldImporters](media/wide-world-importers/wideworldimporters-etl-workflow.png)

Il flusso di lavoro inizia con un'attività di espressione che determina il tempo di cambio data appropriato. Il tempo di cambio data è l'ora corrente meno qualche minuto. (Questo approccio è più affidabile rispetto alla richiesta di destra dei dati sull'ora corrente). Dal momento in cui vengono troncati qualsiasi millisecondi.

L'elaborazione principale avvia popolando la tabella della dimensione Date. L'elaborazione garantisce che siano state popolate tutte le date per l'anno corrente nella tabella.

Successivamente, una serie di attività flusso di dati carica ogni dimensione. Quindi, pagine corrispondenti vengano caricate ogni fatto.

## <a name="prerequisites"></a>Prerequisiti

- SQL Server 2016 (o versione successiva) con i database WideWorldImporters e WideWorldImportersDW (nello stesso o in diverse istanze di SQL Server)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Assicurarsi di creare un catalogo di Integration Services. Per creare un catalogo di Integration Services, in Esplora oggetti di SQL Server Management Studio, fare doppio clic su **Integration Services**, quindi selezionare **Aggiungi catalogo**. Lasciare le opzioni predefinite. Richiesto per attivare SQLCLR e fornire una password.


## <a name="download"></a>Scarica

Per la versione più recente dell'esempio, vedere [wide-world-importers-rilascio](https://go.microsoft.com/fwlink/?LinkID=800630). Scaricare il *ETL.ispac giornaliero* file del pacchetto Integration Services.

Per il codice sorgente ricreare il database di esempio, vedere [wide-world-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl).

## <a name="install"></a>Installazione

1. Distribuire il pacchetto di Integration Services:
   1. In Windows Explorer, aprire il *ETL.ispac giornaliero* pacchetto. Verrà avviata la distribuzione guidata di SQL Server Integration Services.
   2. Sotto **Seleziona origine**, seguono le impostazioni predefinite per la distribuzione del progetto, con il percorso che punta al *ETL.ispac giornaliero* pacchetto.
   3. Sotto **selezionare la destinazione**, immettere il nome del server che ospita il catalogo di Integration Services.
   4. Selezionare un percorso all'interno del catalogo di Integration Services, ad esempio, in una nuova cartella denominata *WideWorldImporters*.
   5. Selezionare **Distribuisci** per completare la procedura guidata.

2. Creare un processo di SQL Server Agent per il processo ETL:
   1. In Management Studio, fare doppio clic **SQL Server Agent**, quindi selezionare **New** > **processo**.
   2. Immettere un nome, ad esempio, *WideWorldImporters ETL*.
   3. Aggiungere un **passaggio processo** del tipo **pacchetto SQL Server Integration Services**.
   4. Selezionare il server contenente il catalogo di Integration Services e quindi selezionare il *ETL giornaliera* pacchetto.
   5. Sotto **Configuration** > **gestioni connessioni**, assicurarsi che le connessioni all'origine e destinazione siano configurate correttamente. Il valore predefinito è per la connessione all'istanza locale.
   6. Selezionare **OK** per creare il processo.

3. Pianificare il processo di esecuzione.
