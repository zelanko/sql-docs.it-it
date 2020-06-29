---
title: Gestione connessione Azure Resource Manager | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPARMCM.F1
- SQL11.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: a2380258-0418-4a8c-a731-5071a44ddf1e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1dce4def11f14072295dbf3cde9d5ab77304fe74
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439348"
---
# <a name="azure-resource-manager-connection-manager"></a>Gestione connessione Azure Resource Manager
La **gestione connessione Azure Resource Manager** consente a un pacchetto SSIS di gestire le risorse di Azure mediante un'[entità servizio](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).

Per creare e configurare una **gestione connessione Azure Resource Manager**, eseguire la procedura seguente:

1. Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare **AzureResourceManager** e fare clic su **Aggiungi**.
2. Nella finestra di dialogo **Editor gestione connessione Azure Resource Manager** compilare i campi **ID applicazione**, **Chiave applicazione** e **ID tenant** per l'entità servizio. Per informazioni dettagliate su queste proprietà, vedere [questo](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal) articolo.
3. Fare clic su **OK** per chiudere la finestra di dialogo.
4. È possibile visualizzare le proprietà del componente Gestione connessione create nella finestra **Proprietà** .
