---
title: Visualizzare l'elenco di pacchetti nel server Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 67a992d1-7524-4f4b-b3d8-ebd9e5ea82a8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 91cba98cf9937c89a41f5860d7bfe537250daffc
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922551"
---
# <a name="view-the-list-of-packages-on-the-integration-services-server"></a>Visualizzazione dell'elenco di pacchetti nel server Integration Services

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  È possibile visualizzare l'elenco di pacchetti archiviati nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in due modi diversi.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] accesso  
 Per visualizzare l'elenco di pacchetti archiviati nel server, eseguire una query sulla vista [catalog.packages &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md).  
  
 In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 Per visualizzare i pacchetti archiviati nel server tramite Esplora oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], attenersi alla procedura riportata di seguito.  
  
### <a name="to-view-packages-using-ssmanstudiofull"></a>Per visualizzare i pacchetti utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . cioè connettersi all'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in cui è ospitato il database di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  In Esplora oggetti espandere l'albero per visualizzare il nodo dei **cataloghi di Integration Services** .  
  
3.  Espandere il nodo **Cataloghi di Integration Services** per visualizzare il nodo **SSISDB** .  
  
4.  Espandere il nodo **SSISDB** per visualizzare un elenco di una o più cartelle. Nella cartella **Progetti** di ogni cartella sono contenuti uno o più progetti e nella cartella **Pacchetti** di ogni progetto sono contenuti uno o più pacchetti.  
  
  
