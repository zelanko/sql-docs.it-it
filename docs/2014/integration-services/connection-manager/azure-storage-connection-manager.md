---
title: Gestione connessione dell'archiviazione di Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpstorageconn.f1
- sql11.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d1e19ee8c9b565f1b0333e68aad4353741511bcb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52799733"
---
# <a name="azure-storage-connection-manager"></a>Gestione connessione dell'archiviazione di Azure
  La gestione connessione di archiviazione di Azure consente a un pacchetto SSIS per connettersi a un account di archiviazione di Azure usando i valori specificati per la proprietà: Nome Account di archiviazione e chiave dell'Account.  
  
1.  Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare **Sottoscrizione di Azure**, quindi fare clic su **Aggiungi**.  
  
2.  Nella finestra di dialogo Editor gestione connessione di archiviazione di Azure, scegliere **Usa account Azure** per connettersi a un servizio di archiviazione di Azure con Internet o scegliere **Usa account per sviluppatore locale** per connettersi al servizio locale ospitato dall'emulatore di archiviazione di Azure.  
  
3.  Se si seleziona l'opzione **Usa account Azure** , eseguire queste operazioni:  
  
    1.  Specificare i valori per i campi **Nome dell'account di archiviazione** e **Chiave dell'account** . Questi valori vengono archiviati come dati sensibili nel pacchetto SSIS.  
  
    2.  Selezionare **Usa HTTPS** per usare HTTPS anziché HTTP per connettersi al servizio di archiviazione di Azure.  
  
4.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
5.  È possibile visualizzare le proprietà del componente Gestione connessione create nella finestra **Proprietà** .  
  
  
