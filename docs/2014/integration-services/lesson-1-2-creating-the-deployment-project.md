---
title: 'Passaggio 2: Creazione del progetto di distribuzione | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6f5b0cc2c86ef483a7e2b2c0f5dccba21383641f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62891848"
---
# <a name="step-2-creating-the-deployment-project"></a>Passaggio 2: Creazione del progetto di distribuzione
  In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]l'unità distribuibile è rappresentata da un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Per poter distribuire i pacchetti, è necessario creare un nuovo progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e aggiungervi tutti i pacchetti e gli eventuali file ausiliari che di desidera distribuire unitamente ai pacchetti.  
  
### <a name="to-create-the-integration-services-project"></a>Per creare il progetto di Integration Services  
  
1.  Fare clic su **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server**e quindi fare clic su **SQL Server Data Tools**.  
  
2.  Dal menu **File** scegliere **Nuovo**e quindi **Progetto** per creare un nuovo progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
3.  Nella finestra di dialogo **Nuovo progetto** selezionare **Progetto di Integration Services** nel riquadro **Modelli** .  
  
4.  Nella casella **Nome** modificare il nome predefinito in **Deployment Tutorial**. Facoltativamente, deselezionare la casella di controllo **Crea directory per soluzione** .  
  
5.  Accettare il percorso predefinito o fare clic su **Sfoglia** per trovare la cartella che si vuole usare.  
  
6.  Nella finestra di dialogo **Percorso progetto** fare clic sulla cartella e scegliere **Apri**.  
  
7.  Fare clic su **OK**.  
  
8.  Per impostazione predefinita, viene creato e aggiunto al progetto un pacchetto vuoto denominato Package.dtsx. Questo pacchetto non verrà tuttavia utilizzato. Al progetto verranno infatti aggiunti i pacchetti esistenti. Poiché nella distribuzione vengono inclusi tutti i pacchetti del progetto, è consigliabile eliminare Package.dtsx. A tale scopo, fare clic con il pulsante destro del mouse su di esso e scegliere **Elimina**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 3: Aggiunta di pacchetti e altri file](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
![Icona di Integration Services (piccola)](media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Progetti di Integration Services &#40;SSIS&#41;](integration-services-ssis-projects-and-solutions.md)  
  
  
