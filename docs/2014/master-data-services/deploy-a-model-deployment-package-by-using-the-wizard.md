---
title: Distribuire un pacchetto di distribuzione di modelli tramite la procedura guidata | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], deploying
- models [Master Data Services], deploying a package
ms.assetid: 4f65dc60-0ff8-46e6-9988-5bc5b9603ad0
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: cbdf233af3c0c27d6b4e95d18dc2c438d5307e7d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65479482"
---
# <a name="deploy-a-model-deployment-package-by-using-the-wizard"></a>Distribuire un pacchetto di distribuzione di modelli tramite la procedura guidata
  Utilizzare Distribuzione guidata modello [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] per distribuire pacchetti contenenti solo oggetti modello. Se è necessario distribuire un pacchetto con i dati, vedere [Distribuire un pacchetto di distribuzione di modelli tramite MDSModelDeploy](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
> [!IMPORTANT]  
>  I pacchetti possono essere distribuiti solo nella versione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzata per crearli. Pertanto non è possibile distribuire pacchetti creati in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Amministrazione sistema** nell'ambiente [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] di destinazione.  
  
-   È necessario che sia già disponibile un pacchetto di distribuzione di modelli. Per altre informazioni, vedere [Creare un pacchetto di distribuzione di modelli tramite la procedura guidata](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md).  
  
-   È necessario essere un amministratore nell'ambiente in cui viene distribuito il modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-deploy-a-model-deployment-package-of-model-objects-only"></a>Per distribuire un pacchetto di distribuzione di modelli di soli oggetti modello  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella barra dei menu della pagina **Vista modelli** scegliere **Sistema** , quindi fare clic su **Distribuzione**.  
  
3.  Su **Distribuzione guidata modello**, fare clic su **Distribuisci**.  
  
4.  Fare clic su **Sfoglia**.  
  
5.  Individuare il pacchetto di distribuzione (file con estensione pkg) e fare clic su **Apri**.  
  
6.  Fare clic su **Avanti**.  
  
7.  Dopo aver caricato il pacchetto, fare clic su **Avanti**.  
  
8.  Se il modello è già presente, è possibile aggiornarlo selezionando **Aggiorna il modello esistente**. Per creare un nuovo modello, selezionare **Crea un nuovo modello** e, dopo aver fatto clic su **Avanti** , è possibile digitare un nome per il nuovo modello.  
  
9. Fare clic su **Fine** per uscire dalla procedura guidata.  
  
 **Note**  
  
-   Se una vista sottoscrizioni nel pacchetto ha lo stesso nome di una vista sottoscrizioni in un modello esistente, la vista viene creata come *modelname. subscriptionviewname*. Se questo nome è già in uso, la vista della sottoscrizione non viene creata.  
  
-   Il processo di distribuzione si svolge in quattro passaggi:  
  
    1.  Creazione degli oggetti modello.  
  
    2.  Creazione delle viste sottoscrizioni.  
  
    3.  Creazione delle regole business.  
  
    4.  Popolamento dei dati master.  
  
-   Quando si crea un nuovo modello o se ne clona uno esistente, se si verifica un errore durante un qualsiasi passaggio del processo, il modello viene eliminato.  
  
     Quando si aggiorna un modello, se si verifica un errore durante uno dei primi tre passaggi, l'operazione viene interrotta; tuttavia il rollback delle modifiche già effettuate non viene eseguito. Se si verifica un errore durante il quarto passaggio, viene eseguito l'aggiornamento dei membri che è possibile aggiornare.  
  
## <a name="next-steps"></a>Passaggi successivi  
 I metadati definiti dall'utente, gli attributi di file e le autorizzazioni utente e gruppo non sono inclusi nei pacchetti di distribuzione dei modelli. Dopo avere distribuito un modello, è necessario aggiornare questi elementi manualmente. Per altre informazioni, vedere:  
  
-   [Aggiungere metadati &#40;Master Data Services&#41;](../../2014/master-data-services/add-metadata-master-data-services.md)  
  
-   [Assegnare autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione di modelli &#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  
