---
title: "Passaggio 1: Compilazione dell'utilità di distribuzione | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1ff4dcff-89b3-4b99-a725-5f7963e98abf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b788f82fc28ee39e7d65ae484da49313eea7c610
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767583"
---
# <a name="step-1-building-the-deployment-utility"></a>Passaggio 1: Compilazione dell'utilità di distribuzione
  In questa attività verrà configurata e compilata un'utilità di distribuzione per il progetto Deployment Tutorial.  
  
 Per poter compilare l'utilità di distribuzione, è necessario modificare le proprietà del progetto Deployment Tutorial. Verrà usata la finestra di dialogo **Deployment Tutorial Property Pages** (Pagine delle proprietà di Deployment Tutorial) per configurare queste proprietà. In questa finestra di dialogo è necessario abilitare la funzionalità di aggiornamento delle configurazioni durante la distribuzione e specificare il processo di compilazione che consente di generare l'utilità di distribuzione. Al termine dell'impostazione delle proprietà, il progetto verrà compilato.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] include un set di finestre che consentono di eseguire il debug dei pacchetti. È possibile visualizzare messaggi di errore, avviso e informativi, tenere traccia dello stato dei pacchetti in fase di esecuzione oppure visualizzare lo stato e i risultati dei processi di compilazione. Per questa lezione, si utilizzerà la finestra Output per visualizzare lo stato e i risultati della compilazione dell'utilità di distribuzione.  
  
### <a name="to-set-the-deployment-utility-properties"></a>Per impostare le proprietà dell'utilità di distribuzione  
  
1.  Se [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] non è già aperto, fare clic sul pulsante **Start**, scegliere **Programmi**, **Microsoft SQL Server**selezionare **Business Intelligence Development Studio**.  
  
2.  Scegliere **Apri** dal menu **File**, fare clic su **Progetto/Soluzione**, selezionare la cartella **Deployment Tutorial** , fare clic su **Apri**e fare doppio clic su **Deployment Tutorial.sln**.  
  
3.  In Esplora soluzioni fare clic con il pulsante destro del mouse su Deployment Tutorial e scegliere **Proprietà**.  
  
4.  Nella finestra di dialogo **Deployment Tutorial Property Pages** (Pagine delle proprietà di Deployment Tutorial) espandere le proprietà di configurazione e fare clic su Utilità di distribuzione.  
  
5.  Nel riquadro destro della finestra di dialogo **pagine delle proprietà di Deployment Tutorial** verificare che `AllowConfigurationChanges` sia impostato su `true`, impostare `CreateDeploymentUtility` su `true`e, facoltativamente, aggiornare il valore predefinito `DeploymentOutputPath`di.  
  
6.  Fare clic su **OK**.  
  
### <a name="to-build-the-deployment-utility"></a>Per compilare l'utilità di distribuzione  
  
1.  In Esplora soluzioni fare clic su **Deployment Tutorial**.  
  
2.  Scegliere **Output** dal menu **Visualizza**. Per impostazione predefinita, la finestra Output si trova nell'angolo inferiore sinistro di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
3.  Scegliere **Build Deployment Tutorial** (Compila Deployment Tutorial) dal menu **Compila**.  
  
4.  Nella finestra Output verificare le informazioni seguenti:  
  
     Compilazione avviata - Progetto SQL Integration Services: Incrementale ...  
  
     Creazione dell'utilità di distribuzione in corso...  
  
     Utilità di distribuzione creata.  
  
     Compilazione completata -- 0 errori, 0 avvisi  
  
     ========== Compilazione: 0 completate, 0 non riuscite, 1 aggiornate, 0 ignorate ==========  
  
5.  Scegliere **Esci** dal menu **File**. Se richiesto per salvare le modifiche agli elementi di Deployment Tutorial, fare clic su **Sì**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 2: Verifica del pacchetto di distribuzione](../integration-services/lesson-2-2-verifying-the-deployment-bundle.md)  
  
![Integration Services icona (piccola)](media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un'utilità di distribuzione](../../2014/integration-services/create-a-deployment-utility.md)  
  
  
