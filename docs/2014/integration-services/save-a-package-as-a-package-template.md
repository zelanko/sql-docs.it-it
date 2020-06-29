---
title: Salvare un pacchetto come modello di pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- reusing packages
- templates [Integration Services]
ms.assetid: efe66cec-3933-4f6e-8d35-fe3d300de66c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: daf617a088dd781cf40bf85bedbd2e5b52ad7e5a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422398"
---
# <a name="save-a-package-as-a-package-template"></a>Salvataggio di un pacchetto come modello di pacchetto
  In questo argomento viene descritta la procedura per designare e utilizzare pacchetti personalizzati come modelli per la creazione di nuovi pacchetti di Integration Services in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Per impostazione predefinita in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] viene utilizzato un modello di pacchetto che crea un pacchetto vuoto quando si aggiunge un nuovo pacchetto a un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Non è possibile sostituire tale modello predefinito, ma è possibile aggiungere nuovi modelli.  
  
 È possibile designare più pacchetti da utilizzare come modelli. Prima di implementare pacchetti personalizzati come modelli è necessario creare i pacchetti.  
  
 Quando si utilizzano pacchetti personalizzati come modelli per la creazione di nuovi pacchetti, questi ultimi hanno nome e GUID uguali a quelli del modello. Per distinguere i vari pacchetti è necessario modificare il valore della proprietà `Name` e generare un nuovo GUID per la proprietà `ID`. Per altre informazioni, vedere [Creare pacchetti in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md) e [Impostazione delle proprietà di un pacchetto](set-package-properties.md).  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>Per designare un pacchetto personalizzato come modello di pacchetto  
  
1.  Individuare nel file system il pacchetto che si desidera utilizzare come modello.  
  
2.  Copiare il pacchetto nella cartella DataTransformationItems, che per impostazione predefinita si trova in C:\Programmi\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
3.  Ripetere i passaggi 1 e 2 per ogni pacchetto che si desidera utilizzare come modello.  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>Per utilizzare un pacchetto personalizzato come modello di pacchetto  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in cui si desidera creare un pacchetto.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, scegliere **Aggiungi** e quindi **Nuovo elemento**.  
  
3.  Nella finestra di dialogo **Aggiungi nuovo \<project name> elemento-** fare clic sul pacchetto che si desidera utilizzare come modello.  
  
     Nell'elenco dei modelli è incluso il modello di pacchetto predefinito Nuovo pacchetto SSIS. I modelli che è possibile utilizzare come modelli di pacchetto sono identificati dall'icona di pacchetto.  
  
4.  Scegliere **Aggiungi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare pacchetti in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md)   
 [Pacchetti di Integration Services &#40;SSIS&#41;](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
