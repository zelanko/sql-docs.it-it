---
description: Definizione dei dati MDX - CREATE KPI
title: Istruzione CREATE KPI (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d1840ebe0dec014a2b768a8571249b103de6552d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494854"
---
# <a name="mdx-data-definition---create-kpi"></a>Definizione dei dati MDX - CREATE KPI


  Crea un indicatore di prestazioni chiave (KPI). Un indicatore KPI è costituito da una raccolta di calcoli associati a un gruppo di misure in un cubo e utilizzati per valutare il successo aziendale o dello scenario.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CREATE KPI CURRENTCUBE | <Cube Name>.KPI_Name AS KPI_Value  
   [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>Argomenti  
 *KPI_Name*  
 Stringa valida che specifica un nome di indicatore KPI.  
  
 *KPI_Value*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un valore numerico.  
  
 *Property_Name*  
 Stringa valida che fornisce il nome di una proprietà di indicatore KPI.  
  
 *Property_Value*  
 Espressione scalare valida che definisce il valore della proprietà dell'indicatore KPI.  
  
## <a name="remarks"></a>Osservazioni  
 Specificando un cubo diverso dal cubo connesso viene generato un errore. Pertanto, per identificare il cubo corrente è consigliabile usare CURRENTCUBE anziché il nome di un cubo.  
  
## <a name="kpi-properties"></a>Proprietà indicatore KPI  
 Nella seguente tabella vengono descritte tutte le proprietà dell'indicatore di prestazioni chiave(KPI). Nessuna di queste proprietà ha un valore predefinito. Pertanto, se non viene assegnato un valore specifico alla proprietà dell'indicatore KPI, le query relative alle proprietà restituiranno un valore null.  
  
|Identificatore proprietà|Significato|  
|-------------------------|-------------|  
|GOAL|Espressione MDX valida che restituisce un valore numerico.|  
|STATO|Espressione MDX valida che restituisce un valore numerico.|  
|STATUS_GRAPHIC|Stringa che definisce un set di immagini grafiche che sarà utilizzato dall'applicazione client.|  
|TREND|Espressione MDX valida che restituisce un valore numerico.|  
|TREND_GRAPHIC|Stringa che definisce un set di immagini grafiche che sarà utilizzato dall'applicazione client.|  
|WEIGHT|Espressione MDX valida che restituisce un valore numerico.|  
|CURRENT_TIME_MEMBER|Espressione MDX valida che restituisce un membro nella dimensione temporale. CURRENT_TIME_MEMBER imposta il punto di riferimento per tutte le funzioni relative all'ora.|  
|PARENT_KPI|Stringa che specifica il nome dell'indicatore KPI padre.|  
|CAPTION|Stringa utilizzata dall'applicazione client come didascalia per l'indicatore di prestazioni chiave KPI.|  
|DISPLAY_FOLDER|Stringa che specifica il percorso della cartella di visualizzazione in cui l'indicatore KPI deve essere mostrato dall'applicazione client. Il separatore di livello delle cartelle è definito dall'applicazione client. Per gli strumenti e i client forniti da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , la barra rovesciata ( \\ ) è il separatore di livello. Per fornire più cartelle di visualizzazione per un membro definito, utilizzare un punto e virgola (;) per separare le cartelle|  
|ASSOCIATED_MEASURE_GROUP|Stringa che specifica il nome del gruppo di misure al quale tutti i calcoli di MDX devono fare riferimento.|  
  
 I valori per le proprietà GOAL, STATUS e TREND sono espressioni MDX che devono rientrare tra -1 e 1. Tuttavia, è l'applicazione client che definisce l'intervallo dei valori effettivo per queste proprietà. Quando si utilizzano gli strumenti e i client forniti da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per esplorare gli indicatori KPI, i valori minori di-1 vengono considerati come-1 e i valori maggiori di 1 vengono considerati come 1.  
  
 STATUS_GRAPHIC e TREND_GRAPHIC sono valori stringa utilizzati dall'applicazione client per identificare il set corretto di immagini da visualizzare. Queste stringhe definiscono anche il comportamento della funzione di visualizzazione. Questo comportamento include il numero di stati da visualizzare (in genere, si tratta di un numero dispari) e le immagini da utilizzare per ognuno di questi stati.  
  
### <a name="kpi-graphics-in-sql-server-data-tools"></a>Simboli dell'indicatore KPI in SQL Server Data Tools  
 In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], i simboli dell'indicatore KPI possono avere tre o cinque stati. Nella tabella seguente sono definiti i valori per ciascuno di questi stati.  
  
|Numero di stati per simbolo di indicatore di prestazioni (KPI)|Valore di questi stati|  
|--------------------------------------|---------------------------|  
|3|Errato = da 1 a 0,5<br /><br /> OK = da 0,4999 a 0,4999<br /><br /> Buono = da 0,50 a 1|  
|5|Negativo = da -1 a -0,75<br /><br /> A rischio = da -0,7499 a -0,25<br /><br /> OK = da 0,2499 a 0,2499<br /><br /> In aumento = da 0,25 a 0,7499<br /><br /> Buono = da 0,75 a 1|  
  
> [!NOTE]  
>  Per alcuni simboli, ad esempio il misuratore capovolto o la freccia di stato capovolta, l'intervallo è invertito. Cioè, -1 è buono e 1 è errato.  
  
 In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], il nome del simbolo dell'indicatore KPI determina se il simbolo ha tre o cinque stati. Nella tabella seguente sono elencati l'utilizzo, il nome e il numero di stati [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] associati alla grafica degli indicatori KPI.  
  
|Utilizzo del simbolo|Nome del simbolo dell'indicatore KPI|Numero di stati|  
|--------------------|-------------------------|----------------------|  
|Stato|Forme|3|  
|Stato|Semaforo|3|  
|Stato|Segnali stradali|3|  
|Stato|Misuratore|3|  
|Stato|Misuratore capovolto|5|  
|Stato|Termometro|3|  
|Stato|Cilindro|3|  
|Stato|Smile|3|  
|Stato|Freccia di varianza|3|  
|Tendenza|Freccia standard|3|  
|Tendenza|Freccia di stato|3|  
|Tendenza|Freccia di stato capovolta|5|  
|Tendenza|Smile|3|  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione DROP KPI &#40;&#41;MDX ](../mdx/mdx-data-definition-drop-kpi.md)   
 [Istruzioni MDX per la definizione dei dati &#40;&#41;MDX ](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
