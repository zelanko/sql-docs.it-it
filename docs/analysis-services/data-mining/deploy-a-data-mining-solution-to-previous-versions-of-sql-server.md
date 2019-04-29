---
title: Distribuire una soluzione di Data Mining in versioni precedenti di SQL Server | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df527197f0ddd1eacc2e86e59092f45b1ac78c9a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011021"
---
# <a name="deploy-a-data-mining-solution-to-previous-versions-of-sql-server"></a>Distribuire una soluzione di data mining in versioni precedenti di SQL Server
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In questa sezione vengono descritti i problemi di compatibilità noti che possono verificarsi quando si tenta di distribuire in un database che utilizza SQL Server 2005 Analysis Services una struttura o un modello di data mining creato in un'istanza di [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] oppure quando si distribuiscono in un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]modelli creati in SQL Server 2005.  
  
 La distribuzione in un'istanza di SQL Server 2000 Analysis Services non è supportata.  
  
 [Distribuzione di modelli Time Series](#bkmk_TimeSeries)  
  
 [Distribuzione di modelli con dati di controllo](#bkmk_Holdout)  
  
 [Distribuzione di modelli con filtri](#bkmk_Filter)  
  
 [Ripristino dai backup del database](#bkmk_Backup)  
  
 [Utilizzo della sincronizzazione del database](#bkmk_Synch)  
  
##  <a name="bkmk_TimeSeries"></a> Distribuzione di modelli Time Series  
 In SQL Server 2008 l'algoritmo Microsoft Time Series è stato migliorato mediante l'aggiunta di un secondo algoritmo complementare, ARIMA. Per altre informazioni sulle modifiche apportate all'algoritmo Time Series, vedere [Algoritmo Microsoft Time Series](../../analysis-services/data-mining/microsoft-time-series-algorithm.md).  
  
 I modelli di data mining Time Series che utilizzano il nuovo algoritmo ARIMA possono pertanto presentare un comportamento diverso quando vengono distribuiti in un'istanza di SQL Server 2005 Analysis Services.  
  
 Se è stato impostato in modo esplicito il parametro PREDICTION_SMOOTHING per controllare la combinazione della stima dei modelli ARTXP e ARIMA, quando il modello viene distribuito in un'istanza di SQL Server 2005, in Analysis Services viene generato un errore per segnalare che il parametro non è valido. Per evitare l'errore, è necessario eliminare il parametro PREDICTION_SMOOTHING e convertire i modelli in un modello esclusivamente ARTXP.  
  
 Viceversa, se si distribuisce in un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]un modello Time Series creato con SQL Server 2005 Analysis Services, quando si apre il modello di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], i file di definizione vengono prima convertiti nel nuovo formato e due nuovi parametri vengono aggiunti per impostazione predefinita a tutti i modelli Time Series. Il parametro FORECAST_METHOD viene aggiunto con valore predefinito MIXED e il parametro PREDICTION_SMOOTHING viene aggiunto con valore predefinito 0,5. Fino a quando non si rielabora il modello, tuttavia, il modello continua a utilizzare solo ARTXP per le previsioni. Non appena si rielabora il modello, la stima cambia per utilizzare sia ARIMA sia ARTXP.  
  
 Per evitare di modificare il modello, è pertanto necessario limitarsi a esplorare il modello senza mai elaborarlo. In alternativa, è possibile impostare in modo esplicito i parametri FORECAST_METHOD o PREDICTION_SMOOTHING.  
  
 Per informazioni dettagliate sulla configurazione dei modelli misti, vedere [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
 Se viene utilizzato il provider dati di SqlClient 10 come provider per l'origine dei dati del modello, è necessario modificare anche la definizione dell'origine dati per specificare la versione precedente di SQL Server Native Client. In caso contrario, in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] viene generato un errore indicante che il provider non è registrato.  
  
##  <a name="bkmk_Holdout"></a> Distribuzione di modelli con dati di controllo  
 Se si crea una struttura di data mining che contiene una partizione di controllo utilizzata per il testing di modelli di data mining, la struttura di data mining può essere distribuita a un'istanza di SQL Server 2005, ma le informazioni sulle partizioni andranno perse.  
  
 Quando si apre la struttura di data mining in SQL Server 2005 Analysis Services, in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] viene generato un errore e la struttura viene rigenerata per rimuovere la partizione di dati di controllo.  
  
 Dopo che la struttura è stata ricostruita, le dimensioni della partizione di controllo non sono più disponibile nella finestra Proprietà. Tuttavia, il valore \<ddl100_100:HoldoutMaxPercent > 30\</ddl100_100:HoldoutMaxPercent >) può essere ancora presente nel file di script ASSL.  
  
##  <a name="bkmk_Filter"></a> Distribuzione di modelli con filtri  
 Se si applica un filtro a un modello di data mining, è possibile distribuire il modello a un'istanza di SQL Server 2005, ma il filtro non verrà applicato.  
  
 Quando si apre il modello di data mining, in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] viene generato un errore e il modello viene rigenerato per rimuovere il filtro.  
  
##  <a name="bkmk_Backup"></a> Ripristino dai backup del database  
 Non è possibile ripristinare in un'istanza di SQL Server 2005 un backup di database creato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . In caso contrario, in SQL Server Management Studio viene generato un errore.  
  
 Se si crea il backup di un database di SQL Server 2005 Analysis Services e lo si ripristina in un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], tutti i modelli Time Series vengono modificati come descritto nella sezione precedente.  
  
##  <a name="bkmk_Synch"></a> Utilizzo della sincronizzazione del database  
 La sincronizzazione del database da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a SQL Server 2005 non è supportata.  
  
 Se si tenta di sincronizzare un database di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , il server restituisce un errore e la sincronizzazione del database non riesce.  
  
## <a name="see-also"></a>Vedere anche  
 [Analysis Services Backward Compatibility](../../analysis-services/analysis-services-backward-compatibility.md)  
  
  
