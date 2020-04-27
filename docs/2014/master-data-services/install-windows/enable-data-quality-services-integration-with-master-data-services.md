---
title: Abilitare l'integrazione di Data Quality Services con Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ab32938d-a80e-4106-80d4-94b2de3d67dc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5cf9a81134af8d6e90a1b869f8cc011a17a4b93a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482918"
---
# <a name="enable-data-quality-services-integration-with-master-data-services"></a>Abilitare l'integrazione di Data Quality Services con Master Data Services
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]la funzionalità di corrispondenza viene fornita da Data Quality Services (DQS). Questa funzionalità deve essere abilitata per essere utilizzata.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   È necessario che siano disponibili un database e un'applicazione Web [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .  
  
-   La funzionalità Data Quality Services e il client Data Quality devono essere installati nella stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita il database MDS. Per altre informazioni, vedere [Installare Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
### <a name="to-enable-data-quality-services-integration"></a>Per abilitare l'integrazione con Data Quality Services  
  
1.  Aprire [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  Nel riquadro sinistro fare clic su **Configurazione Web**.  
  
3.  Nella pagina **Configurazione Web** selezionare il sito Web e l'applicazione Web.  
  
4.  Nella sezione **Abilita integrazione DQS** fare clic su **Abilitare l'integrazione con Data Quality Services**.  
  
5.  Nella finestra di dialogo di conferma fare clic su **OK**.  
  
## <a name="see-also"></a>Vedi anche  
 [Corrispondenza Data Quality nel Componente aggiuntivo MDS per Excel](../microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Componente aggiuntivo Master Data Services per Microsoft Excel](../microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)   
 [Installazione di Master Data Services](install-master-data-services.md)  
  
  
