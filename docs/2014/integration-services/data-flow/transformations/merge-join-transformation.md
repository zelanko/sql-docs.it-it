---
title: Trasformazione Merge join | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointrans.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e1a581536bb4f2a07dbbdf3d6ca187ac4a6f5250
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52767183"
---
# <a name="merge-join-transformation"></a>Merge join - trasformazione
  La trasformazione Merge join fornisce un output generato unendo in join due set di dati ordinati, tramite un join di tipo FULL, LEFT o INNER. È ad esempio possibile utilizzare un join di tipo LEFT per unire in join una tabella che include informazioni sui prodotti con una tabella in cui sono elencati i relativi paesi di produzione. Il risultato è costituito da una tabella in cui sono elencati tutti i prodotti e i relativi paesi di origine.  
  
 Per configurare la trasformazione Merge join, procedere nel modo seguente:  
  
-   Specificare se il join è di tipo FULL, LEFT o INNER.  
  
-   Specificare le colonne utilizzate dal join.  
  
-   Specificare se la trasformazione considera uguali tutti i valori Null.  
  
    > [!NOTE]  
    >  Se i valori Null non vengono considerati uguali, verranno gestiti come nel Motore di database di SQL Server.  
  
 Questa trasformazione include due input e un output. Non supporta un output degli errori.  
  
## <a name="input-requirements"></a>Requisiti relativi all'input  
 Per eseguire la trasformazione Merge join, è necessario che i relativi dati di input siano ordinati. Per altre informazioni su questo requisito importante, vedere [Ordinamento dei dati per le trasformazioni Unione e Merge Join](sort-data-for-the-merge-and-merge-join-transformations.md).  
  
## <a name="join-requirements"></a>Requisiti del join  
 Per eseguire la trasformazione Merge join è necessario che le colonne da unire in join abbiano metadati corrispondenti. Non è ad esempio possibile unire in join una colonna con tipo di dati numeric a una colonna con tipo di dati character. Se i dati sono di tipo string, la lunghezza della colonna nel secondo input dovrà essere minore o uguale a quella della colonna nel primo input, alla quale verrà unita.  
  
## <a name="buffer-throttling"></a>Limitazione delle richieste del buffer  
 Non è più necessario configurare il valore della proprietà `MaxBuffersPerInput`, in quanto Microsoft ha apportato modifiche che riducono il rischio di utilizzo di una quantità eccessiva di memoria da parte della trasformazione Merge join. Questo problema si verificava in genere quando tramite i diversi input della trasformazione Merge Join venivano prodotti dati con frequenze irregolari.  
  
## <a name="related-tasks"></a>Attività correlate  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per informazioni sull'impostazione delle proprietà di questa trasformazione, fare clic su uno degli argomenti seguenti:  
  
-   [Estensione di un set di dati tramite la trasformazione Merge join](merge-join-transformation.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordinamento dei dati per le trasformazioni Unione e Merge Join](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Editor trasformazione Merge join](../../merge-join-transformation-editor.md)   
 [Trasformazione Unione](merge-transformation.md)   
 [Trasformazione Unione input multipli](union-all-transformation.md)   
 [Trasformazioni di Integration Services](integration-services-transformations.md)  
  
  
