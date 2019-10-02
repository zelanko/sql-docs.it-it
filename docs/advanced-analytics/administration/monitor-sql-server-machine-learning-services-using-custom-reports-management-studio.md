---
title: Monitorare l'esecuzione di script Python e R usando report personalizzati in SSMS
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 549cdcd35b939b2247b14817271e3d1063fab1e0
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714395"
---
# <a name="monitor-python-and-r-script-execution-using-custom-reports-in-sql-server-management-studio"></a>Monitorare l'esecuzione di script Python e R usando report personalizzati in SQL Server Management Studio
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Usare i report personalizzati in SQL Server Management Studio (SSMS) per monitorare l'esecuzione di script esterni (Python e R), le risorse usate, diagnosticare i problemi e ottimizzare le prestazioni in SQL Server Machine Learning Services.

In questi report è possibile visualizzare i dettagli, ad esempio:

- Sessioni Python o R attive
- Impostazioni di configurazione per l'istanza
- Statistiche di esecuzione per i processi di Machine Learning
- Eventi estesi per R Services
- Pacchetti Python o R installati nell'istanza corrente

Questo articolo illustra come installare e usare i report personalizzati forniti per SQL Server Machine Learning Services.

Per ulteriori informazioni sui report in SQL Server Management Studio, vedere [Custom Reports in Management Studio](../../ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>Come installare i report

I report vengono progettati utilizzando SQL Server Reporting Services, ma possono essere utilizzati direttamente da SQL Server Management Studio. Non è necessario che Reporting Services sia installato nell'istanza di SQL Server.

Per usare questi report, seguire questa procedura:

1. Scaricare i [report personalizzati di SSMS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) per SQL Server Machine Learning Services da GitHub.

2. Copiare i report in Management Studio

    1. Individuare la cartella dei report personalizzati usata da SQL Server Management Studio. Per impostazione predefinita, i report personalizzati vengono archiviati in questa cartella (dove **user_name** è il nome utente di Windows):

        `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

       È anche possibile specificare una cartella diversa o creare sottocartelle.

    2. Copiare *. File RDL scaricati nella cartella dei report personalizzati.

3. Eseguire i report in Management Studio

    1. In Management Studio fare doppio clic sul nodo **Database** per l'istanza in cui si vogliono eseguire i report.

    2. Fare clic su **Report**e quindi su **Report personalizzati**.

    3. Nella finestra di dialogo **Apri file** individuare la cartella dei report personalizzati.

    4. Selezionare uno dei file RDL scaricati e fare clic su **Apri**.

## <a name="reports"></a>Report

Il [repository dei report personalizzati di SSMS in GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) include i report seguenti:

| Report | Descrizione |
|-|-|
| Sessioni attive | Utenti attualmente connessi all'istanza di SQL Server ed esecuzione di uno script Python o R. |
| Configurazione | Impostazioni di installazione di Machine Learning Services e proprietà del runtime Python o R. |
| Configura istanza | Configurare Machine Learning Services. |
| Statistiche di esecuzione | Statistiche di esecuzione dei servizi Machine Learning. Ad esempio, è possibile ottenere il numero totale di esecuzioni di script esterni e il numero di esecuzioni parallele. |
| Eventi estesi | Eventi estesi disponibili per ottenere maggiori informazioni sull'esecuzione di script esterni. |
| Pacchetti | Elencare i pacchetti R o Python installati nell'istanza di SQL Server e le relative proprietà, ad esempio la versione e il nome. |
| Resource Usage | Visualizza la CPU, la memoria, il consumo di i/o di SQL Server e l'esecuzione di script esterni. È anche possibile visualizzare l'impostazione della memoria per i pool di risorse esterni. |

## <a name="next-steps"></a>Passaggi successivi

- [Monitorare SQL Server Machine Learning Services mediante le viste a gestione dinamica (DMV)](monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
- [Eventi estesi per R Services](../r/extended-events-for-sql-server-r-services.md)
