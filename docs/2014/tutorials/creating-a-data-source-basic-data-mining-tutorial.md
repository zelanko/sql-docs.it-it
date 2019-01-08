---
title: Creazione di un'origine dati (esercitazione di base di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d7107c32-69ed-49a8-9b6e-32753eebf42c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0e216aa5da4ef837da632ba83d4cf6e14edb40b1
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376453"
---
# <a name="creating-a-data-source-basic-data-mining-tutorial"></a>Creazione di un'origine dati (Esercitazione di base sul data mining)
  Oggetto *zdroj dat* è una connessione dati salvata e gestita del progetto e distribuita per il [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] database. L'origine dati contiene il nome del server e del database in cui si trovano i dati di origine in aggiunta ad altre proprietà di connessione necessarie.  
  
> [!IMPORTANT]  
>  Il nome del database è [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. Se questo database non già installato, vedere la [Microsoft SQL Sample Databases](https://go.microsoft.com/fwlink/?LinkId=88417) pagina.  
  
### <a name="to-create-a-data-source"></a>Per creare un'origine dati  
  
1.  Nella **Esplora soluzioni**, fare doppio clic il **Zdroje dat** cartella e selezionare **nuova origine dati**.  
  
2.  Nel **Creazione guidata origine dati** pagina, fare clic su **successivo**.  
  
3.  Nel **selezionare la modalità di definizione connessione** pagina, fare clic su **New** per aggiungere una connessione al [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] database.  
  
4.  Nel **Provider** nell'elenco **gestione connessione**, selezionare **OLE DB nativo\sql Server Native Client 11.0**.  
  
5.  Nel **nome Server** digitare o selezionare il nome del server in cui è installato [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)].  
  
     Ad esempio, digitare **localhost** se il database è ospitato nel server locale.  
  
6.  Nel **accedere al server** gruppo, selezionare **Usa autenticazione di Windows**.  
  
    > [!IMPORTANT]  
    >  Se possibile, gli implementatori devono utilizzare l'autenticazione di Windows, che fornisce un metodo di autenticazione più sicuro rispetto all'autenticazione di SQL Server. Tuttavia, l'autenticazione di SQL Server è disponibile per la compatibilità con le versioni precedenti. Per altre informazioni sui metodi di autenticazione, vedere [configurazione del motore di Database - Provisioning Account](../../2014/sql-server/install/database-engine-configuration-account-provisioning.md).  
  
7.  Nel **selezionare o immettere un nome di database** , selezionare dalla lista [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] e quindi fare clic su **OK**.  
  
8.  Scegliere **Avanti**.  
  
9. Nel **le informazioni sulla rappresentazione** pagina, fare clic su **Usa account del servizio**e quindi fare clic su **Avanti**.  
  
     Nel **Completamento procedura guidata** pagina, si noti che, per impostazione predefinita, l'origine dati è denominata Adventure Works DW 2012.  
  
10. Scegliere **Fine**.  
  
     La nuova origine dati, Adventure Works DW 2012, viene visualizzato nei **Zdroje dat** cartella in Esplora soluzioni.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di un tipo di dati della vista origine &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/creating-a-data-source-view-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Creazione di un'analisi di progetto di servizi &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un'origine dati &#40;SSAS multidimensionale&#41;](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [Definizione di un'origine dati](../analysis-services/lesson-1-2-defining-a-data-source.md)   
 [Impostare opzioni di rappresentazione &#40;SSAS multidimensionale&#41;](../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)  
  
  
