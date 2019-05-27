---
title: Finestra di dialogo Proprietà set di dati, Query | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10160"
- sql12.rtp.rptdesigner.datasetproperties.query.f1
ms.assetid: 1fa34a4b-7de0-4e92-99fa-bc28a206773f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aead5d8e5c85b67333f10bee4e73e2bb1a8633ab
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109369"
---
# <a name="dataset-properties-dialog-box-query"></a>Finestra di dialogo Proprietà set di dati, Query
  Selezionare **Query** nel **proprietà set di dati** finestra di dialogo per scegliere un'origine dati e creare una query.  
  
 Nella finestra di dialogo **Proprietà set di dati** sono presenti le seguenti opzioni:  
  
-   [Finestra di dialogo Proprietà set di dati, Parametri](report-data/dataset-properties-dialog-box-parameters.md)  
  
-   [Finestra di dialogo Proprietà set di dati, Campi](../../2014/reporting-services/dataset-properties-dialog-box-fields.md)  
  
-   [Finestra di dialogo Proprietà set di dati, Opzioni](../../2014/reporting-services/dataset-properties-dialog-box-options.md)  
  
-   [Finestra di dialogo Proprietà set di dati, Filtri](report-data/dataset-properties-dialog-box-filters.md)  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Consente di digitare un nome per il set di dati. Non è possibile specificare un nome uguale a quello di un'area dati o di un gruppo nel report.  
  
 **Data Source**  
 Consente di selezionare l'origine dati su cui basare il set di dati. Per creare una nuova origine dati, fare clic su **Nuova**.  
  
 **Tipo di query**  
 Consente di selezionare il tipo di comando o query da utilizzare per il set di dati. Selezionare **Testo** per eseguire una query che consenta di recuperare dati dal database. Selezionare **Tabella** per usare la funzionalità **TableDirect** di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e selezionare tutti i campi all'interno di una tabella. Selezionare **Stored procedure** per eseguire una stored procedure in base al nome. **Testo** è selezionato per impostazione predefinita e viene usato per la maggior parte delle query. Per modificare la query sull'origine dati selezionata, fare clic su **Progettazione query**.  
  
> [!NOTE]  
>  Non tutti i tipi di query sono supportati da tutte le origini dati. Il tipo **Tabella** , ad esempio, è supportato solo dalle origini dati di tipo **OLE DB** e **ODBC**.  
  
 **Query**  
 Questa opzione viene visualizzata quando si sceglie l'opzione del tipo di comando **Testo** . Digitare una query o importare una query preesistente facendo clic su **Importa**. Fare clic sul pulsante **Espressione** (*fx*) per modificare l'espressione.  
  
> [!NOTE]  
>  Se è disponibile una query compilata in una finestra di progettazione query, il relativo testo verrà visualizzato in questa casella.  
  
 **Nome tabella**  
 Immettere il nome della tabella che si desidera utilizzare come set di dati. Questa opzione viene visualizzata quando si seleziona **Tabella**.  
  
 **Selezionare o immettere un nome di stored procedure**  
 Digitare o scegliere il nome della stored procedure che si desidera utilizzare. Fare clic sul pulsante **Espressione** (*fx*) per modificare l'espressione. Questa opzione viene visualizzata quando si sceglie l'opzione del tipo di comando Stored procedure.  
  
 **Timeout (in secondi)**  
 Consente di digitare il numero di secondi di attesa prima del timeout della query. Il valore predefinito è 30 secondi. Il valore nel campo **Timeout** deve essere vuoto o maggiore di zero. Se non si specifica alcun valore, non si verificherà mai il timeout della query.  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Finestre di progettazione query &#40;Generatore report&#41;](../../2014/reporting-services/query-designers-report-builder.md)   
 [Strumenti di progettazione query in Reporting Services](../../2014/reporting-services/reporting-services-query-designers.md)  
  
  
