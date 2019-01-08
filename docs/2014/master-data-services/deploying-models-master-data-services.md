---
title: Distribuzione di modelli (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], about deployment packages
- deployment packages [Master Data Services]
ms.assetid: 30085c08-034f-4efe-80fe-408f9091ff5c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 58f946f89691a6e26ba4402166b8ad725e7a977c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761783"
---
# <a name="deploying-models-master-data-services"></a>Distribuzione di modelli (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]un pacchetto è un file XML contenente una struttura di modello distribuibile e, facoltativamente, i dati del modello. Utilizzare i pacchetti del modello per spostare le copie di modelli da un ambiente MDS a un altro o per creare nuovi modelli nell'ambiente MDS esistente.  
  
> [!IMPORTANT]  
>  I pacchetti possono essere distribuiti solo nella versione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzata per crearli. Pertanto non è possibile distribuire pacchetti creati in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] o versione successiva.  
  
## <a name="tools-for-deploying-models"></a>Strumenti per la distribuzione di modelli  
 Per utilizzare i pacchetti di modello sono disponibili tre strumenti, a seconda delle proprie esigenze.  
  
-   **Strumento MDSModelDeploy**: Per creare e distribuire i dati e oggetti modello, usare lo strumento MDSModelDeploy.exe. Se si seleziona il percorso predefinito durante l'installazione di MDS, questo strumento è disponibile nel *unità*: \Programmi\Microsoft SQL Server\120\Master Data services\configuration.  
  
-   **Distribuzione guidata modello**: Per creare e distribuire i pacchetti di solo la struttura del modello, usare la procedura guidata nel [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] applicazione web. Non è possibile utilizzare questa procedura guidata per distribuire dati.  
  
-   **Editor pacchetti di modelli**: Per modificare un pacchetto di modelli, utilizzare ModelPackageEditor.exe che avvia la procedura guidata Editor pacchetti di modelli. Questa procedura guidata viene utilizzata per modificare un pacchetto creato dallo strumento MDSModelDeploy o dalla Distribuzione guidata modello. Se si seleziona il percorso predefinito durante l'installazione di MDS, questo strumento è disponibile nel *unità*: \Programmi\Microsoft SQL Server\120\Master Data services\configuration.  
  
> [!IMPORTANT]  
>  È possibile utilizzare MDSDeployModel per creare un nuovo modello, creare un clone di un modello oppure aggiornare un modello esistente e i relativi dati. Se si utilizza lo strumento MDSModelDeploy per aggiornare un modello esistente e i relativi dati e nel pacchetto non è contenuto alcun attributo, entità o membro disponibile nel modello di destinazione, questi elementi non saranno eliminati dal modello tramite MDSModelDeploy.  
  
## <a name="what-packages-contain"></a>Contenuto dei pacchetti  
 Un pacchetto del modello è un file XML salvato con estensione pkg. Quando si crea un pacchetto di distribuzione, è possibile decidere se includere o meno dati. Se si decide di includere dati, è necessario selezionare una versione dei dati da includere.  
  
 Tutti gli oggetti modello vengono inclusi in un pacchetto. Questi oggetti sono:  
  
-   Entità  
  
-   Attributi  
  
-   Gruppi di attributi  
  
-   Gerarchie  
  
-   Raccolte  
  
-   Regole business  
  
-   Flag versione  
  
-   Viste sottoscrizioni  
  
 Non sono inclusi i metadati definiti dall'utente, gli attributi file e le autorizzazioni di utenti e gruppi. Dopo avere distribuito un modello, è necessario aggiornare questi elementi manualmente.  
  
## <a name="sample-packages"></a>Pacchetti di esempio  
 I file di pacchetto di esempio sono inclusi nell'installazione di [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Questi file di pacchetto si trovano nella directory Master Data Services\Samples\Packages in cui è stato installato [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Quando si distribuiscono questi pacchetti di esempio tramite lo strumento MDSModelDeploy, i modelli di esempio vengono creati e popolati con dati.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Creare un nuovo pacchetto di distribuzione di oggetti modello e/o dati tramite lo strumento MDSModelDeploy.|[Creare un pacchetto di distribuzione di modelli tramite MDSModelDeploy](../../2014/master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|Creare un nuovo pacchetto di distribuzione solo di oggetti modello utilizzando la procedura guidata.|[Creare un pacchetto di distribuzione di modelli tramite la procedura guidata](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)|  
|Distribuite un pacchetto di oggetti modello e/o dati tramite lo strumento MDSModelDeploy.|[Distribuire un pacchetto di distribuzione di modelli tramite MDSModelDeploy](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|Distribuire un pacchetto solo di oggetti modello utilizzando la procedura guidata.|[Distribuire un pacchetto di distribuzione di modelli tramite la procedura guidata](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)|  
|Modificare un pacchetto di distribuzione del modello per distribuire parti selezionate di un modello, anziché l'intero modello.|[Modificare un pacchetto di distribuzione di modelli](../../2014/master-data-services/edit-a-model-deployment-package.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Opzioni di distribuzione dei modelli &#40;Master Data Services&#41;](model-deployment-options-master-data-services.md)  
  
  
