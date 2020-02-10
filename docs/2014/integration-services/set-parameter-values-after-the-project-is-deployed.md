---
title: Impostare i valori dei parametri dopo la distribuzione del progetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c9dcca4d-f1a0-45ec-b078-f4d372589baf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 910de9d388e60ae3664153e2f6cb3bb5203b289c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055782"
---
# <a name="set-parameter-values-after-the-project-is-deployed"></a>Impostazione dei valori di parametri dopo la distribuzione del progetto
  La Distribuzione guidata consente di impostare i valori dei parametri predefiniti quando si distribuisce il progetto nel catalogo. Quando il progetto si trova nel catalogo, è possibile utilizzare Transact-SQL o Esplora oggetti di SQL Server Management Studio (SSMS) per impostare i valori predefiniti del server.  
  
### <a name="to-set-server-defaults-with-ssms-object-explorer"></a>Per impostare i valori predefiniti del server con Esplora oggetti di SSMS:  
  
1.  Selezionare e fare clic con il pulsante destro del mouse sul progetto nel nodo **Integration Services**.  
  
2.  Per aprire la finestra di dialogo **Proprietà progetto** fare clic su **Proprietà** .  
  
3.  Aprire la pagina dei parametri facendo clic su **Parametri** in **Selezione pagina**.  
  
4.  Selezionare il parametro desiderato nell'elenco **Parametri** . Nota: la colonna **Contenitore** consente di distinguere tra i parametri del progetto e i parametri del pacchetto.  
  
5.  Nella colonna **Valore** specificare il valore del parametro predefinito del server desiderato.  
  
 Per impostare valori predefiniti del server con Transact-SQL, usare la stored procedure [catalog.set_object_parameter_value &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database). Per visualizzare i valori predefiniti del server corrente, eseguire una query nella vista [catalog.object_parameters &#40;database SSISDB&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database). Per cancellare un valore predefinito del server, usare la stored procedure [catalog.clear_object_parameter_value &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database).  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services &#40;parametri di&#41; SSIS](integration-services-ssis-package-and-project-parameters.md)  
  
  
