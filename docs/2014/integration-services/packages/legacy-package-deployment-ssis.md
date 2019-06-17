---
title: Pacchetto di distribuzione (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c912d4417842bc332262549cc604b97eaa50a44d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767091"
---
# <a name="package-deployment-ssis"></a>Distribuzione di pacchetti (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include strumenti e procedure guidate per la distribuzione di pacchetti dal computer di sviluppo al server di produzione o ad altri computer.  
  
 La procedura per la distribuzione di pacchetti prevede quattro passaggi.  
  
1.  Il primo passaggio è facoltativo e riguarda la creazione delle configurazioni dei pacchetti che aggiornano le proprietà degli elementi dei pacchetti in fase di esecuzione. Le configurazioni vengono incluse automaticamente durante la distribuzione dei pacchetti.  
  
2.  Il secondo passaggio consiste nella compilazione del progetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per creare un'utilità di distribuzione di pacchetti. L'utilità di distribuzione per il progetto contiene i pacchetti che si desidera distribuire.  
  
3.  Il terzo passaggio consiste nel copiare nel computer di destinazione la cartella di distribuzione creata in fase di compilazione del progetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
4.  Il quarto passaggio consiste nell'eseguire nel computer di destinazione l'Installazione guidata pacchetti per installare i pacchetti nel file system o in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come creare un'utilità di distribuzione, vedere [Creazione di un'utilità di distribuzione](../create-a-deployment-utility.md).  
  
 Per informazioni su come distribuire i pacchetti usando l'utilità di distribuzione, vedere [Distribuzione di pacchetti con l'utilità di distribuzione](../deploy-packages-by-using-the-deployment-utility.md).  
  
 Per informazioni su come creare le configurazioni dei pacchetti, vedere [Creazione di configurazioni dei pacchetti](../create-package-configurations.md).  
  
  
