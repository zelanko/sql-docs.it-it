---
title: Trasformazione Merge join | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.mergejointrans.f1
- sql13.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 785f7f0af9a41052a870edc8feaf566585a45e89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725966"
---
# <a name="merge-join-transformation"></a>Merge join - trasformazione

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La trasformazione Merge join fornisce un output generato unendo in join due set di dati ordinati, tramite un join di tipo FULL, LEFT o INNER. È ad esempio possibile utilizzare un join di tipo LEFT per unire in join una tabella che include informazioni sui prodotti con una tabella in cui sono elencati i relativi paesi di produzione. Il risultato è costituito da una tabella in cui sono elencati tutti i prodotti e i relativi paesi di origine.  
  
 Per configurare la trasformazione Merge join, procedere nel modo seguente:  
  
-   Specificare se il join è di tipo FULL, LEFT o INNER.  
  
-   Specificare le colonne utilizzate dal join.  
  
-   Specificare se la trasformazione considera uguali tutti i valori Null.  
  
    > [!NOTE]  
    >  Se i valori Null non vengono considerati uguali, verranno gestiti come nel Motore di database di SQL Server.  
  
 Questa trasformazione include due input e un output. Non supporta un output degli errori.  
  
## <a name="input-requirements"></a>Requisiti relativi all'input  
 Per eseguire la trasformazione Merge join, è necessario che i relativi dati di input siano ordinati. Per altre informazioni su questo requisito importante, vedere [Ordinamento dei dati per le trasformazioni Unione e Merge Join](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
## <a name="join-requirements"></a>Requisiti del join  
 Per eseguire la trasformazione Merge join è necessario che le colonne da unire in join abbiano metadati corrispondenti. Non è ad esempio possibile unire in join una colonna con tipo di dati numeric a una colonna con tipo di dati character. Se i dati sono di tipo string, la lunghezza della colonna nel secondo input dovrà essere minore o uguale a quella della colonna nel primo input, alla quale verrà unita.  
  
## <a name="buffer-throttling"></a>Limitazione delle richieste del buffer  
 Non è più necessario configurare il valore della proprietà **MaxBuffersPerInput** , in quanto Microsoft ha apportato modifiche che riducono il rischio di utilizzo di una quantità eccessiva di memoria da parte della trasformazione Merge join. Questo problema si verificava in genere quando tramite i diversi input della trasformazione Merge Join venivano prodotti dati con frequenze irregolari.  
  
## <a name="related-tasks"></a>Attività correlate  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per informazioni sull'impostazione delle proprietà di questa trasformazione, fare clic su uno degli argomenti seguenti:  
  
-   [Estensione di un set di dati tramite la trasformazione Merge join](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordinare i dati per le trasformazioni Unione e Merge Join](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-join-transformation-editor"></a>Editor trasformazione Merge join
  Utilizzare la finestra di dialogo **Editor trasformazione Merge join** per specificare il tipo di join, le colonne di join e le colonne di output per l'unione di due input combinati tramite un join.  
  
> [!IMPORTANT]  
>  Per eseguire la trasformazione Merge join, è necessario che i relativi dati di input siano ordinati. Per altre informazioni su questo requisito importante, vedere [Ordinamento dei dati per le trasformazioni Unione e Merge Join](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### <a name="options"></a>Opzioni  
 **Tipo di join**  
 Consente di specificare se utilizzare un inner join, un outer join sinistro o un full join.  
  
 **Inverti ordine input**  
 Il pulsante **Inverti ordine input** consente di invertire l'ordine degli input. Questa selezione può risultare utile in caso si scelga di utilizzare un outer join sinistro.  
  
 **Input**  
 Per ogni colonna che si desidera includere nell'output unito, è innanzitutto necessario procedere a una selezione nell'elenco degli input disponibili.  
  
 Gli input vengono visualizzati in due tabelle separate. Selezionare le colonne da includere nell'output. Trascinare le colonne per creare un join tra le tabelle. Per eliminare un join, selezionarlo e quindi premere CANC.  
  
 **Colonna di input**  
 Selezionare una colonna da includere nell'output unito dall'elenco delle colonne disponibili nell'input selezionato.  
  
 **Alias di output**  
 Consente di digitare un alias per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna di input. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Unione](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Trasformazione Unione input multipli](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
