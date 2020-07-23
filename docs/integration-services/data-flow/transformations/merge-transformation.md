---
title: Trasformazione Unione | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.mergetrans.f1
- sql13.dts.designer.mergetransformation.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- merging data [Integration Services]
- Merge transformation
- combining datasets
- datasets [Integration Services], merging
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a444abac97c69755e234e39a9c6e3ae623af8d89
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919585"
---
# <a name="merge-transformation"></a>Unione - trasformazione

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  La trasformazione Unione consente di combinare due set di dati ordinati in un singolo set di dati. Le righe di ogni set di dati vengono inserite nell'output in base ai valori delle relative colonne chiave.  
  
 Includendo la trasformazione Unione in un flusso di dati, è possibile eseguire le attività seguenti:  
  
-   Unire dati da due origini dei dati, ad esempio tabelle e file.  
  
-   Creare set di dati complessi, nidificando più trasformazioni Unione.  
  
-   Unire di nuovo le righe dopo aver corretto gli errori nei dati.  
  
 La trasformazione Unione è simile alle trasformazioni Unione input multipli. Utilizzare la trasformazione Unione input multipli anziché la trasformazione Unione nelle situazioni seguenti:  
  
-   Gli input della trasformazione non sono ordinati.  
  
-   Non è necessario che l'output combinato sia ordinato.  
  
-   La trasformazione include più di due input.  
  
## <a name="input-requirements"></a>Requisiti relativi all'input  
 Per eseguire la trasformazione Unione, è necessario che i relativi dati di input siano ordinati. Per altre informazioni su questo requisito importante, vedere [Ordinamento dei dati per le trasformazioni Unione e Merge Join](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 La trasformazione Unione richiede inoltre che le colonne da unire nei relativi input abbiano metadati corrispondenti. Non è ad esempio possibile unire una colonna con tipo di dati numeric a una colonna con tipo di dati character. Se i dati sono di tipo string, la lunghezza della colonna nel secondo input dovrà essere minore o uguale a quella della colonna nel primo input, alla quale verrà unita.  
  
 In Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] l'interfaccia utente della trasformazione Unione mappa automaticamente le colonne con gli stessi metadati. È quindi possibile eseguire il mapping manualmente altre colonne con tipi di dati compatibili.  
  
 Questa trasformazione include due input e un output. Non supporta un output degli errori.  
  
## <a name="configuration-of-the-merge-transformation"></a>Configurazione della trasformazione Unione  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni dettagliate sull'impostazione delle proprietà, vedere i seguenti argomenti:  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordinare i dati per le trasformazioni Unione e Merge Join](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-transformation-editor"></a>Editor trasformazione Unione
  L' **Editor trasformazione Unione** consente di specificare le colonne di due set di dati ordinati di cui eseguire l'unione.  
  
> [!IMPORTANT]  
>  Per eseguire la trasformazione Unione, è necessario che i relativi dati di input siano ordinati. Per altre informazioni su questo requisito importante, vedere [Ordinamento dei dati per le trasformazioni Unione e Merge Join](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### <a name="options"></a>Opzioni  
 **Nome colonna di output**  
 Consente di specificare il nome della colonna di output.  
  
 **Input unione 1**  
 Consente di selezionare la colonna da unire come Input unione 1.  
  
 **Input unione 2**  
 Consente di selezionare la colonna da unire come Input unione 2.  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Merge join](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Trasformazione Unione input multipli](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
