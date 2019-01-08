---
title: Creare la business intelligence (BI) i flussi di lavoro con R - servizi di SQL Server Machine Learning
description: Supportano di scenari di integrazione di combinazione di business intelligence (BI) e il linguaggio R in SQL Server e SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 32dfb3317cb790c19289ab02362bf8ee765e5259
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432734"
---
# <a name="creating-bi-workflows-with-r"></a>Creazione di flussi di lavoro di Business Intelligence con R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Un database relazionale è una tecnologia altamente ottimizzata per la realizzazione di soluzioni scalabili per l'elaborazione delle transazioni, l'archiviazione e l'esecuzione di query sui dati.

Al contrario, in genere soluzioni R generalmente si basavano sull'importazione di dati da diverse origini, spesso in formato CSV, per eseguire ulteriore esplorazione dei dati e modellazione. Si tratta di procedure non solo poco efficienti, ma anche non sicure.

Questo articolo descrive gli scenari di integrazione di R con SQL Server in cui evitare i problemi più comuni e i rischi di sicurezza che può verificarsi se all'esterno del database vengono sviluppate soluzioni di machine learning.

Vengono inoltre descritti alcuni esempi di come applicazioni di business intelligence, in particolare in Integration Services e Reporting Services, possono interagire con il codice R e usare i dati o gli elementi grafici generati da R.

Si applica a: SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

## <a name="bring-compute-power-to-the-data"></a>Potenza di calcolo ai dati

È stato un obiettivo chiave nella progettazione dell'integrazione di apprendimento automatico con SQL Server per portare analitica vicino ai dati. Ciò offre diversi vantaggi:

+ Sicurezza dei dati. Offrendo l'avvicinamento di R per l'origine dei dati consente di evitare lo spostamento dei dati inutili e non sicuri.

+ Velocità. I database sono ottimizzati per le operazioni basate su set. Le innovazioni recenti per i database, ad esempio le tabelle in memoria rendono i riepiloghi e aggregazioni fulmine e sono la soluzione ideale per l'analisi scientifica dei dati.

+ Facilità di integrazione e distribuzione. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è il punto centrale di operazioni per molte altre attività di gestione dati e applicazioni. Utilizzando i dati che si trovano nel database o warehouse per reporting, assicurarsi che i dati usati da soluzioni di machine learning siano coerenti e aggiornati. 

+ Efficienza tra cloud e locali. Invece di elaborare i dati in R, è possibile usare le pipeline di dati aziendali, inclusi [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e Azure Data Factory. La creazione di report con i risultati o l'analisi è semplice con Power BI o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

Con la giusta combinazione di SQL e R per le diverse attività di elaborazione e analisi di dati, sia i data scientist che gli sviluppatori possono essere più produttivi.

## <a name="use-integration-services-for-data-transformation-and-automation"></a>Utilizzare Integration Services per i dati di trasformazione e automazione

I flussi di lavoro per l'analisi scientifica dei dati sono altamente iterativi e implicano molte trasformazioni dei dati, tra cui ridimensionamento, aggregazioni, calcolo delle probabilità, ridenominazione e unione degli attributi. I data scientist sono abituati a eseguire molte di queste attività in R, Python o con un altro linguaggio, ma, per eseguire tali flussi di lavoro su dati aziendali, è necessaria la perfetta integrazione con strumenti e processi ETL.

Poiché [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consente di eseguire operazioni complesse in R tramite Transact-SQL e stored procedure, è possibile integrare attività specifiche di R con i processi ETL esistenti senza dover intervenire per adattare lo sviluppo. Anziché eseguire una serie di attività a elevato utilizzo di memoria in R, la preparazione dei dati può essere ottimizzata usando gli strumenti più efficienti, tra cui [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Di seguito sono riportate alcune idee per come è possibile automatizzare l'elaborazione dei dati e pipeline di modellazione in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Usare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] attività per creare le funzionalità di dati necessari nel database SQL
+ Usare la diramazione condizionale per cambiare il contesto di calcolo per i processi R
+ Eseguire processi R che generano i propri dati nel database e condividere dati con le applicazioni
+ Quando si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], caricare lo script R salvato in una variabile di testo ed eseguirlo in SQL Server

### <a name="examples"></a>Esempi

[Rendere operativo il progetto di Machine Learning usando SSIS e R Services di SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  

Questo post di blog illustra le tecniche di base per la modifica di codice R usando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: 

+ Chiamare R usando l'attività Esegui SQL per generare i dati e salvarli in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

+ Usare una stored procedure per eseguire il training di un modello R e archiviarlo nel database

+ Eseguire l'assegnazione dei punteggi al modello usando l'attività Script e l'attività Esegui SQL

##  <a name="bkmk_ssrs"></a> Utilizzare Reporting Services per la visualizzazione

Anche se R consente di creare grafici e visualizzazioni interessanti, non è ben integrato con le origini dati esterne e questo significa che ogni grafico deve essere prodotto singolarmente. Anche la condivisione può essere difficile.

Con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] è possibile eseguire operazioni complesse in R tramite stored procedure di [!INCLUDE[tsql](../../includes/tsql-md.md)], facilmente accessibili da un'ampia gamma di strumenti per la creazione di report aziendali, tra cui [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e Power BI.

+ Visualizzare gli oggetti grafici restituiti da uno script R con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
+ Usare la tabella in Power BI

### <a name="examples"></a>Esempi

[R Graphics Device for Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/) (R Graphics Device per Microsoft Reporting Services - SSRS)

Questo progetto CodePlex fornisce il codice che consente di creare un elemento del report personalizzato che esegue il rendering dell'output grafico di R come immagine utilizzabile nei report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  Usando l'elemento del report personalizzato, è possibile:

+ Pubblicare i grafici e i tracciati creati usando R Graphics Device nei dashboard di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]

+ Passare i parametri di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ai tracciati R

> [!NOTE]
> Per questo esempio, il codice che supporta R Graphics Device per Reporting Services deve essere installato nel server di Reporting Services, nonché in Visual Studio. Sono anche necessarie la compilazione e la configurazione manuali.
