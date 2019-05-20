---
title: Gestione connessione Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPHDICM.F1
- SQL14.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 29d01bd9-8b38-43b1-b937-67f8aea57c0f
author: Lingxi-Li
ms.author: lingxl
manager: craigg
ms.openlocfilehash: 89bf14fb82516a9bd819431d92962169d56f68ae
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728356"
---
# <a name="azure-hdinsight-connection-manager"></a>Gestione connessione Azure HDInsight

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


La **gestione connessione Azure HDInsight** consente a un pacchetto SSIS di connettersi a un cluster HDInsight di Azure.

**Gestione connessione di Azure HDInsight** è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Per creare e configurare una **gestione connessione Azure HDInsight**, eseguire la procedura seguente:

1. Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare **AzureHDInsight**e fare clic su **Aggiungi**.
2. Nella finestra di dialogo **Editor gestione connessione Azure HDInsight** specificare il **nome DNS del cluster** (senza il prefisso del protocollo), il **nome utente** e la **password** del cluster HDInsight a cui connettersi.
3. Scegliere **OK** per chiudere la finestra di dialogo.
4. È possibile visualizzare le proprietà del componente Gestione connessione create nella finestra **Proprietà** .
