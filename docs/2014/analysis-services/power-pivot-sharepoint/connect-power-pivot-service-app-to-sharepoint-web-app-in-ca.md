---
title: Connettere un'applicazione del servizio PowerPivot a un'applicazione Web di SharePoint in Amministrazione centrale | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a5da8e29-7ffd-44e7-bf61-344fa5bea8ce
author: minewiskan
ms.author: owend
ms.openlocfilehash: a7288979fdba0752149d8bdc6491e8c51cdebedc
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547513"
---
# <a name="connect-a-powerpivot-service-application-to-a-sharepoint-web-application-in-central-administration"></a>Connettere un'applicazione del servizio PowerPivot a un'applicazione Web SharePoint in Amministrazione centrale
  Un'applicazione di servizio PowerPivot può essere utilizzata da un numero qualsiasi di applicazioni Web SharePoint nella farm. Per rendere disponibile un'applicazione di servizio PowerPivot, aggiungerla a un elenco di associazioni al servizio.  
  
> [!IMPORTANT]  
>  Per assicurare il corretto funzionamento del dashboard di gestione PowerPivot, è necessario che almeno un'applicazione di servizio PowerPivot sia presente nel gruppo predefinito. Non aggiungere più di un'applicazione di servizio PowerPivot al gruppo predefinito. L'aggiunta di più voci dello stesso tipo di applicazione di servizio non è una configurazione supportata e potrebbe provocare errori. Se si creano applicazioni di servizio aggiuntive, aggiungerle agli elenchi personalizzati.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Aggiungere l'applicazione di servizio PowerPivot al gruppo predefinito](#default)  
  
 [Aggiungere l'applicazione di servizio PowerPivot a un elenco personalizzato di associazioni al servizio](#custom)  
  
##  <a name="add-powerpivot-services-application-to-the-default-group"></a><a name="default"></a>Aggiungere l'applicazione di servizi PowerPivot al gruppo predefinito  
 Un elenco di associazioni al servizio è un elenco di servizi condivisi che forniscono risorse ad altre applicazioni Web SharePoint nella farm. Per la farm è disponibile un gruppo predefinito di associazioni al servizio.  
  
 Per essere nell'elenco, un'applicazione di servizio PowerPivot può essere aggiunta al momento della creazione o in seguito eseguendo i passaggi seguenti.  
  
1.  In Amministrazione centrale, in **Gestione applicazioni**, fare clic su **Configura associazioni dell'applicazione di servizio**.  
  
2.  In Gruppo proxy applicazioni fare clic su **predefinito**.  
  
3.  Selezionare la casella di controllo accanto all'applicazione di servizio PowerPivot (indicata dal nome del tipo `PowerPivot Service Application Proxy`). Se sono presenti più applicazioni di servizio PowerPivot, sceglierne solo una.  
  
4.  Fare clic su **OK**.  
  
##  <a name="add-powerpivot-services-application-a-custom-service-association-list"></a><a name="custom"></a>Aggiunta di un'applicazione di servizi PowerPivot a un elenco di associazioni di servizi personalizzato  
 Il gruppo predefinito può essere sostituito da un elenco personalizzato. Un elenco personalizzato viene creato in modo specifico per una sola applicazione Web SharePoint. Il gruppo predefinito viene sostituito solo dalle associazioni al servizio specificate da un amministratore di farm o del servizio. Se sono state create più applicazioni di servizio PowerPivot, è necessario utilizzare un elenco personalizzato per specificare quale utilizzare. Un elenco personalizzato non può essere riutilizzato da altre applicazioni Web. Si applica solo all'applicazione Web per cui è stato creato.  
  
1.  In **Gestione applicazioni**di Amministrazione centrale fare clic su **Gestisci applicazioni Web**.  
  
2.  Selezionare l'applicazione, ad esempio SharePoint -80.  
  
3.  In Applicazioni Web, in Gestisci, fare clic su **Connessioni servizio**.  
  
4.  In **Modifica il gruppo di connessioni seguente**selezionare **[personalizzato]**.  
  
5.  Selezionare la casella di controllo accanto a ogni connessione all'applicazione di servizio che si desidera utilizzare. Se sono presenti più applicazioni di servizio PowerPivot (indicato dal tipo impostato su `PowerPivot Service Application Proxy`), assicurarsi di sceglierne una sola.  
  
6.  Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione e configurazione di un'applicazione di servizio PowerPivot in Amministrazione centrale](create-and-configure-power-pivot-service-application-in-ca.md)   
 [Configurazione iniziale &#40;PowerPivot per SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)  
  
  
