---
description: Applicare e rifiutare un insieme di modifiche (Master Data Services)
title: Approvare o rifiutare un insieme di modifiche
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 45bd01f9-ae15-4fc5-a2ba-eee565a26ef8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 42b3b6ae849313a00111ceda1fb19eda334c0278
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456814"
---
# <a name="approve-or-reject-a-changeset-master-data-services"></a>Applicare e rifiutare un insieme di modifiche (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Un insieme di modifiche è una raccolta delle modifiche in sospeso relative ai dati master. Se le modifiche all'entità richiedono l'approvazione dell'amministratore e un insieme di modifiche viene inviato per l'approvazione, è possibile esaminare e quindi approvare o rifiutare l'insieme di modifiche.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Esplora** . Per altre informazioni, vedere [Autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   È necessario avere autorizzazioni di amministratore per l'entità.  
  
-   Per le modifiche all'entità è necessario richiedere l'approvazione dell'amministratore.  
  
-   Se lo stato dell'insieme di modifiche è in sospeso, è possibile esaminare e quindi approvare o rifiutare l'insieme di modifiche.  
  
-   Gli utenti non possono approvare le proprie modifiche. Gli amministratori dell'entità devono assegnare un amministratore secondario per approvare il proprio insieme di modifiche.  
  
## <a name="to-approve-or-reject-a-changeset"></a>Per approvare o rifiutare un insieme di modifiche  
  
1.  Nella [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Home page selezionare il modello e la versione, quindi fare clic su **Esplora**.  
  
2.  Scegliere un'entità nel menu **Entità** .  
  
3.  Nel riquadro di destra selezionare **Insiemi di modifiche** e fare doppio clic sull'insieme di modifiche da approvare o rifiutare.  
  
4.  Fare clic su **Applica** per applicare l'insieme di modifiche e rivedere le modifiche in sospeso.  
  
5.  Fare clic su **Rifiuta** per rifiutare l'insieme di modifiche e inviarlo di nuovo al proprietario.  
  
6.  Fare clic su **Approva** per approvare l'insieme di modifiche. Il commit dell'insieme di modifiche viene eseguito automaticamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un insieme di modifiche &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Applicare e aggiornare un insieme di modifiche &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Eseguire il commit o inviare un insieme di modifiche &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
  
