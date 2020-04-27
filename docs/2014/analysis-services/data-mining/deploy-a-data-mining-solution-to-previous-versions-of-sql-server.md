---
title: Distribuire una soluzione di data mining a versioni precedenti di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [Analysis Services]
- holdout [data mining]
- deploy [Analysis Services]
- time series [Analysis Services]
- deploying [Analysis Services - data mining]
- synchronization [Analysis Services]
- deployment [Analysis Services]
ms.assetid: 2715c245-f206-43af-8bf5-e6bd2585477a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc721d58c69b0275c9846863f761d60db66e5aaf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084682"
---
# <a name="deploy-a-data-mining-solution-to-previous-versions-of-sql-server"></a>Distribuire una soluzione di data mining in versioni precedenti di SQL Server
  In questa sezione vengono descritti i problemi di compatibilità noti che possono verificarsi quando si tenta di distribuire in un database che utilizza SQL Server 2005 Analysis Services una struttura o un modello di data mining creato in un'istanza di [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] oppure quando si distribuiscono in un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]modelli creati in SQL Server 2005.  
  
 La distribuzione in un'istanza di SQL Server 2000 Analysis Services non è supportata.  
  
 [Distribuzione di modelli Time Series](#bkmk_TimeSeries)  
  
 [Distribuzione di modelli con dati di controllo](#bkmk_Holdout)  
  
 [Distribuzione di modelli con filtri](#bkmk_Filter)  
  
 [Ripristino da backup di database](#bkmk_Backup)  
  
 [Utilizzo della sincronizzazione del database](#bkmk_Synch)  
  
##  <a name="deploying-times-series-models"></a><a name="bkmk_TimeSeries"></a> Distribuzione di modelli Time Series  
 In SQL Server 2008 l'algoritmo Microsoft Time Series è stato migliorato mediante l'aggiunta di un secondo algoritmo complementare, ARIMA. Per altre informazioni sulle modifiche apportate all'algoritmo Time Series, vedere [Algoritmo Microsoft Time Series](microsoft-time-series-algorithm.md).  
  
 I modelli di data mining Time Series che utilizzano il nuovo algoritmo ARIMA possono pertanto presentare un comportamento diverso quando vengono distribuiti in un'istanza di SQL Server 2005 Analysis Services.  
  
 Se è stato impostato in modo esplicito il parametro PREDICTION_SMOOTHING per controllare la combinazione della stima dei modelli ARTXP e ARIMA, quando il modello viene distribuito in un'istanza di SQL Server 2005, in Analysis Services viene generato un errore per segnalare che il parametro non è valido. Per evitare l'errore, è necessario eliminare il parametro PREDICTION_SMOOTHING e convertire i modelli in un modello esclusivamente ARTXP.  
  
 Viceversa, se si distribuisce in un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]un modello Time Series creato con SQL Server 2005 Analysis Services, quando si apre il modello di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], i file di definizione vengono prima convertiti nel nuovo formato e due nuovi parametri vengono aggiunti per impostazione predefinita a tutti i modelli Time Series. Il parametro FORECAST_METHOD viene aggiunto con valore predefinito MIXED e il parametro PREDICTION_SMOOTHING viene aggiunto con valore predefinito 0,5. Fino a quando non si rielabora il modello, tuttavia, il modello continua a utilizzare solo ARTXP per le previsioni. Non appena si rielabora il modello, la stima cambia per utilizzare sia ARIMA sia ARTXP.  
  
 Per evitare di modificare il modello, è pertanto necessario limitarsi a esplorare il modello senza mai elaborarlo. In alternativa, è possibile impostare in modo esplicito i parametri FORECAST_METHOD o PREDICTION_SMOOTHING.  
  
 Per informazioni dettagliate sulla configurazione dei modelli misti, vedere [Riferimento tecnico per l'algoritmo Microsoft Time Series](microsoft-time-series-algorithm-technical-reference.md).  
  
 Se viene utilizzato il provider dati di SqlClient 10 come provider per l'origine dei dati del modello, è necessario modificare anche la definizione dell'origine dati per specificare la versione precedente di SQL Server Native Client. In caso contrario, in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] viene generato un errore indicante che il provider non è registrato.  
  
##  <a name="deploying-models-with-holdout"></a><a name="bkmk_Holdout"></a>Distribuzione di modelli con i supporti  
 Se si utilizza [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] per creare una struttura di data mining che contiene una partizione di dati di controllo utilizzata per testare i modelli di data mining, è possibile distribuire la struttura di data mining in un'istanza di SQL Server 2005, ma le informazioni sulle partizioni andranno perse.  
  
 Quando si apre la struttura di data mining in SQL Server 2005 Analysis Services, in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] viene generato un errore e la struttura viene rigenerata per rimuovere la partizione di dati di controllo.  
  
 Dopo la ricompilazione della struttura, la dimensione della partizione di dati di dati non è più disponibile nella Finestra Proprietà; Tuttavia, il valore \<Ddl100_100: HoldoutMaxPercent>30\</ddl100_100: HoldoutMaxPercent>) potrebbe essere ancora presente nel file script ASSL.  
  
##  <a name="deploying-models-with-filters"></a><a name="bkmk_Filter"></a>Distribuzione di modelli con filtri  
 Se si utilizza [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] per applicare un filtro a un modello di data mining, è possibile distribuire il modello in un'istanza di SQL Server 2005, ma il filtro non verrà applicato.  
  
 Quando si apre il modello di data mining, in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] viene generato un errore e il modello viene rigenerato per rimuovere il filtro.  
  
##  <a name="restoring-from-database-backups"></a><a name="bkmk_Backup"></a> Ripristino dai backup del database  
 Non è possibile ripristinare in un'istanza di SQL Server 2005 un backup di database creato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . In caso contrario, in SQL Server Management Studio viene generato un errore.  
  
 Se si crea il backup di un database di SQL Server 2005 Analysis Services e lo si ripristina in un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], tutti i modelli Time Series vengono modificati come descritto nella sezione precedente.  
  
##  <a name="using-database-synchronization"></a><a name="bkmk_Synch"></a>Utilizzo della sincronizzazione del database  
 La sincronizzazione del database da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a SQL Server 2005 non è supportata.  
  
 Se si tenta di sincronizzare un database di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , il server restituisce un errore e la sincronizzazione del database non riesce.  
  
## <a name="see-also"></a>Vedi anche  
 [Analysis Services Backward Compatibility](../analysis-services-backward-compatibility.md)  
  
  
