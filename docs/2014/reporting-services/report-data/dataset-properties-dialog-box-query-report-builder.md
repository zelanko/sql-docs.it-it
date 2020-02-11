---
title: Finestra di dialogo Proprietà set di dati, Query (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10024"
ms.assetid: 75432318-0b00-4797-917c-0a2e74f9d951
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1cde36fba94293e8f79660399cd4ee35158f671d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107352"
---
# <a name="dataset-properties-dialog-box-query-report-builder"></a>Finestra di dialogo Proprietà set di dati, Query (Generatore report)
  Selezionare **Query** nella finestra di dialogo **Proprietà set di dati** per scegliere un set di dati condiviso da un server di report o per creare un set di dati incorporato. Per un set di dati incorporato, è necessario scegliere un'origine dati e compilare una query.  
  
 Nella finestra di dialogo **Proprietà set di dati** sono presenti le seguenti opzioni:  
  
-   [Finestra di dialogo Proprietà set di dati, parametri &#40;Generatore report&#41;](../dataset-properties-dialog-box-parameters-report-builder.md)  
  
-   [Finestra di dialogo Proprietà set di dati, campi &#40;Generatore report&#41;](../dataset-properties-dialog-box-fields-report-builder.md)  
  
-   [Finestra di dialogo Proprietà set di dati, opzioni &#40;Generatore report&#41;](dataset-properties-dialog-box-options-report-builder.md)  
  
-   [Finestra di dialogo Proprietà set di dati, filtri &#40;Generatore report&#41;](../dataset-properties-dialog-box-filters-report-builder.md)  
  
 Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare un nome per il set di dati. Non è possibile specificare un nome uguale a quello di un'area dati o di un gruppo nel report.  
  
 **Usare un set di dati condiviso**  
 Selezionare questa opzione per utilizzare un set di dati predefinito dal server di report.  
  
 **Sfoglia**  
 Selezionare una cartella in un server di report o sito di SharePoint e scegliere un set di dati condiviso (estensione rsd).  
  
 **Usa un set di dati incorporato nel report**  
 Selezionare questa opzione per creare un set di dati da utilizzare solo per il report specifico.  
  
 **Origine dati**  
 Consente di selezionare l'origine dati su cui basare il set di dati. Per creare una nuova origine dati, fare clic su **Nuova**.  
  
 **Tipo di query**  
 Consente di selezionare il tipo di comando o query da utilizzare per il set di dati. Selezionare **Testo** per eseguire una query che consenta di recuperare dati dal database. Selezionare **Tabella** per usare la funzionalità **TableDirect** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e selezionare tutti i campi all'interno di una tabella. Selezionare **Stored procedure** per eseguire una stored procedure in base al nome. Il **testo** è selezionato per impostazione predefinita e viene utilizzato per la maggior parte delle query. Per modificare la query sull'origine dati selezionata, fare clic su **Progettazione query**.  
  
> [!NOTE]  
>  Non tutti i tipi di query sono supportati da tutte le origini dati. Il tipo **Tabella** , ad esempio, è supportato solo dalle origini dati di tipo **OLE DB** e **ODBC**.  
  
 **Query**  
 Questa opzione viene visualizzata quando si sceglie l'opzione del tipo di comando **Testo** . Digitare una query o importare una query preesistente facendo clic su **Importa**. Fare clic sul pulsante **espressione** (*FX*) per modificare l'espressione.  
  
> [!NOTE]  
>  Se è disponibile una query compilata in una finestra di progettazione query, il relativo testo verrà visualizzato in questa casella.  
  
 **Nome tabella**  
 Immettere il nome della tabella che si desidera utilizzare come set di dati. Questa opzione viene visualizzata quando si seleziona **Tabella**.  
  
 **Selezionare o immettere il nome del stored procedure**  
 Digitare o scegliere il nome della stored procedure che si desidera utilizzare. Fare clic sul pulsante **espressione** (*FX*) per modificare l'espressione. Questa opzione viene visualizzata quando si sceglie l'opzione del tipo di comando Stored procedure.  
  
 **Timeout (in secondi)**  
 Digitare il numero di secondi prima del timeout della query. Il valore predefinito è 30 secondi. Il valore nel campo **Timeout** deve essere vuoto o maggiore di zero. Se non si specifica alcun valore, non si verificherà mai il timeout della query.  
  
 **Aggiorna campi**  
 Eseguire il comando di query per aggiornare l'elenco di campi nella pagina [Finestra di dialogo Proprietà set di dati, Campi](../dataset-properties-dialog-box-fields-report-builder.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere dati a un report &#40;Generatore report e SSRS&#41;](report-datasets-ssrs.md)   
 [Guida Generatore report per finestre di dialogo, riquadri e procedure guidate](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Progettazione query &#40;Generatore report&#41;](../query-designers-report-builder.md)  
  
  
