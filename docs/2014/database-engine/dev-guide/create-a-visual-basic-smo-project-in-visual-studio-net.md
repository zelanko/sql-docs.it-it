---
title: Creare un progetto Visual Basic SMO in Visual Studio .NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic [SMO]
ms.assetid: d7a3892c-0f1c-4c4d-8480-b58dce3720bc
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 49eb94833d10b2e901c008092aea29eab8e4ad48
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933682"
---
# <a name="create-a-visual-basic-smo-project-in-visual-studio-net"></a>Creare un progetto SMO per Visual Basic in Visual Studio .NET
  In questa sezione viene descritto come compilare un'applicazione console SMO semplice.  
  
 In questo esempio vengono importati spazi dei nomi affinché il programma faccia riferimento ai tipi SMO. L'importazione dello spazio dei nomi `Agent` è facoltativa. Utilizzarla quando si scrive un programma che utilizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Lo spazio dei nomi `Common` è necessario per stabilire una connessione protetta all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Lo spazio dei nomi `SqlClient` viene utilizzato per elaborare gli errori di eccezione SQL.  
  
### <a name="creating-a-visual-basic-smo-project-in-visual-studionet"></a>Creazione di un progetto Visual Basic SMO in Visual Studio.NET  
  
1.  Avviare [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] (o [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)]).  
  
2.  Scegliere **Nuovo progetto** dal menu **File**. Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nella finestra di dialogo **Tipi progetto** selezionare **Visual Basic**, quindi selezionare **Windows**. Nel [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] riquadro Modelli installati selezionare **applicazione console.**  
  
4.  Opzionale Nel campo **nome** Digitare il nome della nuova applicazione.  
  
5.  Fare clic su **OK** per caricare il [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] modello applicazione console.  
  
6.  Scegliere **Aggiungi riferimento** dal menu **Progetto**. Verrà visualizzata la finestra di dialogo **Aggiungi riferimento**.  
  
7.  Fare clic su **Sfoglia**, individuare gli assembly SMO nella cartella C:\Programmi\Microsoft SQL Server\120\SDK\Assemblies e selezionare i file seguenti. che costituiscono i file minimi necessari per compilare un'applicazione SMO:  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc  
  
    > [!NOTE]  
    >  Per selezionare più file, utilizzare il tasto `Ctrl`.  
  
8.  Aggiungere eventuali assembly SMO necessari. Se ad esempio si esegue la programmazione specifica di [!INCLUDE[ssSB](../../includes/sssb-md.md)], aggiungere gli assembly seguenti:  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. Fare clic su **Apri**.  
  
10. Scegliere **codice**dal menu **Visualizza** . in alternativa, selezionare la finestra Module1. vb per visualizzare la finestra del codice.  
  
11. Nel codice, prima di qualsiasi dichiarazione, digitare le istruzioni **Imports** seguenti per qualificare i tipi nello spazio dei nomi SMO.  
  
    ```  
    Imports Microsoft.SqlServer.Management.Smo  
    Imports Microsoft.SqlServer.Management.Common  
    ```  
  
12. SMO dispone di vari spazi dei nomi in Microsoft.SqlServer.Management.Smo, ad esempio Microsoft.SqlServer.Management.Smo.Agent. Aggiungere questi spazi dei nomi poiché sono necessari.  
  
13. A questo punto è possibile aggiungere il codice SMO.  
  
  
