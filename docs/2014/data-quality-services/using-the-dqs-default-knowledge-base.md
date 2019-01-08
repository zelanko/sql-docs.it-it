---
title: Uso della Knowledge Base predefinita di DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae4688108f7e0d2bf045581b7afe50235c7ff012
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368265"
---
# <a name="using-the-dqs-default-knowledge-base"></a>Utilizzo della Knowledge Base predefinita di DQS
  In questo argomento viene descritta la Knowledge Base predefinita, **DQS Data**, installata con [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Si tratta di una Knowledge Base precompilata che contiene i domini seguenti:  
  
-   **Paese/area geografica**: Contiene i lunghi (nome ufficiale designato dal paese) e nomi brevi (nome comune usato in elenchi, mappe e così via), abbreviazione di due lettere, abbreviazione di tre lettere e codice di tre cifre per ogni posizione.  Il valore iniziale è impostato sul nome paese lungo.  
  
-   **Paese (tre lettere iniziali)**: Contiene i lunghi (nome ufficiale designato dal paese) e nomi brevi (nome comune usato in elenchi, mappe e così via), abbreviazione di due lettere, abbreviazione di tre lettere e codice di tre cifre per ogni posizione.  Il valore iniziale è impostato sull'abbreviazione paese di tre lettere.  
  
-   **Paese/area geografica (due lettere iniziali)**: Contiene i lunghi (nome ufficiale designato dal paese) e nomi brevi (nome comune usato in elenchi, mappe e così via), abbreviazione di due lettere, abbreviazione di tre lettere e codice di tre cifre per ogni posizione.  Il valore iniziale è impostato sull'abbreviazione paese di due lettere.  
  
-   **US - provincie**: Contiene un elenco di provincie US.  
  
-   **US - cognome**: Contiene un elenco dei cognomi (cognomi) che si verificano 100 o più volte in Census 2000.  
  
-   **US - luoghi**: Contiene un elenco di luoghi per i 50 stati, District of Columbia e Porto Rico estratti da Census 2010.  
  
-   **US - stato**: Contiene il lungo (ufficiale) convenzionale nome e l'abbreviazione di due lettere per ogni stato negli Stati Uniti. Il valore iniziale è impostato sul nome stato convenzionale.  
  
-   **US - stato (intestazione di 2 lettere)**: Contiene il lungo (ufficiale) convenzionale nome e l'abbreviazione di due lettere per ogni stato negli Stati Uniti. Il valore iniziale è impostato sull'abbreviazione di due lettere del nome dello stato.  
  
## <a name="using-the-default-knowledge-base"></a>Utilizzo della Knowledge Base predefinita  
 È possibile utilizzare la Knowledge Base DQS predefinita, i dati DQS, nei modi seguenti:  
  
-   Avviare rapidamente ed eseguire un progetto Data Quality per la pulizia dei dati utilizzando la Knowledge Base predefinita senza dover creare prima una nuova Knowledge Base in DQS.  
  
-   Eseguire le attività Gestione dominio, Individuazione informazioni o Criteri di corrispondenza sulla Knowledge Base predefinita. A tale scopo, fare clic su **Apri Knowledge Base** nella [Data Quality Client Home Screen](../../2014/data-quality-services/data-quality-client-home-screen.md), selezionare la Knowledge Base **Dati DQS** nella schermata **Apri Knowledge Base** , quindi selezionare l'attività richiesta nell'area **Seleziona attività** . Fare clic su **Avanti** per continuare.  
  
-   Creare una nuova Knowledge Base utilizzando una Knowledge Base predefinita. Per creare una Knowledge Base da una esistente, vedere [Create a Knowledge Base](../../2014/data-quality-services/create-a-knowledge-base.md).  
  
-   Utilizzarla in [Componente Pulizia DQS in Integration Services](https://go.microsoft.com/fwlink/?LinkId=238830) e nel [componente aggiuntivo Master Data Services per Excel](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Knowledge Base e domini DQS](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
