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
ms.openlocfilehash: c57abdf2cd6fbdf5cbb0953f1604440d714e1e7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968261"
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
