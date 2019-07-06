---
title: Creare un progetto Visual c# SMO in Visual Studio .NET | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7e67f69a6e1ce5ce18eb265fdc86eba8e8fcd0bc
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67585093"
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>Come creare un progetto SMO Visual C# in Visual Studio .NET
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  In questa sezione viene descritto come compilare un'applicazione console SMO semplice.  
  
 In questo esempio vengono importati spazi dei nomi affinché il programma faccia riferimento ai tipi SMO. L'importazione del **agente** dello spazio dei nomi è facoltativo. Utilizzarla quando si scrive un programma che utilizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Il **comuni** dello spazio dei nomi è necessario per stabilire una connessione sicura all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il **SqlClient** dello spazio dei nomi viene usato per elaborare gli errori di eccezione SQL.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Creazione di un progetto Visual C# SMO in Visual Studio.NET  
  
1. Start Visual Studio
  
2. Nel **File** menu, fare clic su **New** e quindi **progetto**.  Verrà visualizzata la finestra di dialogo **Nuovo progetto** .   
  
3. Nel [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Installed** riquadro, passare alla **modelli**\\**Visual c#** \\**Windows** e selezionare **applicazione Console**.  
  
4. (Facoltativo) Nel **nome** testo, digitare il nome della nuova applicazione.  

5. Fare clic su **OK** per caricare il modello di applicazione console.  

6. Seguire le istruzioni sullo [installazione di SMO](installing-smo.md) per installare il pacchetto per il progetto a cui fare riferimento.
  
7. Scegliere **Codice** dal menu **Visualizza**.
    
8. Nel codice, prima dell'istruzione dello spazio dei nomi, digitare quanto segue **usando** istruzioni per qualificare i tipi nello spazio dei nomi SMO:
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO dispone di vari spazi dei nomi in Microsoft.SqlServer.Management.Smo, ad esempio Microsoft.SqlServer.Management.Smo.Agent. Aggiungere questi spazi dei nomi poiché sono necessari.  
  
16. A questo punto è possibile aggiungere il codice SMO.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

