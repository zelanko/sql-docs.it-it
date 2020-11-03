---
title: Creare un report per dispositivi mobili a schede usando il drill-through | Report per dispositivi mobili di Reporting Services | Microsoft Docs
description: Informazioni su come creare un report per dispositivi mobili di Reporting Services analogo a un report a schede in termini di aspetto e funzionamento usando il drill-through e parametri.
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 95b153be1b4dc5a45effeb678ca0ccef83f06e6e
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907339"
---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>Creare un report per dispositivi mobili a schede usando il drill-through
Informazioni su come creare un report per dispositivi mobili di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] analogo a un report a schede in termini di aspetto e funzionamento usando il drill-through e parametri.

In questo report, ad esempio, i misuratori nella parte superiore si comportano come le schede. Quando si sceglie il misuratore relativo ai trasporti, i dati nella parte restante del grafico vengono filtrati in base ai dati dei trasporti.

![Screenshot che mostra un report sui trasporti finanziari con il misuratore Transportation selezionato.](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

In realtà si tratta di un set di cinque report separati, ognuno con un parametro diverso che filtra il report in modo che corrisponda al misuratore selezionato nella parte superiore del report. Vengono prima creati i cinque report, quindi per ciascuno dei cinque report vengono creati gli altri quattro misuratori nei drill-through agli altri quattro report.

Di seguito sono illustrati i passaggi per questo esempio.

## <a name="create-the-basic-report"></a>Creare il report di base

1. Creare un report denominato Sales con cinque misuratori:

    * Sales
    * Trasporti
    * Carburante
    * Archiviazione
    * Spese varie

   ![Screenshot di un report denominato Sales con cinque misuratori.](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. Impostare **Evidenziatore** su **Attivato** per i misuratori Sales in modo che appaia evidenziato rispetto agli altri elementi del report, in questo caso in bianco su nero.

    ![Screenshot del misuratore Sales con una freccia rossa che punta al dispositivo di scorrimento Evidenziatore impostato su Attivato.](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. Salvarlo in un server di report di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)].

## <a name="make-copies-of-the-report"></a>Creare copie del report

1. Creare quattro copie del report Sales e assegnare loro un nome: 

    * Trasporti
    * Carburante
    * Archiviazione
    * Spese varie

3. Salvare le copie nel server di report di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)].

## <a name="set-the-gauge-as-a-drillthrough"></a>Impostare il misuratore come drill-through

In questa sezione ogni misuratore (ad eccezione del misuratore Sales) vine impostato come drill-through al report corrispondente.

1. Nel report Sales selezionare il misuratore Transportation.

    ![Screenshot del report Sales con una freccia rossa dal misuratore Transportation all'opzione Destinazione del drill-through.](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. Con la scheda **Layout** selezionata, nel riquadro **Proprietà visive** selezionare **Destinazione del drill-through**.

3. Selezionare **Report per dispositivi mobili**.

4. Individuare e selezionare il report che sarà la destinazione del drill-through, in questo caso "Financials - Transportation".

    ![Screenshot della finestra di dialogo Apri dal server con l'opzione Financials - Transportation evidenziata.](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. In **Configura report di destinazione** selezionare il parametro per applicare un filtro al report e selezionare **Applica**.

   ![Screenshot della sezione Configura report di destinazione che mostra i parametri del report Financials - Transportation.](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. Ripetere questi passaggi per ciascuno degli altri misuratori del report Sales. 

## <a name="set-the-gauges-for-the-other-reports"></a>Impostare i misuratori per gli altri report

1.  Aprire il report Transportation, impostare il misuratore Sales come drill-through al report Sales e gli altri tre misuratori come drill-through ai rispettivi report.

2. Sempre nel report Transportation impostare **Evidenziatore** per il misuratore Transportation su **Attivato** in modo da evidenziarlo rispetto agli altri elementi del report.

3. Ripetere questi passaggi per i report Fuel, Storage e Misc Expenses. 

## <a name="view-the-report-in-the-web-portal"></a>Visualizzare il report nel portale Web

1. Passare al server di report di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] e aprire uno dei report. 

2. Si noti che ogni misuratore ha un'icona di drill-through nell'angolo superiore destro.

    ![Screenshot del misuratore Fuel.](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. Selezionare uno dei misuratori per passare al report filtrato con i dati del misuratore.

   ![Screenshot che mostra un report Financials - Transportation con una freccia rossa che punta al misuratore Transportation racchiuso in un riquadro rosso.](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>Vedere anche
    
* [Aggiungere parametri a un report per dispositivi mobili](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [Aggiungere il drill-through da un report per dispositivi mobili ad altri report per dispositivi mobili o URL](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  

