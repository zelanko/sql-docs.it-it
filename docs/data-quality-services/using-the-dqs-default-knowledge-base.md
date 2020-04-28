---
title: Utilizzo della Knowledge Base predefinita di DQS
ms.custom: ''
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 2696a911edeefecc1dc34efeb77351acbaafc0d8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257740"
---
# <a name="using-the-dqs-default-knowledge-base"></a>Utilizzo della Knowledge Base predefinita di DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritta la Knowledge Base predefinita, **DQS Data**, installata con [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Si tratta di una Knowledge Base precompilata che contiene i domini seguenti:  
  
-   **Paese**: contiene i nomi lunghi (nome ufficiale designato dal paese) e brevi (nome comune usato in elenchi, mappe, ecc.), abbreviazione di due lettere, abbreviazione di tre lettere e codice di tre cifre per ogni posizione.  Il valore iniziale è impostato sul nome paese lungo.  
  
-   **Paese (tre lettere iniziali)**: contiene i nomi lunghi (nome ufficiale designato dal paese) e brevi (nome comune utilizzato in elenchi, su mappe e così via), abbreviazione di due lettere, abbreviazione di tre lettere e codice di tre cifre per ogni posizione.  Il valore iniziale è impostato sull'abbreviazione paese di tre lettere.  
  
-   **Paese (due lettere iniziali)**: contiene i nomi lunghi (nome ufficiale designato dal paese) e brevi (nome comune usato in elenchi, mappe, ecc.), abbreviazione di due lettere, abbreviazione di tre lettere e codice di tre cifre per ogni posizione.  Il valore iniziale è impostato sull'abbreviazione paese di due lettere.  
  
-   **US - Provincie**: contiene un elenco di provincie US.  
  
-   **US - Cognome**: contiene un elenco di cognomi che si verificano più di 100 volte in Census 2000.  
  
-   **US - Luoghi**: contiene un elenco di luoghi per i 50 stati, District of Columbia e Porto Rico estratti da Census 2010.  
  
-   **US - Stato**: contiene il nome lungo (ufficiale) convenzionale e l'abbreviazione di due lettere per ogni stato negli USA. Il valore iniziale è impostato sul nome stato convenzionale.  
  
-   **US - Stato (intestazione di 2 lettere)**: contiene il nome lungo (ufficiale) convenzionale e l'abbreviazione di due lettere per ogni stato negli USA. Il valore iniziale è impostato sull'abbreviazione di due lettere del nome dello stato.  
  
## <a name="using-the-default-knowledge-base"></a>Utilizzo della Knowledge Base predefinita  
 È possibile utilizzare la Knowledge Base DQS predefinita, i dati DQS, nei modi seguenti:  
  
-   Avviare rapidamente ed eseguire un progetto Data Quality per la pulizia dei dati utilizzando la Knowledge Base predefinita senza dover creare prima una nuova Knowledge Base in DQS.  
  
-   Eseguire le attività Gestione dominio, Individuazione informazioni o Criteri di corrispondenza sulla Knowledge Base predefinita. A tale scopo, fare clic su **Apri Knowledge Base** nella [Data Quality Client Home Screen](../data-quality-services/data-quality-client-home-screen.md), selezionare la Knowledge Base **Dati DQS** nella schermata **Apri Knowledge Base** , quindi selezionare l'attività richiesta nell'area **Seleziona attività** . Fare clic su **Avanti** per continuare.  
  
-   Creare una nuova Knowledge Base utilizzando una Knowledge Base predefinita. Per creare una Knowledge Base da una esistente, vedere [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md).  
  
-   Utilizzarla in [Componente Pulizia DQS in Integration Services](https://go.microsoft.com/fwlink/?LinkId=238830) e nel [componente aggiuntivo Master Data Services per Excel](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Knowledge Base e domini DQS](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
