---
title: 'Passaggio 1: Creazione di un nuovo progetto di Integration Services | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 18dbf43f2305e9991d6fe37615f572e1dc464fda
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529523"
---
# <a name="lesson-1-1---creating-a-new-integration-services-project"></a>Lezione 1-1 - Creazione di un nuovo progetto di Integration Services
Il primo passaggio nella creazione di un pacchetto in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] consiste nel creare un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Questo progetto include i modelli per gli oggetti, ovvero origini dati, viste origini dati e pacchetti usati in una soluzione di trasformazione dei dati.  
  
I pacchetti che verranno creati in questa esercitazione relativa a [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] interpretano i valori dei dati dipendenti dalle impostazioni locali. Se il computer non è configurato per l'utilizzo dell'opzione Inglese (Stati Uniti) per le impostazioni locali, è necessario impostare proprietà aggiuntive nel pacchetto. I pacchetti utilizzati nelle lezioni 2-5 vengono copiati dal pacchetto creato nella lezione 1 e non è necessario aggiornare le proprietà dipendenti dalle impostazioni locali nei pacchetti copiati.  
  
> [!NOTE]  
> Per questa esercitazione è richiesto Microsoft SQL Server Data Tools.  
>   
> Per altre informazioni sull'installazione di SQL Server Data Tools, vedere [Scaricare SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027).  
  
### <a name="to-create-a-new-integration-services-project"></a>Per creare un nuovo progetto di Integration Services  
  
1.  Fare clic sul menu **Start** , scegliere **Programmi**, **Microsoft SQL Server**, quindi **SQL Server Data Tools**.  
  
2.  Scegliere **Nuovo** dal menu **File**e fare clic su **Progetto** per creare un nuovo progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
3.  Nella finestra di dialogo **Nuovo progetto** espandere il nodo **Business Intelligence** in **Modelli installati**e selezionare **Progetto di Integration Services** nel riquadro **Modelli** .  
  
4.  Nella casella **Nome** impostare il nome predefinito su **SSIS Tutorial**. Facoltativamente, deselezionare la casella di controllo **Crea directory per soluzione** .  
  
5.  Accettare il percorso predefinito o fare clic su **Sfoglia** per individuare la cartella che si vuole usare. Nella finestra di dialogo **Percorso progetto** fare clic sulla cartella, quindi scegliere **Seleziona cartella**.  
  
6.  Fare clic su **OK**.  
  
    Per impostazione predefinita viene creato e aggiunto al progetto un pacchetto vuoto in Pacchetti SSIS, denominato **Package.dtsx**.  
  
7.  Nella barra degli strumenti **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Package.dtsx**, fare clic su **Rinomina**e rinominare il pacchetto predefinito in **Lesson 1.dtsx**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
[Passaggio 2: Aggiunta e configurazione di una gestione connessione file flat](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
