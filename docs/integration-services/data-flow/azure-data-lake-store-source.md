---
title: Origine di Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSSRC.F1
- sql14.dts.designer.afpadlssrc.f1
ms.assetid: f9c3311f-7316-48d6-bf10-d810e70b4304
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2699b5d76f15ea81875256cddcd63af1b6451f04
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71293382"
---
# <a name="azure-data-lake-store-source"></a>Origine di Azure Data Lake Store

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Il componente **Origine di Azure Data Lake Store** consente a un pacchetto SSIS di leggere dati da Azure Data Lake Store. I formati di file supportati sono: testo e AVRO.
  
 **Origine di Azure Data Lake Store** è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
> [!NOTE]
> Per assicurarsi che la Gestione connessioni di Azure Data Lake Store e che i componenti che la usano, cioè l'origine e la destinazione di Azure Data Lake Store, possano connettersi ai servizi, scaricare la versione del Feature Pack di Azure più recente da [qui](https://www.microsoft.com/download/details.aspx?id=49492). 
  
## <a name="configure-the-azure-data-lake-store-source"></a>Configurare Origine di Azure Data Lake Store
 1. Per visualizzare l'editor per Origine di Azure Data Lake Store, trascinare la selezione **Origine di Azure Data Lake Store** nell'area di progettazione del flusso di dati e fare doppio clic per aprire l'editor.  
  
2.  Nel campo **Gestione connessioni di Azure Data Lake Store** specificare un'istanza esistente di Gestione connessioni di Azure Data Lake Store o creare una nuova istanza che faccia riferimento a un servizio di Azure Data Lake Store.  
  
    1.  Per il campo **Percorso File** , specificare il percorso del file di origine in Azure Data Lake Store.   
  
    2.  Per il campo **Formato file** specificare il formato file che si vuole usare.  
  
        Se il formato del file corrisponde a testo, è necessario impostare il valore **Carattere delimitatore di colonna** . Selezionare anche **Nomi di colonne nella prima riga di dati** se la prima riga nel file contiene i nomi di colonna.  
  
3.  Dopo aver specificato le informazioni di connessione, passare alla pagina **Colonne** per eseguire il mapping delle colonne di origine alle colonne di destinazione per il flusso di dati SSIS.   

## <a name="text-qualifier"></a>Qualificatore di testo

L'**origine Azure Data Lake Store** non supporta un qualificatore di testo. Se è necessario specificare un qualificatore di testo per elaborare i file in modo corretto, valutare la possibilità di scaricare i file nel computer locale ed elaborare i file con l'**origine file flat**. L'origine file flat consente di specificare un qualificatore di testo. Per altre informazioni, vedere [Origine file flat](flat-file-source.md).
