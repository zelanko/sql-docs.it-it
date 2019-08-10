---
title: Creazione di un'origine dati (esercitazione di base sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d7107c32-69ed-49a8-9b6e-32753eebf42c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7fc2d6eebc342de7126ebd3c8c41c12e07107089
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68888746"
---
# <a name="creating-a-data-source-basic-data-mining-tutorial"></a>Creazione di un'origine dati (Esercitazione di base sul data mining)
  Un' *origine dati* è una connessione dati salvata e gestita nel progetto e distribuita [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nel database. L'origine dati contiene il nome del server e del database in cui si trovano i dati di origine in aggiunta ad altre proprietà di connessione necessarie.  
  
> [!IMPORTANT]  
>  Il nome del database è [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. Se il database non è ancora stato installato, vedere la pagina relativa ai [database di esempio di Microsoft SQL](https://go.microsoft.com/fwlink/?LinkId=88417) .  
  
### <a name="to-create-a-data-source"></a>Per creare un'origine dati  
  
1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse sulla cartella **origini dati** e scegliere **nuova origine dati**.  
  
2.  Nella pagina **iniziale della creazione guidata origine dati** fare clic su **Avanti**.  
  
3.  Nella [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] pagina **Selezione metodo di definizione connessione** fare clic su **nuova** per aggiungere una connessione al database.  
  
4.  Nell'elenco **provider** in **gestione connessione**selezionare **Native OLE DB nativo\SQL Server Native Client 11,0**.  
  
5.  Nella casella **nome server** Digitare o selezionare il nome del server in cui è installato [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)].  
  
     Ad esempio, digitare **localhost** se il database è ospitato nel server locale.  
  
6.  Nel gruppo **accedi al server** selezionare **Usa autenticazione di Windows**.  
  
    > [!IMPORTANT]  
    >  Se possibile, gli implementatori devono utilizzare l'autenticazione di Windows, che fornisce un metodo di autenticazione più sicuro rispetto all'autenticazione di SQL Server. Tuttavia, l'autenticazione di SQL Server è disponibile per la compatibilità con le versioni precedenti. Per ulteriori informazioni sui metodi di autenticazione, vedere [motore di database configurazione-](../../2014/sql-server/install/database-engine-configuration-account-provisioning.md)provisioning dell'account.  
  
7.  Nell'elenco **selezionare o immettere un nome di database** selezionare [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] e quindi fare clic su **OK**.  
  
8.  Fare clic su **Avanti**.  
  
9. Nella pagina **informazioni di rappresentazione** , fare clic su **Usa account del servizio**, quindi fare clic su **Avanti**.  
  
     Nella pagina **Completamento procedura guidata** si noti che, per impostazione predefinita, l'origine dati è denominata Adventure Works DW 2012.  
  
10. Scegliere **Fine**.  
  
     La nuova origine dati, Adventure Works DW 2012, viene visualizzata nella cartella **origini dati** in Esplora soluzioni.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di una vista &#40;origine dati esercitazione di base sul data mining&#41;](../../2014/tutorials/creating-a-data-source-view-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Esercitazione sulla creazione di &#40;un Analysis Services progetto di base sul data mining&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un'origine dati &#40;SSAS multidimensionale&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional)   
 [Definizione di un'origine dati](https://docs.microsoft.com/analysis-services/lesson-1-2-defining-a-data-source)   
 [Impostare opzioni di rappresentazione &#40;SSAS multidimensionale&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional)  
  
  
