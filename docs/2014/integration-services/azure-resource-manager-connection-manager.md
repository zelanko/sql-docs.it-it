---
title: Gestione connessione Azure Resource Manager | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPARMCM.F1
- SQL11.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: a2380258-0418-4a8c-a731-5071a44ddf1e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 55f7aaaa80992240468f3a94d6fd3b9a0f8807b9
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388529"
---
# <a name="azure-resource-manager-connection-manager"></a>Gestione connessione Azure Resource Manager
La **gestione connessione Azure Resource Manager** consente a un pacchetto SSIS di gestire le risorse di Azure mediante un'[entità servizio](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).

Per creare e configurare una **gestione connessione Azure Resource Manager**, eseguire la procedura seguente:

1. Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare **AzureResourceManager** e fare clic su **Aggiungi**.
2. Nella finestra di dialogo **Editor gestione connessione Azure Resource Manager** compilare i campi **ID applicazione**, **Chiave applicazione** e **ID tenant** per l'entità servizio. Per informazioni dettagliate su queste proprietà, vedere [questo](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal) articolo.
3. Scegliere **OK** per chiudere la finestra di dialogo.
4. È possibile visualizzare le proprietà del componente Gestione connessione create nella finestra **Proprietà** .
