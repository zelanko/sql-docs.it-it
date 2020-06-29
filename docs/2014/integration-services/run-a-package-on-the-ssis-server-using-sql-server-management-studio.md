---
title: Eseguire un pacchetto nel server SSIS utilizzando SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 56dc1bf8-99d4-41dc-bdc4-f64f1ccfd688
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d17009988dea54621d4fd7ef542cf452bfe95c6e
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422958"
---
# <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>Eseguire un pacchetto sul server SSIS mediante SQL Server Management Studio
  Dopo aver distribuito il progetto nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , è possibile eseguire il pacchetto nel server.  
  
 È possibile utilizzare i report relativi alle operazioni per visualizzare informazioni sui pacchetti eseguiti, o che sono attualmente in esecuzione, nel server. Per altre informazioni, vedere [report per il server Integration Services](../../2014/integration-services/reports-for-the-integration-services-server.md).  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>Per eseguire un pacchetto nel server mediante SQL Server Management Studio  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e connettersi all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in cui è contenuto il catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
2.  In Esplora oggetti espandere il nodo **Cataloghi di Integration Services** , il nodo **SSISDB** e navigare al pacchetto contenuto nel progetto distribuito.  
  
3.  Fare clic con il pulsante destro del mouse sul nome del pacchetto e selezionare **Esegui**.  
  
4.  Configurare l'esecuzione del pacchetto utilizzando le impostazioni delle schede **parametri**, **gestioni connessioni**e **Avanzate** nella finestra di dialogo **Esegui pacchetto** .  
  
5.  Fare clic su **OK** per eseguire il pacchetto.  
  
     -oppure-  
  
     Utilizzare le stored procedure per eseguire il pacchetto. Fare clic su **Script** per generare l'istruzione Transact-SQL tramite cui viene creata e avviata un'istanza dell'esecuzione. Nell'istruzione è inclusa una chiamata alle stored procedure catalog.create_execution, catalog.set_execution_parameter_value e catalog.start_execution. Per altre informazioni su queste stored procedure, vedere [catalog.create_execution &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database), [catalog.set_execution_parameter_value &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) e [catalog.start_execution &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database).  
  
  
