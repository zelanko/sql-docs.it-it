---
title: Origine di Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSSRC.F1
- SQL11.DTS.DESIGNER.AFPADLSSRC.F1
ms.assetid: 7d9e8457-62aa-4aea-98ee-7d1121dfae4f
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: 07ca2a75fa3f7e6329443bb4f71a23f52662f0f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061344"
---
# <a name="azure-data-lake-store-source"></a>Origine di Azure Data Lake Store
  Il componente **Origine di Azure Data Lake Store** consente a un pacchetto SSIS di leggere dati da Azure Data Lake Store. I formati di file supportati sono: testo e AVRO.
  
## <a name="configure-the-azure-data-lake-store-source"></a>Configurare Origine di Azure Data Lake Store 
  
1.  Per visualizzare l'editor per Origine di Azure Data Lake Store, trascinare la selezione **Origine di Azure Data Lake Store** nell'area di progettazione del flusso di dati e fare doppio clic per aprire l'editor.  
  
2.  Nel campo **Gestione connessioni di Azure Data Lake Store** specificare un'istanza esistente di Gestione connessioni di Azure Data Lake Store o creare una nuova istanza che faccia riferimento a un servizio di Azure Data Lake Store.  
  
    1.  Per il campo **Percorso File** , specificare il percorso del file di origine in Azure Data Lake Store.   
  
    2.  Per il campo **Formato file** specificare il formato file che si vuole usare.  
  
        Se il formato del file è testo, è necessario specificare il valore del **carattere delimitatore di colonna** . Selezionare anche **nomi di colonna nella prima riga di dati** se la prima riga nel file contiene i nomi di colonna.  
  
3.  Dopo aver specificato le informazioni di connessione, passare alla pagina **Colonne** per eseguire il mapping delle colonne di origine alle colonne di destinazione per il flusso di dati SSIS.  
