---
title: Configurare le proprietà generali per un report (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], properties
- properties [Reporting Services], general
ms.assetid: 10b941b2-28e6-4408-9ee4-acebc63c8496
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 23184e77efbe41eae3d4de434a30ff8f3a4847ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177031"
---
# <a name="configure-general-properties-for-a-report-report-manager"></a>Configurare le proprietà generali per un report (Gestione report)
  
### <a name="to-configure-general-report-properties"></a>Per configurare le proprietà generali del report

1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md).

2.  In Gestione report passare alla pagina **contenuto** . quindi passare al report per il quale si desidera configurare le proprietà generali e aprirlo.

3.  Fare clic sulla scheda **Proprietà**.

     In alternativa, se la pagina **contenuto** è in visualizzazione dettagli, fare clic sull'icona della pagina delle proprietà:

     ![Icona della pagina delle proprietà](media/prop.gif "Icona della pagina delle proprietà")

4.  Viene visualizzata la pagina delle proprietà **generale** ed è possibile configurare le proprietà come indicato di seguito:

    -   Nella sezione **Proprietà** è possibile modificare il nome e la descrizione del report.

    -   È possibile selezionare la casella di controllo **Nascondi in visualizzazione elenco** per nascondere l'elemento quando la pagina viene aperta nel layout di pagina predefinito (visualizzazione elenco), che consente di disporre gli elementi in orizzontale e in basso nella pagina.

    -   Nella sezione **definizione del report** fare clic su **modifica** per estrarre una copia della definizione del report. Le modifiche apportate localmente alla definizione del report non vengono salvate nel server di report.

         In alternativa, per aggiornare la definizione del report da un file con estensione rdl, fare clic su **Aggiorna**.

        > [!NOTE]
        >  Se si aggiorna la definizione di un report è necessario reimpostare le impostazioni dell'origine dei dati dopo l'aggiornamento.

    -   Utilizzare i pulsanti **Elimina** o **Sposta** per eliminare o spostare il report.

    -   È inoltre possibile creare un report collegato.

5.  Al termine della configurazione delle proprietà generali per il report, fare clic su **applica**.

## <a name="see-also"></a>Vedere anche
 [Spostare o eliminare un elemento &#40;Gestione report](report-server/move-or-delete-an-item-report-manager.md) [pagina contenuto&#41;&#40;](../../2014/reporting-services/contents-page-report-manager.md) Gestione report&#41;la [ricerca, la visualizzazione e la gestione dei report &#40;Generatore report e SSRS &#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md) [pagina delle proprietà generale, report &#40;](../../2014/reporting-services/general-properties-page-reports-report-manager.md) Gestione report&#41;


