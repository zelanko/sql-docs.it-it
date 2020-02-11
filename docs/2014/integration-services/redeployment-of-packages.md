---
title: Ridistribuzione di pacchetti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- redeploying packages [Integration Services]
- deploying packages [Integration Services], redeploying
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 14edf3c34278ce89686a390c5b69662753ae653d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056476"
---
# <a name="redeployment-of-packages"></a>Ridistribuzione di pacchetti
  Dopo la distribuzione di un progetto, potrebbe essere necessario aggiornare o estendere la funzionalità dei pacchetti e ridistribuire quindi il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contenente i pacchetti aggiornati. Durante il processo di ridistribuzione di pacchetti, è consigliabile analizzare le proprietà di configurazione incluse nell'utilità di distribuzione. Potrebbe ad esempio essere utile non consentire alcuna modifica di configurazione dopo la ridistribuzione del pacchetto.  
  
## <a name="process-for-redeployment"></a>Ridistribuzione  
 Dopo avere completato l'aggiornamento di pacchetti, è necessario ricompilare il progetto, copiare la cartella di distribuzione nel computer di destinazione e rieseguire l'Installazione guidata pacchetti.  
  
 Se si aggiornano solo alcuni pacchetti di un progetto, potrebbe risultare utile ridistribuire solo i pacchetti aggiornati anziché l'intero progetto. Per distribuire solo alcuni pacchetti, è possibile creare un nuovo progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , aggiungervi i pacchetti aggiornati e quindi compilare e distribuire il progetto. Quando il pacchetto viene aggiunto a un altro progetto, le configurazioni di pacchetto vengono copiate automaticamente insieme al pacchetto.  
  
## <a name="related-tasks"></a>Attività correlate  
 [Distribuzione di pacchetti con l'utilità di distribuzione](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)  
  
  
