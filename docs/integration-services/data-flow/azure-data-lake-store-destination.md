---
title: Destinazione di Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSDEST.F1
- sql14.dts.designer.afpadlsdest.f1
ms.assetid: 4c4f504f-dd2b-42c5-8a20-1a8ad9a5d632
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ebd3d19d42a39b92458d418d6ba13486f9c14e96
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922771"
---
# <a name="azure-data-lake-store-destination"></a>Destinazione di Azure Data Lake Store

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Il componente **Destinazione di Azure Data Lake Store** consente a un pacchetto SSIS di scrivere dati in Azure Data Lake Store. I formati di file supportati sono: Testo, Avro e ORC. 
  
 **Destinazione di Azure Data Lake Store** è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
 
> [!NOTE]
> Per assicurarsi che la Gestione connessioni di Azure Data Lake Store e che i componenti che la usano, cioè l'origine e la destinazione di Azure Data Lake Store, possano connettersi ai servizi, scaricare la versione del Feature Pack di Azure più recente da [qui](https://www.microsoft.com/download/details.aspx?id=49492). 

**Configurare Destinazione di Azure Data Lake Storage**

1. Trascinare **Destinazione di Azure Data Lake Store** nella finestra di progettazione del flusso di dati e fare doppio clic per visualizzare l'editor.  

2.  Nel campo **Gestione connessioni di Azure Data Lake Store** specificare un'istanza esistente di Gestione connessioni di Azure Data Lake Store o creare una nuova istanza che faccia riferimento a un servizio di Azure Data Lake Store.  
  
    1.  Per il campo **Percorso file** specificare il nome del file in cui si vogliono scrivere i dati. Se il file esiste già, il relativo contenuto viene sovrascritto.  
  
    2.  Per il campo **Formato file** specificare il formato file che si vuole usare.  
  
       Se il formato del file corrisponde a testo, è necessario impostare il valore **Carattere delimitatore di colonna** . Selezionare anche **Nomi di colonne nella prima riga di dati** se la prima riga nel file contiene i nomi di colonna.  

       Se il formato di file è ORC, è necessario Java. Per informazioni dettagliate, vedere [qui](../../integration-services/azure-feature-pack-for-integration-services-ssis.md#dependency-on-java).
  
3.  Dopo aver specificato le informazioni di connessione, passare alla pagina **Colonne** per eseguire il mapping delle colonne di origine alle colonne di destinazione per il flusso di dati SSIS.  
