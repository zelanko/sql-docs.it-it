---
title: Destinazione di Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSDEST.F1
- SQL11.DTS.DESIGNER.AFPADLSDEST.F1
ms.assetid: d0e86032-2a6b-48b2-898f-e94328474fde
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f10f78f59a6ec1dd5d5119a89624295935d6ff9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771897"
---
# <a name="azure-data-lake-store-destination"></a>Destinazione di Azure Data Lake Store
  Il componente **Destinazione di Azure Data Lake Store** consente a un pacchetto SSIS di scrivere dati in Azure Data Lake Store. I formati di file supportati sono: Testo, Avro e ORC. 
  
## <a name="configure-the-azure-data-lake-store-destination"></a>Configurare Destinazione di Azure Data Lake Store 

1. Trascinare **Destinazione di Azure Data Lake Store** nella finestra di progettazione del flusso di dati e fare doppio clic per visualizzare l'editor.  

2.  Nel campo **Gestione connessioni di Azure Data Lake Store** specificare un'istanza esistente di Gestione connessioni di Azure Data Lake Store o creare una nuova istanza che faccia riferimento a un servizio di Azure Data Lake Store.  
  
    1.  Per il campo **Percorso file** specificare il nome del file in cui si vogliono scrivere i dati. Se il file esiste già, il suo contenuto verrà sovrascritto.  
  
    2.  Per il campo **Formato file** specificare il formato file che si vuole usare.  
  
        Se il formato del file corrisponde a testo, è necessario impostare il valore **Carattere delimitatore di colonna** . Selezionare anche **Nomi di colonne nella prima riga di dati** se la prima riga nel file contiene i nomi di colonna.  

        Se il formato del file corrisponde a ORC, è necessario installare JRE per la piattaforma corrispondente. 
  
3.  Dopo aver specificato le informazioni di connessione, passare alla pagina **Colonne** per eseguire il mapping delle colonne di origine alle colonne di destinazione per il flusso di dati SSIS.  
