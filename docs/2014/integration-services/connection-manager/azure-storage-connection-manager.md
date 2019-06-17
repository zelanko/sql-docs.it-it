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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ea689f96911af35176d6467e73d496b59f35e3c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833559"
---
# <a name="azure-storage-connection-manager"></a>Gestione connessione dell'archiviazione di Azure
  La gestione connessione di archiviazione di Azure consente a un pacchetto SSIS per connettersi a un account di archiviazione di Azure usando i valori specificati per la proprietà: Nome dell'account di archiviazione e Chiave dell'account.  
  
1.  Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare **Sottoscrizione di Azure**, quindi fare clic su **Aggiungi**.  
  
2.  Nella finestra di dialogo Editor gestione connessione di archiviazione di Azure, scegliere **Usa account Azure** per connettersi a un servizio di archiviazione di Azure con Internet o scegliere **Usa account per sviluppatore locale** per connettersi al servizio locale ospitato dall'emulatore di archiviazione di Azure.  
  
3.  Se si seleziona l'opzione **Usa account Azure** , eseguire queste operazioni:  
  
    1.  Specificare i valori per i campi **Nome dell'account di archiviazione** e **Chiave dell'account** . Questi valori vengono archiviati come dati sensibili nel pacchetto SSIS.  
  
    2.  Selezionare **Usa HTTPS** per usare HTTPS anziché HTTP per connettersi al servizio di archiviazione di Azure.  
  
4.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
5.  È possibile visualizzare le proprietà del componente Gestione connessione create nella finestra **Proprietà** .  
  
  
