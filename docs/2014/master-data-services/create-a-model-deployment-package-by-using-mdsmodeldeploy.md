---
title: Creare un pacchetto di distribuzione di modelli tramite MDSModelDeploy | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: c2687e39-dc20-494f-a707-2aa29f4c329e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0f26ef1429d24b93d3c2aa59d613a6ec37684a89
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971811"
---
# <a name="create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Creare un pacchetto di distribuzione di modelli tramite MDSModelDeploy
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]usare lo strumento MDSModelDeploy per creare un pacchetto. A seconda dei comandi specificati, il pacchetto può contenere:  
  
-   Solo oggetti modello.  
  
-   Dati e oggetti modello.  
  
 Per distribuire un pacchetto contenente solo oggetti modello, è possibile utilizzare la Distribuzione guidata modello nell'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Per altre informazioni, vedere [Creare un pacchetto di distribuzione di modelli tramite la procedura guidata](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md).  
> [!NOTE]  
> Questa versione dello strumento MDSModelDeploy non può usare più di gigabyte (GB) di memoria. Quando si creano o si distribuiscono modelli di grandi dimensioni utilizzando **gli oggetti modello e** l'opzione dati, è possibile che si verifichino errori di "memoria insufficiente" o "flusso troppo lungo". Per risolvere questo problema, utilizzare la gestione temporanea MDS per distribuire i dati. in alternativa, eseguire l'aggiornamento a MDS 2016 o versione successiva, che include la versione aggiornata dello strumento MDSModelDeploy.
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
1.  Di seguito sono riportate le autorizzazioni di base necessarie per eseguire lo strumento MDSModelDeploy:  
  
    -   Stessa autorizzazione di Windows di Gestione configurazione MDS (amministratore di Windows)  
  
    -   Autorizzazione DBA per il database MDS.  
  
2.  Di seguito sono riportate le autorizzazioni necessarie per creare il pacchetto tramite lo strumento MDSModelDeploy:  
  
    -   Autorizzazione dell'amministratore di modelli di MDS per il modello di dati  
  
    -   Autorizzazione per la funzione Gestione integrazione di MDS.  
  
3.  Di seguito sono riportate le autorizzazioni necessarie per distribuire un modello tramite lo strumento MDSModelDeploy:  
  
    -   Autorizzazione per la funzione Esplora di MDS  
  
    -   Autorizzazione per la funzione Gestione integrazione di MDS  
  
    -   Autorizzazione per la funzione Amministrazione sistema di MDS.  
  
4.  Di seguito sono riportate le autorizzazioni necessarie per elencare i modelli tramite lo strumento MDSModelDeploy:  
  
    -   Autorizzazione per la funzione Esplora di MDS  
  
    -   Autorizzazione dell'amministratore di modelli di MDS sul modello di dati per visualizzare il modello nell'elenco.  
  
 È necessario che sia disponibile un modello affinché sia possibile crearne un pacchetto. Per altre informazioni, vedere [Creare un modello &#40;Master Data Services&#41;](create-a-model-master-data-services.md).  
  
 Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Per creare un pacchetto di distribuzione modelli tramite MDSModelDeploy  
  
1.  Aprire un prompt dei comandi.  
  
2.  Spostarsi sul percorso di MDSModelDeploy.exe.  
  
    -   Se MDS è stato installato nel percorso predefinito, il file si trova in *unità*: \Programmi\microsoft SQL Server\120\Master Data Services\Configuration.  
  
    -   Se MDS non è stato installato nel percorso predefinito, cercare MDSModelDeploy.exe nel computer locale.  
  
3.  Facoltativa. Visualizzare le opzioni e la Guida.  
  
    -   Per visualizzare tutte le opzioni disponibili, digitare `MDSModelDeploy` e premere Invio.  
  
    -   Per visualizzare la Guida per un'opzione, digitare quanto segue, dove *OptionName* è il nome dell'opzione: `MDSModelDeploy help OptionName`.  
  
4.  Facoltativa. Se sono disponibili più applicazioni Web, determinare il nome del servizio in cui verrà eseguita la distribuzione digitando questo comando e premendo INVIO:  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     Verrà restituito un elenco di valori, ad esempio `MDS1, Default Web Site, MDS`. Il primo valore di questo elenco, in questo caso `MDS1`, è necessario per distribuire il modello.  
  
5.  Per creare un pacchetto contenente oggetti modello e dati, digitare quanto segue, dove *ModelName*, *VersionName*, *ServiceName*e *PackageName* sono rispettivamente i nomi del modello, della versione, del servizio e del file di output con estensione pkg:  
  
    ```  
    MDSModelDeploy createpackage -model ModelName -version VersionName -service ServiceName -package PackageName -includedata  
    ```  
  
     Se non si vuole includere dati, non usare le opzioni `-version` e `-includedata` .  
  
6.  Premere Invio. Al termine della creazione del pacchetto, verrà visualizzato un messaggio "Operazione MDSModelDeploy completata".  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   [Distribuire un pacchetto di distribuzione di modelli tramite MDSModelDeploy](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di distribuzione del modello &#40;Master Data Services&#41;](../../2014/master-data-services/model-deployment-options-master-data-services.md)   
 [Distribuzione di modelli &#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  
