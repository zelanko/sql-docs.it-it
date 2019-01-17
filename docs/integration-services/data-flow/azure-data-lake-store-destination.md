---
title: Destinazione di Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSDEST.F1
- sql14.dts.designer.afpadlsdest.f1
ms.assetid: 4c4f504f-dd2b-42c5-8a20-1a8ad9a5d632
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 87991a1f0fe12cfcc10df7e7bc3c542075bd050d
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215700"
---
# <a name="azure-data-lake-store-destination"></a>Destinazione di Azure Data Lake Store
  Il componente **Destinazione di Azure Data Lake Store** consente a un pacchetto SSIS di scrivere dati in Azure Data Lake Store. I formati di file supportati sono: Testo, Avro e ORC. 
  
 **Destinazione di Azure Data Lake Store** è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
 
> [!NOTE]
> Per assicurarsi che la Gestione connessioni di Azure Data Lake Store e che i componenti che la usano, cioè l'origine e la destinazione di Azure Data Lake Store, possano connettersi ai servizi, scaricare la versione del Feature Pack di Azure più recente da [qui](https://www.microsoft.com/download/details.aspx?id=49492). 

## <a name="configure-the-azure-data-lake-store-destination"></a>Configurare Destinazione di Azure Data Lake Store  
1. Trascinare **Destinazione di Azure Data Lake Store** nella finestra di progettazione del flusso di dati e fare doppio clic per visualizzare l'editor.  

2.  Nel campo **Gestione connessioni di Azure Data Lake Store** specificare un'istanza esistente di Gestione connessioni di Azure Data Lake Store o creare una nuova istanza che faccia riferimento a un servizio di Azure Data Lake Store.  
  
    1.  Per il campo **Percorso file** specificare il nome del file in cui si vogliono scrivere i dati. Se il file esiste già, il suo contenuto verrà sovrascritto.  
  
    2.  Per il campo **Formato file** specificare il formato file che si vuole usare.  
  
        Se il formato del file corrisponde a testo, è necessario impostare il valore **Carattere delimitatore di colonna** . Selezionare anche **Nomi di colonne nella prima riga di dati** se la prima riga nel file contiene i nomi di colonna.  

        Se il formato del file corrisponde a ORC, è necessario installare JRE per la piattaforma corrispondente. 
  
3.  Dopo aver specificato le informazioni di connessione, passare alla pagina **Colonne** per eseguire il mapping delle colonne di origine alle colonne di destinazione per il flusso di dati SSIS.  
  
  
