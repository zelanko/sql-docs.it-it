---
title: Creare un attributo di data (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating date attributes [Master Data Services]
- attributes [Master Data Services], creating date attributes
ms.assetid: 22a8f1a3-b4f2-4cfa-8495-7daad5ce9d12
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 7362431d33af429090497e9502daf1e1730fb768
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925200"
---
# <a name="create-a-date-attribute-master-data-services"></a>Creare un attributo di data (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare un attributo date quando si desidera che gli utenti inseriscano una data come valore di attributo.  
  
> [!NOTE]  
>  L'attributo viene chiamato DateTime, ma i valori ora non sono supportati.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   È necessario avere un'entità per la quale creare l'attributo. Per altre informazioni, vedere [Creare un'entità &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-create-a-date-attribute"></a>Per creare un attributo di data  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **Entità**.  
  
3.  Nella pagina **Gestione entità** selezionare un modello dall'elenco **Modello** .  
  
4.  Selezionare la riga relativa all'entità per la quale si desidera creare un attributo.  
  
5.  Fare clic su **Modifica entità selezionata**.  
  
6.  Nella pagina **Modifica entità** :  
  
    -   Se l'attributo è per membri foglia, nel riquadro **Attributi membro foglia** fare clic su **Aggiungi attributo foglia**.  
  
    -   Se l'attributo è per membri consolidati, nel riquadro **Attributi membro consolidati** fare clic su **Aggiungi attributo consolidato**.  
  
    -   Se l'attributo è per raccolte, nel riquadro **Attributi raccolta** fare clic su **Aggiungi attributo raccolta**.  
  
7.  Nella pagina **Aggiungi attributo** selezionare l'opzione **Formato libero** .  
  
8.  Nella casella **Nome** digitare un nome per l'attributo. Per un elenco di parole che non vanno usate come nomi di attributo, vedere [Parole riservate &#40;Master Data Services&#41;](../../2014/master-data-services/reserved-words-master-data-services.md).  
  
9. Nella casella **Larghezza in pixel visualizzazione** digitare la larghezza della colonna attributo da visualizzare nella griglia **Esplora** .  
  
10. Nell'elenco **Tipo di dati** selezionare **DateTime**.  
  
11. Nell'elenco **Maschera di input** selezionare un formato per le date.  
  
12. Facoltativamente, selezionare **Abilita rilevamento modifiche** per tenere traccia delle modifiche a gruppi di attributi. Per altre informazioni, vedere [Aggiungere attributi ad un gruppo rilevamento modifiche &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
13. Fare clic su **Salva attributo**.  
  
14. Nella pagina **Gestione entità** , fare clic su **Salva entità**.  
  
## <a name="to-display-the-time-portion-of-a-datetime-value"></a>Per visualizzare la porzione dell'ora di un valore datetime  
 Per fare in modo che nell'interfaccia utente venga visualizzata la porzione dell'ora di un valore datetime, è necessario selezionare una maschera di input appropriata per l'attributo. Questa operazione non viene effettuata da nessuna delle maschere predefinite per gli attributi Datetime, tuttavia è possibile aggiungerne una nuova tramite cui sarà possibile visualizzare l'ora. A tale scopo, aggiungere una riga nella tabella mdm.tblList del database MDS in cui sono archiviate le maschere predefinite. Nella riga dovrebbero essere presenti i valori seguenti:  
  
|||  
|-|-|  
|ListCode|lstInputMask|  
|ListName|Maschera di input|  
|Seq|19|  
|List Option|dd/MM/yyyy hh:mm:ss tt|  
|Option ID|19|  
|IsVisible|1|  
|Group_ID|3|  
  
 Dopo aver immesso una riga con i valori riportati in precedenza nella tabella mdm.tblList, la maschera "dd/MM/yyyy hh:mm:ss tt" sarà disponibile nella casella di riepilogo Maschera di input. È quindi possibile selezionare questa maschera per visualizzare la data e l'ora in una colonna di attributo datetime di un'entità in Esplora risorse di MDS.  
  
 La maschera di input è una stringa in formato DateTime .NET personalizzato. Per altre informazioni, vedere [Stringhe di formato di data e ora personalizzato](https://msdn.microsoft.com/library/8kb3ddd4\(v=vs.110\).aspx)  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [Modificare un nome di attributo &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [Creare un attributo basato su dominio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Creare un attributo di file &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
