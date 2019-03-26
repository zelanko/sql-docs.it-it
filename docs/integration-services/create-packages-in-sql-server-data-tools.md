---
title: Creare pacchetti in SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: bb3c085b-1458-49fa-8348-6a76b6e97ea6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a14545174705a0352023567bbb943d56dac9d336
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58279375"
---
# <a name="create-packages-in-sql-server-data-tools"></a>Creare pacchetti in SQL Server Data Tools
  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]è possibile creare un nuovo pacchetto con uno dei metodi seguenti:  
  
-   Utilizzare il modello di pacchetto incluso in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
-   Utilizzare un modello personalizzato  
  
     Per utilizzare pacchetti personalizzati come modelli per la creazione di nuovi pacchetti, è sufficiente copiare tali modelli nella cartella DataTransformationItems, che per impostazione predefinita si trova in C:\Programmi\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
-   Copiare un pacchetto esistente.  
  
     Se sono disponibili altri pacchetti che includono funzionalità che si desidera riutilizzare, sarà possibile compilare più rapidamente il flusso di controllo e i flussi di dati nel nuovo pacchetto copiando e incollando gli oggetti necessari da tali pacchetti. Per altre informazioni su come copiare e incollare oggetti nei progetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , vedere [Riutilizzo di oggetti di pacchetto](../integration-services/reuse-of-package-objects.md).  
  
     Se si crea un nuovo pacchetto copiando un pacchetto esistente oppure utilizzando un pacchetto personalizzato come modello, verranno copiati anche il nome e il GUID del pacchetto esistente. Sarà pertanto necessario modificare il nome e il GUID del nuovo pacchetto per distinguerlo da quello da cui è stato copiato. Se ad esempio sono presenti più pacchetti con lo stesso GUID, sarà più difficile stabilire a quale pacchetto appartengono i dati di un log. È possibile rigenerare la GUID nella proprietà **ID** e aggiornare il valore della proprietà **Name** usando la finestra Proprietà in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Per altre informazioni, vedere [Impostazione delle proprietà di un pacchetto](../integration-services/set-package-properties.md) e [Utilità dtutil](../integration-services/dtutil-utility.md).  
  
-   Utilizzare un pacchetto personalizzato designato come modello.  
  
-   Eseguire l’Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
     L'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] crea un pacchetto completo per un'importazione o un'esportazione semplice. Questa procedura guidata consente di configurare le connessioni, l'origine e la destinazione e di aggiungere tutte le trasformazioni dei dati necessarie per eseguire immediatamente l'importazione o l'esportazione. È facoltativamente possibile salvare il pacchetto per eseguirlo nuovamente in un secondo momento o rifinire e migliorare il pacchetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Se si salva il pacchetto, tuttavia, è necessario aggiungerlo a un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] esistente prima che sia possibile modificarlo o eseguirlo in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
 I pacchetti creati in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] tramite Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] vengono salvati nel file system. Per salvare un pacchetto in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o nell'archivio pacchetti, è necessario salvare una copia del pacchetto. Per altre informazioni, vedere [Salvataggio di una copia di un pacchetto](https://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31).  

 Per un video che illustra come creare un pacchetto di base usando il modello di pacchetto predefinito, vedere [Creazione di un pacchetto di base (video su SQL Server)](https://go.microsoft.com/fwlink/?LinkId=131023).  

## <a name="get-sql-server-data-tools"></a>Ottenere SQL Server Data Tools
Per installare SQL Server Data Tools (SSDT), vedere [Scaricare SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md).

## <a name="create-a-package-in-sql-server-data-tools-using-the-package-template"></a>Creare un pacchetto in SQL Server Data Tools usando il modello del pacchetto  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in cui si desidera creare un pacchetto.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse sulla cartella **Pacchetti SSIS** e scegliere **Nuovo pacchetto SSIS**.  
  
3.  Facoltativamente, è possibile aggiungere al pacchetto un flusso di controllo, attività flusso di dati e gestori di eventi. Per altre informazioni, vedere [Flusso di controllo](../integration-services/control-flow/control-flow.md), [Flusso di dati](../integration-services/data-flow/data-flow.md) e [Gestori eventi di Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-event-handlers.md).  
  
4.  Scegliere **Salva elementi selezionati** dal menu **File** per salvare il nuovo pacchetto.  
  
    > [!NOTE]  
    >  È possibile salvare un pacchetto vuoto.  
  
## <a name="choose-the-target-version-of-a-project-and-its-packages"></a>Scegliere la versione di destinazione di un progetto e i pacchetti correlati  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse su un progetto di Integration Services e scegliere **Proprietà** per aprire le pagine delle proprietà per il progetto.  
  
2.  Nella scheda **Generale** di **Proprietà di configurazione**selezionare la proprietà **TargetServerVersion** , quindi scegliere SQL Server 2016, SQL Server 2014 o SQL Server 2012.  
  
     ![Proprietà TargetServerVersion nella finestra di dialogo delle proprietà del progetto](../integration-services/media/targetserverversion2.png "Proprietà TargetServerVersion nella finestra di dialogo delle proprietà del progetto")  
  
 È possibile creare, gestire ed eseguire pacchetti destinati a SQL Server 2016, SQL Server 2014 o SQL Server 2012.  
  
  
