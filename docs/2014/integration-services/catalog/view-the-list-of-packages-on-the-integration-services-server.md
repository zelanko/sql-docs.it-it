---
title: Visualizzare l'elenco di pacchetti nel server Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 67a992d1-7524-4f4b-b3d8-ebd9e5ea82a8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 47b30f9ea0b2abae73f9260b873b7c8436c423eb
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439008"
---
# <a name="view-the-list-of-packages-on-the-integration-services-server"></a>Visualizzazione dell'elenco di pacchetti nel server Integration Services
  È possibile visualizzare l'elenco di pacchetti archiviati nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in due modi diversi.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] accesso  
 Per visualizzare l'elenco di pacchetti archiviati nel server, eseguire una query sulla vista [catalog.packages &#40;SSISDB Database&#41;](/sql/integration-services/system-views/catalog-packages-ssisdb-database).  
  
 In [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
 Per visualizzare i pacchetti archiviati nel server tramite Esplora oggetti in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], attenersi alla procedura riportata di seguito.  
  
### <a name="to-view-packages-using-ssmanstudiofull"></a>Per visualizzare i pacchetti utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
  
1.  In [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]connettersi al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . cioè connettersi all'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in cui è ospitato il database di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  In Esplora oggetti espandere l'albero per visualizzare il nodo dei **cataloghi di Integration Services** .  
  
3.  Espandere il nodo **Cataloghi di Integration Services** per visualizzare il nodo **SSISDB** .  
  
4.  Espandere il nodo **SSISDB** per visualizzare un elenco di una o più cartelle. Nella cartella **Progetti** di ogni cartella sono contenuti uno o più progetti e nella cartella **Pacchetti** di ogni progetto sono contenuti uno o più pacchetti.  
  
  
