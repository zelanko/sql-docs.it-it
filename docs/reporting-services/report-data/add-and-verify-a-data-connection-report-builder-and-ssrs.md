---
title: Aggiungere e verificare una connessione dati (Generatore report) | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 03/01/2017
ms.openlocfilehash: 26ea58eaaaffbbd0c53d78ca971f472413be322b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082265"
---
# <a name="add-and-verify-a-data-connection-report-builder-and-ssrs"></a>Aggiungere e verificare una connessione dati (Generatore report e SSRS)

In Generatore report è possibile aggiungere un'origine dati condivisa dal server di report o creare un'origine dati incorporata per il report in uso. In Progettazione report è possibile creare un'origine dati condivisa o un'origine dati incorporata e distribuirla a un server di report.

Per aggiungere un'origine dati condivisa al report, accedere a un server di report e selezionare un'origine dati condivisa. L'origine dati condivisa del report punta alla definizione dell'origine dati condivisa nel server di report.

Per creare un'origine dati incorporata, l'utente deve disporre delle informazioni di connessione all'origine esterna di dati oltre a dover conoscere le autorizzazioni necessarie per l'accesso ai dati. Queste informazioni provengono solitamente dal proprietario dell'origine dati. Per verificare che le credenziali specificate siano sufficienti si può testare la connessione.

Per altre informazioni, vedere [Creare stringhe di connessione dati - Generatore report e SSRS](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) e [Specificare le credenziali in Generatore report](https://docs.microsoft.com/sql/reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources?view=sql-server-2017)

> [!NOTE]  
> [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

## <a name="to-create-a-connection-to-a-shared-data-source-in-report-builder"></a>Per creare una connessione a un'origine dati condivisa in Generatore report

1. Nel riquadro dei dati del report della barra degli strumenti fare clic su **Nuova** , quindi su **Origine dati**. Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .

2. Nella casella di testo **Nome** digitare un nome per l'origine dei dati.

    > [!NOTE]  
    >  Questo nome viene salvato nella definizione del report locale e non viene utilizzato per denominare l'origine dati condivisa nel server di report. 

3. Selezionare **Usa una connessione condivisa o un modello di report**. Verrà visualizzato l'elenco delle origini dati condivise e dei modelli di report utilizzati di recente. Per selezionarne una da un server di report fare clic su **Sfoglia** e scegliere la cartella nel server di report in cui sono disponibili le origini dati condivise.

4. Selezionare l'origine dati condivisa e quindi fare clic su **Apri**.

5. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

L'origine dati verrà visualizzata nel riquadro dei dati del report.

### <a name="to-verify-a-data-connection"></a>Per verificare una connessione dati  

1. Sulla barra degli strumenti del riquadro dei dati del report fare doppio clic sull'origine dati. Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .

2. Fare clic su **Test connessione**.

3. Se la connessione riesce, verrà visualizzato il messaggio seguente: "Creazione connessione completata". [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

4. In caso contrario, verrà visualizzato il messaggio: "Impossibile connettersi all'origine dati".  

5. Fare clic su **Dettagli**e utilizzare le informazioni per risolvere il problema.

    Per altre informazioni, vedere [Specifica di credenziali in Generatore report](https://docs.microsoft.com/sql/reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources?view=sql-server-2017).

6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="see-also"></a>Vedere anche

- [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
- [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)
- [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)
- [Creare stringhe di connessione dati - Generatore report e SSRS](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)