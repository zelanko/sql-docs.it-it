---
title: La connessione del servizio App di Power Pivot in App Web di SharePoint in Autorità di certificazione | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fd72f62cc513064e01c04e5a501b18a070f4c7a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208277"
---
# <a name="connect-power-pivot-service-app-to-sharepoint-web-app-in-ca"></a>La connessione del servizio App di Power Pivot per App Web di SharePoint nella CA
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Un'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] può essere usata da un numero qualsiasi di applicazioni Web SharePoint nella farm. Per rendere disponibile un'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , aggiungerla a un elenco di associazioni del servizio.  
  
> [!IMPORTANT]  
>  Per assicurare il corretto funzionamento del dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , è necessario che almeno un'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sia presente nel gruppo predefinito. Non aggiungere più di un'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] al gruppo predefinito. L'aggiunta di più voci dello stesso tipo di applicazione di servizio non è una configurazione supportata e potrebbe provocare errori. Se si creano applicazioni di servizio aggiuntive, aggiungerle agli elenchi personalizzati.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
 [Aggiungere l'applicazione del servizio PowerPivot al gruppo predefinito](#default)  
  
 [Aggiungere l'applicazione del servizio PowerPivot a un elenco personalizzato di associazioni del servizio](#custom)  
  
##  <a name="default"></a> Aggiungere l'applicazione di servizio al gruppo predefinito  
 Un elenco di associazioni al servizio è un elenco di servizi condivisi che forniscono risorse ad altre applicazioni Web SharePoint nella farm. Per la farm è disponibile un gruppo predefinito di associazioni al servizio.  
  
 Per essere nell'elenco, un'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] può essere aggiunta al momento della creazione o successivamente, eseguendo questi passaggi.  
  
1.  In Amministrazione centrale, in **Gestione applicazioni**, fare clic su **Configura associazioni dell'applicazione di servizio**.  
  
2.  In Gruppo proxy applicazioni fare clic su **predefinito**.  
  
3.  Selezionare la casella di controllo accanto all'applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (indicata dal nome del tipo **Power Pivot Service Application Proxy**). Se sono presenti più applicazioni del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , sceglierne solo una.  
  
4.  Fare clic su **OK**.  
  
##  <a name="custom"></a> Aggiungere l'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a un elenco personalizzato di associazioni del servizio  
 Il gruppo predefinito può essere sostituito da un elenco personalizzato. Un elenco personalizzato viene creato in modo specifico per una sola applicazione Web SharePoint. Il gruppo predefinito viene sostituito solo dalle associazioni al servizio specificate da un amministratore di farm o del servizio. Se sono state create più applicazioni del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , è necessario usare un elenco personalizzato per specificare quale usare. Un elenco personalizzato non può essere riutilizzato da altre applicazioni Web. Si applica solo all'applicazione Web per cui è stato creato.  
  
1.  In **Gestione applicazioni**di Amministrazione centrale fare clic su **Gestisci applicazioni Web**.  
  
2.  Selezionare l'applicazione, ad esempio SharePoint -80.  
  
3.  In Applicazioni Web, in Gestisci, fare clic su **Connessioni servizio**.  
  
4.  In **Modifica il gruppo di connessioni seguente**selezionare **[personalizzato]** .  
  
5.  Selezionare la casella di controllo accanto a ogni connessione all'applicazione di servizio che si desidera utilizzare. Se sono presenti più applicazioni di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , ovvero il tipo è impostato su **Power Pivot Service Application Proxy**(Proxy dell'applicazione di servizio PowerPivot), assicurarsi di sceglierne una sola.  
  
6.  Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e configurare un'applicazione del servizio Power Pivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [Configurazione iniziale (Power Pivot per SharePoint)](http://msdn.microsoft.com/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)  
  
  
