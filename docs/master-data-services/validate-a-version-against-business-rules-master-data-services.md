---
title: Convalidare una versione rispetto a regole business
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- validating versions [Master Data Services]
- validating versions [Master Data Services], about validating versions
- versions [Master Data Services], validating
- business rules [Master Data Services], applying to all members
ms.assetid: 5aee7901-6d05-41d4-8bbb-c6f26791d1df
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2995a02e738b2c185edff26ee0d6a395df14f59f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73727832"
---
# <a name="validate-a-version-against-business-rules-master-data-services"></a>Convalidare una versione rispetto a regole business (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]convalidare una versione per applicare regole di business a tutti i membri nella versione del modello.  
  
 In questa procedura viene illustrato come usare l'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] per convalidare i dati. Se si dispone dell'autorizzazione nel database MDS, è possibile utilizzare una stored procedure. Per altre informazioni, vedere [Stored procedure di convalida &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md).  
  
> [!NOTE]  
>  Tutti i membri devono superare la convalida prima che possa essere eseguito il commit di una versione.  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario avere l'autorizzazione per accedere all'area funzionale **Gestione versioni** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Lo stato della versione deve essere **Aperto** o **Bloccato**.  
  
-   Nella pagina **Convalida versioni** devono essere presenti membri con uno stato diverso da **Convalida completata**.  
  
### <a name="to-validate-a-version"></a>Per convalidare una versione  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Gestione versioni**.  
  
2.  Nella pagina **Gestisci versioni** scegliere **Convalida versione**dalla barra dei menu.  
  
3.  Nella pagina **Convalida versioni** selezionare il modello e la versione che si desidera convalidare.  
  
4.  Fare clic su **Convalida**.  
  
5.  Nella finestra di dialogo di conferma fare clic su **OK**.  
  
    > [!NOTE]  
    >  Quando non è più visualizzato l'indicatore di stato, la versione ha terminato la convalida.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   [Bloccare una versione &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Stati di convalida &#40;Master Data Services&#41;](../master-data-services/validation-statuses-master-data-services.md)   
 [&#40;della stored procedure di convalida Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [Versioni &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Regole business &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Convalidare membri specifici rispetto a regole business &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
  
