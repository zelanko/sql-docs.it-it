---
title: Distribuire i pacchetti usando l'utilità di distribuzione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], installing
- installing packages
- dependencies [Integration Services]
- deploying packages [Integration Services], installing
ms.assetid: eaf4b56e-2023-4d17-971c-703031da758c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 73b71e83f3b0f0f895b2cc5b8fd3495fb4893a32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059616"
---
# <a name="deploy-packages-by-using-the-deployment-utility"></a>Distribuzione di pacchetti con l'utilità di distribuzione
  Se è stata compilata un'utilità di distribuzione per l'installazione di pacchetti di un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in un computer diverso da quello in cui l'utilità è stata compilata, è prima necessario copiare la cartella di distribuzione nel computer di destinazione.  
  
 Il percorso di tale cartella è specificato nella proprietà DeploymentOutputPath del progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per il quale è stata creata l'utilità di distribuzione. Il percorso predefinito è bin\Deployment relativo al progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Per altre informazioni, vedere [Creazione di un'utilità di distribuzione](../../2014/integration-services/create-a-deployment-utility.md).  
  
 Per installare i pacchetti è possibile utilizzare Installazione guidata pacchetti, che può essere avviata facendo doppio clic sul file dell'utilità di distribuzione, dopo aver copiato la cartella di distribuzione sul server. Il file è denominato \<nome progetto>.SSISDeploymentManifest ed è disponibile nella cartella di distribuzione nel computer di destinazione.  
  
> [!NOTE]  
>  In base alla versione del pacchetto che si distribuisce, è possibile rilevare un errore se versioni diverse di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sono state installate in modalità side-by-side. Questo errore può verificarsi perché l'estensione del file SSISDeploymentManifest è uguale per tutte le versioni di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Se si fa doppio clic sul file viene chiamato il programma di installazione (dtsinstall.exe) della versione di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]installata più di recente, che potrebbe non corrispondere a quella del file dell'utilità di distribuzione. Per evitare tale problema, eseguire la versione corretta di dtsinstall.exe dalla riga di comando e specificare il percorso del file dell'utilità di distribuzione.  
  
 L'Installazione guidata pacchetti consente di eseguire in modo semplificato i passaggi necessari per l'installazione di pacchetti nel file system o in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. È possibile configurare l'installazione nei modi seguenti:  
  
-   Specificando il tipo di posizione e la posizione per l'installazione dei pacchetti.  
  
-   Specificando la posizione per l'installazione delle dipendenze dei pacchetti.  
  
-   Convalidando i pacchetti dopo l'installazione nel server di destinazione.  
  
 Le dipendenze basate su file per i pacchetti vengono sempre installate nel file system. Se si installa un pacchetto nel file system, le dipendenze vengono installate nella stessa cartella specificata per il pacchetto. Se si installa un pacchetto in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], è possibile specificare la cartella in cui archiviare le dipendenze basate su file.  
  
 Se il pacchetto include configurazioni che si desidera modificare per l'utilizzo nel computer di destinazione, è possibile aggiornare i valori delle proprietà tramite la procedura guidata.  
  
 Oltre a installare pacchetti eseguendo l'Installazione guidata pacchetti, è possibile copiare e spostare pacchetti tramite l'utilità del prompt dei comandi **dtutil** . Per altre informazioni, vedere [dtutil Utility](dtutil-utility.md).  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>Per distribuire pacchetti in un'istanza di SQL Server  
  
1.  Aprire la cartella di distribuzione del computer di destinazione.  
  
2.  Fare doppio clic sul file di manifesto \<nome progetto>.SSISDeploymentManifest per avviare l'Installazione guidata pacchetti.  
  
3.  Nella pagina **Distribuzione pacchetti SSIS** selezionare l'opzione **Distribuzione di SQL Server** .  
  
4.  Facoltativamente, selezionare **Convalida pacchetti dopo l'installazione** per convalidare i pacchetti dopo che sono stati installati nel server di destinazione.  
  
5.  Nella pagina **Impostazione istanza di SQL Server di destinazione** specificare l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in cui installare i pacchetti e selezionare una modalità di autenticazione. Se si seleziona l'Autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , è necessario specificare un nome utente e una password.  
  
6.  Nella pagina **Selezione cartella di installazione** specificare la cartella del file system in cui installare i pacchetti e le relative dipendenze.  
  
7.  Se il pacchetto include configurazioni, è possibile modificarle aggiornando i valori dell'elenco **Valore** nella pagina Configurazione pacchetti.  
  
8.  Se è stata impostata la convalida dei pacchetti dopo l'installazione, esaminare i risultati della convalida dei pacchetti distribuiti.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione del pacchetto &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
