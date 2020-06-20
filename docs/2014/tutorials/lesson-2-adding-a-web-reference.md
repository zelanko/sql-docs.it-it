---
title: 'Lezione 2: aggiunta di un riferimento Web | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a2c2b8b8-6b13-45ca-ab3b-1582447b6807
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e455dd25c2b5d4ffa28bd2bdc28ff679861f1f1d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011406"
---
# <a name="lesson-2-adding-a-web-reference"></a>Lezione 2: Aggiunta di un riferimento Web
  L'individuazione di un servizio Web è il processo che consente a un client di individuare un servizio Web e ottenerne la descrizione. Il processo di individuazione di un servizio Web in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] implica l'interrogazione di un sito Web in base a un algoritmo predeterminato. Scopo di questo processo è quello di individuare la descrizione del servizio, ovvero un documento XML scritto nel linguaggio WSDL (Web Services Description Language).  
  
 Nella descrizione del servizio vengono indicati i servizi disponibili e le modalità di interazione con tali servizi. Senza una descrizione del servizio non è possibile interagire con un servizio Web a livello di programmazione.  
  
 L'applicazione deve disporre di un mezzo per comunicare con il servizio Web e per individuarlo in fase di esecuzione. Questo risultato si ottiene tramite l'aggiunta di un riferimento Web al progetto del servizio Web, operazione che consente di generare una classe proxy che si interfaccia con il servizio Web e ne fornisce una rappresentazione locale. Per ulteriori informazioni, vedere gli argomenti relativi alla generazione di un proxy del servizio Web XML nella documentazione di [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
### <a name="to-add-a-web-reference"></a>Per aggiungere un riferimento Web  
  
1.  Scegliere **Aggiungi riferimento al servizio**dal menu **progetto** .  
  
2.  Nella finestra di dialogo **Aggiungi riferimento al servizio** fare clic su **Avanzate**.  
  
3.  Nella finestra di dialogo **Impostazioni riferimento al servizio** fare clic su **Aggiungi riferimento Web**.  
  
4.  Nella casella **URL** della finestra di dialogo **Aggiungi riferimento Web** digitare l'URL per ottenere la descrizione del servizio Web ReportServer, ad esempio http://localhost/reportserver/reportservice2010.asmx . Fare quindi clic sul pulsante **Vai** per recuperare le informazioni sul servizio Web.  
  
     \- - oppure -  
  
     Se il servizio Web ReportServer esiste nel computer locale, fare clic sul collegamento **servizi Web nel computer locale** nel riquadro del browser. quindi fare clic sul collegamento del servizio Web ReportService2010 nell'elenco visualizzato.  
  
5.  Nella casella **nome riferimento Web** rinominare il riferimento Web in ReportService2010, ovvero lo spazio dei nomi che verrà utilizzato per questo riferimento Web.  
  
6.  Fare clic su **Aggiungi riferimento** per aggiungere un riferimento Web per il servizio Web di destinazione.  
  
     Tramite [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] verrà scaricata la descrizione del servizio e verrà generata una classe proxy che funge da interfaccia tra l'applicazione e il servizio Web ReportServer. È inoltre necessario aggiungere un riferimento allo spazio dei nomi <xref:System.Web.Services> per il riferimento Web da utilizzare.  
  
7.  Scegliere Aggiungi riferimento dal menu **Progetto**.  
  
8.  Nella finestra di dialogo **Aggiungi riferimento** , nella scheda **.NET** selezionare **System. Web. Services**, quindi fare clic su **OK**.  
  
 Per altre informazioni, vedere [Accesso all'API SOAP](../reporting-services/report-server-web-service/accessing-the-soap-api.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Servizio Web ReportServer](../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Lezione 3: accesso al servizio Web](../../2014/tutorials/lesson-3-accessing-the-web-service.md)   
 [Accesso al servizio Web ReportServer utilizzando Visual Basic o Visual C&#35; &#40;SSRS tutorial&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  
