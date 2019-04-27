---
title: Configurare dimensioni massime caricamento File (PowerPivot per SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ac516c63-1e79-4ae8-bca6-32d3c1a09c00
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96e4cf621a1c0f7f701012ed479797fc450d1533
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743269"
---
# <a name="configure-maximum-file-upload-size-powerpivot-for-sharepoint"></a>Configurare le dimensioni massime di caricamento dei file (PowerPivot per SharePoint)
  Nelle cartelle di lavoro di PowerPivot sono spesso contenute grandi quantità di dati che comportano il superamento delle dimensioni massime del file consentite per i caricamenti di SharePoint. Quando si tenta di caricare un file che supera il limite massimo, verrà visualizzato l'errore seguente in SharePoint:  
  
-   "Le dimensioni del file specificato superano le dimensioni massime supportate".  
  
 Per aumentare le dimensioni del file, iniziare impostando l'opzione Dimensioni massime cartella di lavoro per Excel Services su 50 megabyte. In questo modo, i limiti delle dimensioni massime del file per Excel vengono allineati a quelli delle applicazioni Web di SharePoint (impostati su 50 megabyte in SharePoint 2010 e su 200 in SharePoint 2013 per impostazione predefinita). Se le dimensioni del file superano i 50 megabyte, aumentare i limiti delle dimensioni del file sia per Excel Services sia per l'applicazione Web.  
  
 Per modificare le dimensioni massime di caricamento del file è necessario essere un amministratore di SharePoint.  
  
### <a name="configure-maximum-file-size-for-excel-services"></a>Configurare le dimensioni massime del file per Excel Services  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sul nome dell'applicazione Excel Services.  
  
3.  Fare clic su **Percorsi attendibili file**.  
  
4.  Fare clic sulla posizione per modificare le proprietà. Per impostazione predefinita, in Excel Services l'applicazione Web predefinita viene considerata sito attendibile. Se si usa l'applicazione Web predefinita, fare clic su **http://** per aprire la pagina di configurazione per questo percorso.  
  
5.  Scorrere fino a **Proprietà cartella di lavoro**.  
  
6.  In Dimensioni massime cartella di lavoro aumentare le dimensioni del file da 10 (valore predefinito) a 50 o a una dimensione maggiore, appropriata ai file in uso.  
  
     Per impostazione predefinita, 50 megabyte rappresenta la dimensione di caricamento file massima per le applicazioni Web di SharePoint. Se l'opzione Dimensioni massime cartella di lavoro viene impostata su un valore maggiore di 50 megabyte, seguire i passaggi nella procedura descritta di seguito per aumentare Dimensioni massime caricamento per l'applicazione Web di SharePoint allo stesso valore.  
  
     Il valore massimo che è possibile specificare è 2 gigabyte (o 2047 megabyte come specificato in Amministrazione centrale).  
  
7.  Fare clic su **OK**.  
  
### <a name="configure-maximum-file-size-for-a-sharepoint-web-application"></a>Configurare le dimensioni massime del file per un'applicazione Web di SharePoint  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni Web**.  
  
    > [!NOTE]  
    >  Effettuare i passaggi seguenti solo se è stato aumentato il valore dell'opzione Dimensioni massime cartella di lavoro in Excel Services.  
  
2.  Selezionare l'applicazione, ad esempio **SharePoint - 80**.  
  
3.  Sulla barra multifunzione delle applicazioni Web, fare clic sulla freccia GIÙ sul pulsante Impostazioni generali.  
  
4.  Fare clic su **Impostazioni generali**.  
  
5.  Scorrere fino a **Dimensioni massime caricamento**.  
  
6.  Impostare la proprietà sul numero uguale o maggiore di quello impostato in Dimensioni massime cartella di lavoro in Excel Services.  
  
7.  Fare clic su **OK**.  
  
  
