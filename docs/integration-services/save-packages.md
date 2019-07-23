---
title: Salvare pacchetti | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.savecopyas.f1
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b2184475ac3da6629a70b5013277686636a6fc8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897072"
---
# <a name="save-packages"></a>Salvataggio di pacchetti

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] è possibile usare Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] per compilare i pacchetti e quindi salvarli nel file system come file XML, con estensione dtsx. È inoltre possibile salvare copie del file XML di un pacchetto nel database msdb in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o nell'archivio pacchetti. L'archivio pacchetti è costituito dalle cartelle del percorso del file system gestito dal servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Se si salva un pacchetto nel file system, successivamente sarà possibile utilizzare il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per importarlo in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o nell'archivio pacchetti. Per altre informazioni, vedere [Servizio Integration Services &#40;servizio SSIS&#41;](../integration-services/service/integration-services-service-ssis-service.md).  
  
 È inoltre possibile usare l'utilità della riga di comando **dtutil**per copiare un pacchetto dal file system al database msdb e viceversa. Per altre informazioni, vedere [dtutil Utility](../integration-services/dtutil-utility.md).  
## <a name="save-a-package-to-the-file-system"></a>Salvataggio di un pacchetto nel file system  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto da salvare in un file.  
  
2.  In Esplora soluzioni selezionare il pacchetto che si desidera salvare.  
  
3.  Scegliere **Salva elementi selezionati** dal menu **File**.  
  
    > [!NOTE]  
    >  È possibile verificare il percorso e il nome del file in cui è stato salvato il pacchetto nella finestra Proprietà.  

## <a name="save-a-copy-of-a-package"></a>Salvataggio di una copia di un pacchetto
  Questa sezione descrive come salvare una copia di un pacchetto nel file system, nell'archivio pacchetti o nel database **msdb** in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando si specifica il percorso di salvataggio della copia del pacchetto, è inoltre possibile modificarne il nome.  
  
 L'archivio pacchetti può includere sia il database **msdb** che le cartelle del file system, solo **msdb**, oppure solo le cartelle del file system. In **msdb**i pacchetti vengono salvati nella tabella **sysssispackages** . Tale tabella include una colonna **folderid** che identifica la cartella logica alla quale il pacchetto appartiene. Le cartelle logiche consentono di raggruppare i pacchetti salvati in **msdb** , nello stesso modo in cui le cartelle del file system consentono di raggruppare i pacchetti salvati nel file system. Le righe della tabella **sysssispackagefolders** di **msdb** definiscono le cartelle.  
  
 Se **msdb** non è definito come parte dell'archivio pacchetti, è possibile continuare ad associare i pacchetti a cartelle logiche esistenti se si seleziona SQL Server nell'opzione **Percorso pacchetto** .  
  
> [!NOTE]  
>  Affinché sia possibile salvarne una copia, il pacchetto deve essere aperto in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
### <a name="to-save-a-copy-of-a-package"></a>Per salvare una copia di un pacchetto  
  
1.  In Esplora soluzioni fare doppio clic sul pacchetto di cui si desidera salvare una copia.  
  
2.  Dal menu **File** scegliere **Salva copia di \<file di pacchetto> con nome**.  
  
3.  Nella finestra di dialogo **Salva copia del pacchetto** selezionare la posizione di un pacchetto dall'elenco **Posizione pacchetto**. Sono disponibili le opzioni seguenti:  
    -   SQL Server
    -   File system 
    -   Archivio pacchetti SSIS 
  
4.  Se la posizione è **SQL Server** o **Archivio pacchetti SSIS**, specificare il nome di un server.  
  
5.  Se si esegue il salvataggio in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], specificare il tipo di autenticazione e, se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , specificare un nome utente e una password.  
  
6.  Per specificare il percorso del pacchetto, digitarlo oppure fare clic sul pulsante Sfoglia **(...)** per specificare il percorso del pacchetto. Il nome predefinito del pacchetto è Pacchetto. In alternativa, modificare il nome del pacchetto in base alle proprie esigenze.  
  
     Se per l'opzione **Percorso pacchetto** si seleziona **SQL Server** , il percorso del pacchetto sarà composto dalle cartelle logiche di **msdb** più il nome del pacchetto. Ad esempio, se il pacchetto DownloadMonthlyData è associato alla cartella Finance della cartella MSDB (il nome predefinito della cartella logica radice di **msdb**), il percorso del pacchetto denominato DownloadMonthlyData sarà MSDB/Finance/DownloadMonthlyData.  
  
     Se per l'opzione **Percorso pacchetto** si seleziona **Archivio pacchetti SSIS** , il percorso del pacchetto corrisponderà alla cartella gestita dal servizio Integration Services. Ad esempio, se il pacchetto UpdateDeductions si trova nella cartella HumanResources all'interno della cartella del file system gestita dal servizio, il percorso del pacchetto sarà /File System/HumanResources/UpdateDeductions. Analogamente, se il pacchetto PostResumes è associato alla cartella HumanResources della cartella MSDB, il percorso del pacchetto sarà MSDB/HumanResources/PostResumes.  
  
     Se per l'opzione **Percorso pacchetto** si seleziona **File system** , il percorso del pacchetto corrisponderà alla posizione nel file system più il nome del file. Ad esempio, se il nome del pacchetto è UpdateDemographics, il relativo percorso sarà C:\HumanResources\Quarterly\UpdateDemographics.dtsx.  
  
7.  Controllare il livello di protezione del pacchetto.  
  
8.  Facoltativamente, per modificare il livello di protezione fare clic sul pulsante Sfoglia **(...)** accanto alla casella **Livello di protezione**.  
  
    -   Nella finestra di dialogo **Livello di protezione pacchetto** selezionare un livello di protezione diverso.  
  
    -   Fare clic su **OK**.  
  
9. Fare clic su **OK**.  

## <a name="save-a-package-as-a-package-template"></a>Salvare un pacchetto come modello di pacchetto
 Questa sezione descrive come designare e usare pacchetti personalizzati come modelli per la creazione di nuovi pacchetti di Integration Services in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Per impostazione predefinita in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] viene utilizzato un modello di pacchetto che crea un pacchetto vuoto quando si aggiunge un nuovo pacchetto a un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Non è possibile sostituire tale modello predefinito, ma è possibile aggiungere nuovi modelli.  
  
 È possibile designare più pacchetti da utilizzare come modelli. Prima di implementare pacchetti personalizzati come modelli è necessario creare i pacchetti.  
  
 Quando si utilizzano pacchetti personalizzati come modelli per la creazione di nuovi pacchetti, questi ultimi hanno nome e GUID uguali a quelli del modello. Per distinguere i vari pacchetti è necessario modificare il valore della proprietà **Name** e generare un nuovo GUID per la proprietà **ID** . Per altre informazioni, vedere [Creare pacchetti in SQL Server Data Tools](../integration-services/create-packages-in-sql-server-data-tools.md) e [Impostazione delle proprietà di un pacchetto](../integration-services/set-package-properties.md).  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>Per designare un pacchetto personalizzato come modello di pacchetto  
  
1.  Individuare nel file system il pacchetto che si desidera utilizzare come modello.  
  
2.  Copiare il pacchetto nella cartella DataTransformationItems, che per impostazione predefinita si trova in C:\Programmi\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
3.  Ripetere i passaggi 1 e 2 per ogni pacchetto che si desidera utilizzare come modello.  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>Per utilizzare un pacchetto personalizzato come modello di pacchetto  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in cui si desidera creare un pacchetto.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, scegliere **Aggiungi** e quindi **Nuovo elemento**.  
  
3.  Nella finestra di dialogo **Aggiungi nuovo elemento -\<nome progetto>** fare clic sul pacchetto che si vuole usare come modello.  
  
     Nell'elenco dei modelli è incluso il modello di pacchetto predefinito Nuovo pacchetto SSIS. I modelli che è possibile utilizzare come modelli di pacchetto sono identificati dall'icona di pacchetto.  
  
4.  Scegliere **Aggiungi**.  
