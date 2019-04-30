---
title: Cercare parti del report e impostare una cartella predefinita (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5cf38068-65d1-4fe8-81f3-a404d8fbc663
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ae8fddf7e008c1c97c30c18deb2d8aec60b77415
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185747"
---
# <a name="browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs"></a>Ricerca di parti del report e impostazione di una cartella predefinita (Generatore report e SSRS)
  Il modo più semplice per creare un report consiste nell'aggiungere parti del report esistenti, ad esempio tabelle e grafici, al report in uso dalla raccolta di parti del report. Quando una parte di report viene aggiunta al report in uso, vengono aggiunti anche tutti gli elementi necessari affinché funzioni. Ad esempio, qualsiasi parte di report che consenta la visualizzazione dei dati dipende da un set di dati, ovvero una query e una connessione a un'origine dati. Dopo aver aggiunto la parte di report al report in uso, è possibile modificarla in base alle necessità.  
  
 È possibile impostare una cartella predefinita per la pubblicazione di parti di report sul server di report o su un sito di SharePoint integrato con un server di report.  
  
 Per altre informazioni, vedere [Parti del report &#40;Generatore report e SSRS&#41;](../report-parts-report-builder-and-ssrs.md).  
  
### <a name="to-browse-for-report-parts"></a>Per cercare parti di report  
  
1.  Scegliere **Parti del report** dal menu **Inserisci**.  
  
     Se non si è già connessi, fare clic su **Connessione a un server di report**e immettere il nome.  
  
    > [!NOTE]  
    >  È necessario essere connessi a un server di report per cercare le parti di report.  
  
2.  La ricerca può essere ristretta specificando dettagli relativi alla parte di report. Digitare il nome e la descrizione per intero o in parte nella casella **Cerca** o fare clic su **Aggiungi criteri** e aggiungere i valori per tutti o alcuni di questi campi:  
  
    -   Creato da  
  
    -   Data creazione  
  
    -   Data ultima modifica  
  
    -   Autore ultima modifica  
  
    -   Cartella server  
  
    -   Tipo  
  
     Per trovare un'immagine, ad esempio, fare clic su **Aggiungi criteri**e quindi su **Tipo**. Nella casella a discesa selezionare la casella di controllo **Immagine** premere INVIO e quindi fare clic sulla lente di ingrandimento Cerca.  
  
    > [!NOTE]  
    >  Per i valori **Creato da** e **Autore ultima modifica** cercare il nome utente della persona come rappresentato nel server di report.  
  
### <a name="to-set-a-default-folder-for-report-parts"></a>Per impostare una cartella predefinita per parti di report  
  
1.  Fare clic su **Generatore report**e quindi su **Opzioni**.  
  
2.  Nella scheda **Impostazioni** della finestra di dialogo **Opzioni** digitare un nome per la cartella nella casella di testo **Pubblica parti del report in questa cartella per impostazione predefinita** .  
  
 In Generatore report verrà creata questa cartella se non ancora esistente e se l'utente dispone delle autorizzazioni per la creazione di cartelle nel server di report.  
  
 Non è necessario riavviare Generatore report affinché questa impostazione venga applicata.  
  
## <a name="see-also"></a>Vedere anche  
 [Verificare o gli aggiornamenti Turn Off &#40;Report e SSRS&#41;](../check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)   
 [Parti del report &#40;Generatore report e SSRS&#41;](../report-parts-report-builder-and-ssrs.md)   
 [Parti del report e set di dati in Generatore report](../report-data/report-parts-and-datasets-in-report-builder.md)   
 [Risolvere i problemi di parti del Report &#40;Report e SSRS&#41;](../troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [Pubblicare e ripubblicare parti del report &#40;Generatore report e SSRS&#41;](publish-and-republish-report-parts-report-builder-and-ssrs.md)  
  
  
