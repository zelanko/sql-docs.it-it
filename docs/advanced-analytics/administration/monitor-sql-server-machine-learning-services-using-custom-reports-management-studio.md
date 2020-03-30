---
title: Monitorare gli script con report personalizzati
description: Usare report personalizzati in SQL Server Management Studio (SSMS) per monitorare l'esecuzione di script esterni (Python ed R) e le risorse usate, diagnosticare i problemi e ottimizzare le prestazioni in Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: afc90985fc7c0c6d7a04cb575ee9e93a4b7b4c51
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727752"
---
# <a name="monitor-python-and-r-script-execution-using-custom-reports-in-sql-server-management-studio"></a>Monitorare l'esecuzione di script Python ed R tramite report personalizzati in SQL Server Management Studio
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Usare report personalizzati in SQL Server Management Studio (SSMS) per monitorare l'esecuzione di script esterni (Python ed R) e le risorse usate, diagnosticare i problemi e ottimizzare le prestazioni in Machine Learning Services per SQL Server.

In questi report è possibile visualizzare dettagli quali:

- Sessioni Python o R attive
- Impostazioni di configurazione per l'istanza
- Statistiche di esecuzione per i processi di Machine Learning
- Eventi estesi per R Services
- Pacchetti di Python o R installati nell'istanza corrente

Questo articolo spiega come installare e usare i report personalizzati disponibili per Machine Learning Services per SQL Server.

Per altre informazioni sui report in SQL Server Management Studio, vedere [Report personalizzati in Management Studio](../../ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>Come installare i report

I report vengono progettati usando SQL Server Reporting Services, ma possono essere usati direttamente da SQL Server Management Studio. Non è necessario che Reporting Services sia installato nell'istanza di SQL Server.

Per usare questi report, seguire questa procedura:

1. Scaricare i [report personalizzati di SSMS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) per Machine Learning Services per SQL Server da GitHub.

2. Copiare i report in Management Studio

    1. Individuare la cartella dei report personalizzati usata da SQL Server Management Studio. Per impostazione predefinita, i report personalizzati vengono archiviati in questa cartella (dove **user_name** corrisponde al nome utente Windows):

        `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

       È anche possibile specificare una cartella diversa oppure creare sottocartelle.

    2. Copiare i file con estensione RDL scaricati in precedenza nella cartella dei report personalizzati.

3. Eseguire i report in Management Studio

    1. In Management Studio fare doppio clic sul nodo **Database** per l'istanza in cui si vogliono eseguire i report.

    2. Fare clic su **Report**e quindi su **Report personalizzati**.

    3. Nella finestra di dialogo **Apri file** individuare la cartella dei report personalizzati.

    4. Selezionare uno dei file RDL scaricati e fare clic su **Apri**.

## <a name="reports"></a>Report

Il [repository dei report di SSMS personalizzati in GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) include i report seguenti:

| Report | Descrizione |
|-|-|
| Sessioni attive | Gli utenti connessi all'istanza di SQL Server che stanno eseguendo uno script Python o R. |
| Configurazione | Impostazioni di installazione di Machine Learning Services e proprietà del runtime Python o R. |
| Configure Instance (Configura istanza) | Configurazione di Machine Learning Services. |
| Execution Statistics (Statistiche di esecuzione) | Statistiche di esecuzione di Machine Learning Services. È ad esempio possibile ottenere il numero totale di esecuzioni di script esterni e il numero di esecuzioni parallele. |
| Eventi estesi | Eventi estesi disponibili per ottenere altre informazioni dettagliate sull'esecuzione di script esterni. |
| Pacchetti | Creazione dell'elenco dei pacchetti R o Python installati nell'istanza di SQL Server e delle relative proprietà, ad esempio la versione e il nome. |
| Resource Usage | Visualizzazione della CPU, della memoria, del consumo di I/O di SQL Server e dell'esecuzione di script esterni. È anche possibile visualizzare l'impostazione relativa alla memoria per i pool di risorse esterni. |

## <a name="next-steps"></a>Passaggi successivi

- [Monitorare Machine Learning Services per SQL Server tramite DMV](monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
- [Eventi estesi per R Services](../r/extended-events-for-sql-server-r-services.md)
