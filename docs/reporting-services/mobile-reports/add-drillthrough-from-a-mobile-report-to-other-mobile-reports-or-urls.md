---
title: Aggiungere il drill-through da un report per dispositivi mobili ad altri report per dispositivi mobili o URL | Microsoft Docs
ms.date: 09/20/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 30d0a3fd-5588-417e-b25d-cc5b7624cdb1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9bf66cdaad2f0ad85ff0213bb0711723e6ed3d05
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291953"
---
# <a name="add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls"></a>Aggiungere il drill-through da un report per dispositivi mobili ad altri report per dispositivi mobili o URL
È possibile aggiungere il drill-through da qualsiasi misuratore, grafico o griglia dati di un report per dispositivi mobili di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] a un altro report o URL personalizzato. 

Un *drill-through*  è un collegamento da un report di origine che apre un altro URL o report di destinazione. Il report drill-through di destinazione contiene spesso dettagli su alcuni elementi presenti nel report di riepilogo. A seconda del report per dispositivi mobili di origine, uno o più parametri possono essere passati al report per dispositivi mobili di destinazione o integrati in un URL personalizzato.  
  
Quando si visualizza il report per dispositivi mobili di origine nel portale Web di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] e si seleziona un elemento con una destinazione di drill-through, si viene indirizzati a tale destinazione, che può essere un altro report per dispositivi mobili o un URL.  

Gli elementi di report con drill-through, verso un URL o un altro report per dispositivi mobili, sono contrassegnati da un'apposita icona ![mobile-report-drill-through-icon](../../reporting-services/mobile-reports/media/mobile-report-drill-through-icon.png) nell'angolo superiore destro.

![mobile-report-gauge-drill-through](../../reporting-services/mobile-reports/media/mobile-report-gauge-drill-through.png) 

>**Suggerimento**: creare prima il report di destinazione e salvarlo in un portale Web di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]. Se si prevede di passare i parametri dal report di origine, aggiungere quindi i parametri anche al report di destinazione. A questo punto è possibile impostare il drill-through dal report di origine al report di destinazione. [Aggiungere parametri a un report per dispositivi mobili](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md).
 
## <a name="set-up-drillthrough-to-a-mobile-report"></a>Impostare il drill-through in un report per dispositivi mobili  

1. Nella vista Layout di [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]selezionare una visualizzazione che supporti il drill-through.   

   Il drill-through è supportato dalle mappe e dai misuratori, nonché dalla maggior parte dei grafici e delle griglie dati semplici.
   
2. Nel riquadro **Proprietà visive** selezionare **Destinazione del drill-through** > **Report per dispositivi mobili**.  
3. Selezionare il server e il report per dispositivi mobili di destinazione.  

   >Nota: se il report per dispositivi mobili di destinazione non si trova nello stesso server del report per dispositivi mobili di origine, connettersi ad esso con un URL personalizzato, come illustrato nella sezione seguente.  
 
4. Dopo aver selezionato un report per dispositivi mobili di destinazione, verranno visualizzati i parametri di input disponibili, incluse le proprietà che possono essere associate ai controlli di selezione e i parametri configurati nei set di dati del report per dispositivi mobili di destinazione.  

   ![mobile-report-drillthrough-target](../../reporting-services/mobile-reports/media/mobile-report-drillthrough-target.PNG)
   
   *Proprietà di drill-through per il report per dispositivi mobili di destinazione*  
  
5. Selezionare la freccia a destra di ogni proprietà per connettere proprietà con tipi di dati corrispondenti alle proprietà di output disponibili nel report per dispositivi mobili di origine. In questa pagina è possibile anche impostare valori predefiniti per ogni output, nel caso in cui l'utente del report non abbia interagito con il report per dispositivi mobili di origine prima di eseguire il drill-through al report per dispositivi mobili di destinazione.  
  
## <a name="set-up-a-drillthrough-to-a-custom-url"></a>Impostare un drill-through a un URL personalizzato  
  
1. Nella vista Layout di [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]selezionare una visualizzazione che supporti destinazioni di drill-through.    
2. Nel riquadro **Proprietà visive** selezionare **Destinazione del drill-through** > **URL personalizzato**.  Verrà aperta la finestra di dialogo per la configurazione del drill-through.  
  
3. In **Imposta URL di drill-through** immettere l'URL di destinazione a cui essere indirizzati quando viene selezionata la visualizzazione e quindi selezionare una voce dall'elenco **Parametri disponibili** sulla destra. Nel riquadro seguente viene visualizzata un'anteprima dell'URL personalizzato combinato con esempi di parametri risolti (se disponibili).  
  
   ![mobile-report-drillthrough-url](../../reporting-services/mobile-reports/media/mobile-report-drillthrough-url.PNG)
  
   *Drill-through a proprietà personalizzate dell'URL*  
  
4. Fare clic su **Applica**.  

  
Quando si visualizza l'anteprima di un report per dispositivi mobili in [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)], se si fa clic su una visualizzazione con drill-through, viene visualizzato un messaggio in cui si informa l'utente che drill-through è disabilitato. È infatti possibile eseguire il drill-through alla destinazione solo dopo aver salvato, pubblicato e visualizzato un report per dispositivi mobili, non dal layout o dalla modalità di anteprima di [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] .  

## <a name="hide-a-target-mobile-report-on-the-web-portal"></a>Nascondere un report per dispositivi mobili nel portale Web
Se non si intende impostare un valore predefinito per il report di destinazione, è possibile nasconderlo nel portale Web. In caso contrario, se un utente tenta di visualizzarlo direttamente nel portale Web, senza passare attraverso il report di origine, il report di destinazione risulterà vuoto.

1. Nel portale Web selezionare i puntini di sospensione (...) relativi al report di destinazione che si vuole nascondere e selezionare Gestisci.

2. In **Proprietà**selezionare **Nascondi in visualizzazione affiancata**.

È possibile scegliere di visualizzare gli elementi nascosti nel portale Web: 

* Nell'angolo superiore destro del portale Web selezionare **Visualizza** > **Mostra nascosti**. 

Gli elementi nascosti vengono visualizzati in un colore più chiaro.
    
### <a name="see-also"></a>Vedere anche  
 
* [Aggiungere parametri a un report per dispositivi mobili di Reporting Services](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [Creare report per dispositivi mobili con SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 
* [Portale Web (modalità nativa SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)

