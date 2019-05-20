---
title: Impostare la lingua per i parametri del report in un URL | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- overriding report language settings
- report servers [Reporting Services], language settings
- languages [Reporting Services]
- URL access [Reporting Services], language overrides
- international considerations [Reporting Services]
- global considerations [Reporting Services]
ms.assetid: e1ccf22f-80d6-45bc-aae0-f5f263275092
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 98ff61142ff7b748ba6a16b632b256e8b0ec3c47
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65579403"
---
# <a name="set-the-language-for-report-parameters-in-a-url"></a>Impostare la lingua per i parametri del report in un URL
  Il parametro di accesso con URL *rs:ParameterLanguage* consente di risolvere un problema di interpretazione dei parametri del report con distinzione delle impostazioni cultura, come date, ore, valuta e numeri, in base alla lingua del browser. Con *rs:ParameterLanguage*l'URL viene ora interpretato in modo indipendente dal browser. Se, ad esempio, per il server di report sono definite le impostazioni internazionali per il tedesco, ma un utente accede a un report tramite un URL utilizzando un browser che è impostato su Inglese (Stati Uniti), i valori dei parametri passati a un server di report vengono interpretati in modo errato.  
  
 Considerare il seguente URL che rimanda a un report:  
  
```  
https://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008  
```  
  
 In questo caso il server, in esecuzione in base alle impostazioni cultura "de-de", genera un URL tramite una sottoscrizione di posta elettronica o un collegamento ipertestuale. Il collegamento ipertestuale indica che i parametri del report devono essere interpretati con una data di inizio del 4 ottobre 2008 e una data di fine dell'11 ottobre 2008, in base agli standard di data/ora per il tedesco. Se tuttavia un utente accede all'URL tramite un browser impostato su "en-us", il server interpreta i valori come il 10 aprile 2008 e  10 novembre 2008, in base agli standard di data/ora per l'inglese degli Stati Uniti. Per risolvere il problema, è possibile usare *rs:ParameterLanguage* per eseguire l'override della lingua del browser per l'interpretazione dei parametri:  
  
```  
https://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
```  
  
 Oltre ai valori **true** e **false** , per il parametro di accesso con URL *rc:Parameters*è ora possibile passare il valore **Collapsed**. Quando si usa *rc:Parameters*=**Collapsed** in un URL, l'area dei messaggi di richiesta dei parametri del visualizzatore HTML viene compressa e non è più visualizzata, ma l'utente può comunque scegliere di visualizzarla. Il valore **false** consente di rimuovere l'area dei messaggi di richiesta dei parametri dalla barra degli strumenti del visualizzatore HTML, in modo che non sia più disponibile per l'utente finale.  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso con URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Riferimento ai parametri di accesso con URL](../reporting-services/url-access-parameter-reference.md)  
  
  
