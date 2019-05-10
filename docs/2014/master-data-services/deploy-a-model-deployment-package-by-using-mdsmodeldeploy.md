---
title: Distribuire un pacchetto di distribuzione di modelli tramite MDSModelDeploy | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: fb2a4df4-5e0d-4b34-818f-383dbde1b15c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 81c87a7990c6c7125cbccbe99050cd5ee477e6d4
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483068"
---
# <a name="deploy-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Distribuire un pacchetto di distribuzione di modelli tramite MDSModelDeploy
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]utilizzare lo strumento MDSModelDeploy per distribuire un pacchetto contenente:  
  
-   Solo oggetti modello.  
  
-   Dati e oggetti modello.  
  
 Per distribuire un pacchetto contenente solo oggetti modello, è possibile utilizzare la Distribuzione guidata modello nell'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Per altre informazioni, vedere [Distribuire un pacchetto di distribuzione di modelli tramite la procedura guidata](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md).  
  
> [!IMPORTANT]  
>  I pacchetti possono essere distribuiti solo nella versione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzata per crearli. Pertanto non è possibile distribuire pacchetti creati in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] o versione successiva.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Amministrazione sistema** nell'ambiente [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] di destinazione.  
  
-   È necessario che sia già disponibile un pacchetto di distribuzione di modelli. Per altre informazioni, vedere  [Creare un pacchetto di distribuzione di modelli tramite MDSModelDeploy](../../2014/master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
-   È necessario essere un amministratore nell'ambiente in cui viene distribuito il modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Se si aggiorna un modello con i dati, lo stato della versione nella quale si esegue la distribuzione non può essere **Bloccato** o **Commit eseguito**.  
  
### <a name="to-deploy-a-model-deployment-package"></a>Per distribuire un pacchetto di distribuzione di modelli  
  
1.  Determinare se si distribuisce un nuovo modello, un clone di un modello o si aggiorna un modello clonato in precedenza. Per altre informazioni, vedere [Opzioni di distribuzione dei modelli &#40;Master Data Services&#41;](../../2014/master-data-services/model-deployment-options-master-data-services.md).  
  
2.  Aprire un prompt dei comandi e spostarsi su MDSModelDeploy.exe.  
  
    -   Se MDS è stato installato nel percorso predefinito, lo strumento è disponibile all'indirizzo *unità*: \Programmi\Microsoft SQL Server\120\Master Data services\configuration\mdsmodeldeploy.exe.  
  
    -   Se MDS non è stato installato nel percorso predefinito, cercare MDSModelDeploy.exe nel computer locale.  
  
3.  Facoltativo. Visualizzare le opzioni e la Guida.  
  
    -   Per visualizzare tutte le opzioni disponibili, digitare `MDSModelDeploy` e premere Invio.  
  
    -   Per visualizzare la Guida per un'opzione, digitare quanto segue, dove *OptionName* è il nome dell'opzione: `MDSModelDeploy help OptionName`.  
  
4.  Facoltativo. Se sono disponibili più applicazioni Web, determinare il nome del servizio in cui verrà eseguita la distribuzione digitando questo comando e premendo INVIO:  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     Verrà restituito un elenco di valori, ad esempio `MDS1, Default Web Site, MDS`. Il primo valore di questo elenco, in questo caso `MDS1`, è necessario per distribuire il modello.  
  
5.  A seconda del fatto che si crei, si cloni o si aggiorni un modello, al prompt dei comandi digitare quanto segue e premere INVIO.  
  
    -   Per creare un nuovo modello:  
  
        ```  
        MDSModelDeploy deploynew -package PackageName -model ModelName -service ServiceName  
        ```  
  
    -   Per creare un clone di un modello:  
  
        ```  
        MDSModelDeploy deployclone -package PackageName  
        ```  
  
    -   Per aggiornare un modello esistente e i relativi dati:  
  
        ```  
        MDSModelDeploy deployupdate -package PackageName -version VersionName  
        ```  
  
    > [!IMPORTANT]  
    >  Se si utilizza lo strumento MDSModelDeploy per aggiornare un modello esistente e i relativi dati e nel pacchetto non è contenuto alcun attributo, entità o membro disponibile nel modello di destinazione, questi elementi non saranno eliminati dal modello tramite MDSModelDeploy.  
  
     Dove *PackageName* è il nome del file di pacchetto (con estensione pkg), *ModelName* è il nome del nuovo modello, *VersionName* è il nome della versione e *ServiceName* è il nome del servizio del passaggio precedente. Assicurarsi che i nomi della versione e del modello corrispondano esattamente ai nomi, rispettando la distinzione tra maiuscole e minuscole.  
  
6.  Al termine della distribuzione del pacchetto, verrà visualizzato un messaggio "Operazione MDSModelDeploy completata".  
  
 **Note:**  
  
-   Se una vista sottoscrizioni nel pacchetto ha lo stesso nome di una vista sottoscrizioni in un modello esistente, la vista viene creata come *subscriptionviewname*. Se questo nome è già in uso, la vista della sottoscrizione non viene creata.  
  
-   Il processo di distribuzione si svolge in quattro passaggi:  
  
    1.  Creazione degli oggetti modello.  
  
    2.  Creazione delle regole business.  
  
    3.  Creazione delle viste sottoscrizioni.  
  
    4.  Popolamento dei dati master.  
  
-   Quando si crea un nuovo modello o se ne clona uno esistente, se si verifica un errore durante un qualsiasi passaggio del processo, il modello viene eliminato.  
  
     Quando si aggiorna un modello, se si verifica un errore durante i primi tre passaggi, l'operazione viene interrotta; tuttavia il rollback delle modifiche già effettuate non viene eseguito. Se si verifica un errore durante il quarto passaggio, viene eseguito l'aggiornamento dei membri che è possibile aggiornare.  
  
## <a name="next-steps"></a>Passaggi successivi  
 I metadati definiti dall'utente, gli attributi di file e le autorizzazioni utente e gruppo non sono inclusi nei pacchetti di distribuzione dei modelli. Dopo avere distribuito un modello, è necessario aggiornare questi elementi manualmente. Per altre informazioni, vedere:  
  
-   [Aggiungere metadati &#40;Master Data Services&#41;](../../2014/master-data-services/add-metadata-master-data-services.md)  
  
-   [Assegnare autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione di modelli &#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  
