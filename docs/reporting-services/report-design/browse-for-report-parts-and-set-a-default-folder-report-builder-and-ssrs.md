---
title: Cercare parti del report e impostare una cartella predefinita (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 5cf38068-65d1-4fe8-81f3-a404d8fbc663
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2eef96c7bde16746a91fe53f94adb19bbadadf2e
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65581830"
---
# <a name="browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs"></a>Ricerca di parti del report e impostazione di una cartella predefinita (Generatore report e SSRS)
Il modo più semplice per creare un report impaginato di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] consiste nell'aggiungere parti del report esistenti, ad esempio tabelle e grafici, al report in uso dalla raccolta di parti del report. Quando una parte di report viene aggiunta al report in uso, vengono aggiunti anche tutti gli elementi necessari affinché funzioni. Ad esempio, qualsiasi parte di report che consenta la visualizzazione dei dati dipende da un set di dati, ovvero una query e una connessione a un'origine dati. Dopo aver aggiunto la parte di report al report in uso, è possibile modificarla in base alle necessità.  
  
 È possibile impostare una cartella predefinita per la pubblicazione di parti di report sul server di report o su un sito di SharePoint integrato con un server di report.  
  
 Per altre informazioni, vedere [Parti del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
## <a name="to-browse-for-report-parts"></a>Per cercare parti di report  
  
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
  
## <a name="to-set-a-default-folder-for-report-parts"></a>Per impostare una cartella predefinita per parti di report  
  
1.  Fare clic su **Generatore report**e quindi su **Opzioni**.  
  
2.  Nella scheda **Impostazioni** della finestra di dialogo **Opzioni** digitare un nome per la cartella nella casella di testo **Pubblica parti del report in questa cartella per impostazione predefinita** .  
  
 In Generatore report verrà creata questa cartella se non ancora esistente e se l'utente dispone delle autorizzazioni per la creazione di cartelle nel server di report.  
  
 Non è necessario riavviare Generatore report affinché questa impostazione venga applicata.  
  
## <a name="see-also"></a>Vedere anche  
 [Verificare o disattivare gli aggiornamenti (Generatore report e SSRS)](https://msdn.microsoft.com/9c69792d-d7c4-453b-ae2f-6d2d071d8606)   
 [Parti del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [Parti del report e set di dati in Generatore report](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Risoluzione dei problemi relativi alle parti del report (Generatore report e SSRS)](https://msdn.microsoft.com/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Pubblicare e ripubblicare parti del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)  
  
  
