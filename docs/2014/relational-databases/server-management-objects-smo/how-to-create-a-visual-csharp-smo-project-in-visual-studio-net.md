---
title: Creare un progetto Visual c# SMO in Visual Studio .NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 371da8231138fb43e9b001808b9fb88ad09543b5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52799507"
---
# <a name="create-a-visual-c-smo-project-in-visual-studio-net"></a>Creare un progetto SMO per Visual C# in Visual Studio .NET
  In questa sezione viene descritto come compilare un'applicazione console SMO semplice.  
  
 In questo esempio vengono importati spazi dei nomi affinché il programma faccia riferimento ai tipi SMO. L'importazione dello spazio dei nomi `Agent` è facoltativa. Utilizzarla quando si scrive un programma che utilizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Lo spazio dei nomi `Common` è necessario per stabilire una connessione protetta all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Lo spazio dei nomi `SqlClient` viene utilizzato per elaborare gli errori di eccezione SQL.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Creazione di un progetto Visual C# SMO in Visual Studio.NET  
  
1.  Avviare [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] (o [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)]).  
  
2.  Scegliere **Nuovo progetto** dal menu **File**. Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nella **tipi di progetto** finestra di dialogo **Visual c#**, quindi selezionare **Windows**. Nel [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] riquadro Modelli installati, selezionare **applicazione di Windows**.  
  
4.  (Facoltativo) Nel **nome** digitare il nome della nuova applicazione  
  
5.  Selezionare il tipo di applicazione di Visual C#. Per gli esempi che seguono selezionare **applicazione Console**.  
  
6.  Scegliere **Aggiungi riferimento** dal menu **Progetto**. Verrà visualizzata la finestra di dialogo **Aggiungi riferimento**.  
  
7.  Fare clic su **esplorare**, individuare gli assembly SMO nella [!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)] cartella e quindi selezionare i file seguenti. che costituiscono i file minimi necessari per compilare un'applicazione SMO:  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
    > [!NOTE]  
    >  Per selezionare più file, utilizzare il tasto `Ctrl`.  
  
8.  Aggiungere eventuali assembly SMO necessari. Se ad esempio si esegue la programmazione specifica di [!INCLUDE[ssSB](../../includes/sssb-md.md)], aggiungere gli assembly seguenti:  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. Fare clic su **Apri**.  
  
10. Nel **View** menu, fare clic su **codice**. oppure selezionare il Program1.cs [Progettazione] Windows e fare doppio clic sul windows form per visualizzare la finestra del codice.  
  
11. Nel codice prima dell'istruzione dello spazio dei nomi, digitare le istruzioni `using` seguenti per qualificare i tipi nello spazio dei nomi SMO:  
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
12. SMO dispone di vari spazi dei nomi in Microsoft.SqlServer.Management.Smo, ad esempio Microsoft.SqlServer.Management.Smo.Agent. Aggiungere questi spazi dei nomi poiché sono necessari.  
  
13. A questo punto è possibile aggiungere il codice SMO.  
  
  
