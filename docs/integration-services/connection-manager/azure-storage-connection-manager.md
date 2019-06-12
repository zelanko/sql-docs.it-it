---
title: Gestione connessione dell'archiviazione di Azure | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03acf5db82c21a66e2fbd8337713b6989ce36a31
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403065"
---
# <a name="azure-storage-connection-manager"></a>Gestione connessione dell'archiviazione di Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  **Gestione connessione dell'archiviazione di Azure** consente a un pacchetto SSIS di connettersi a un account di archiviazione di Azure.
   
 **Gestione connessione dell'archiviazione di Azure** è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md). 
  
Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare **Sottoscrizione di Azure**, quindi fare clic su **Aggiungi**.  
  
Sono disponibili le proprietà seguenti.

- **Service:** specifica il servizio di archiviazione a cui connettersi.
- **Account name:** specifica il nome dell'account di archiviazione.
- **Authentication:** specifica il metodo di autenticazione da usare. Sono supportati i metodi di autenticazione **AccessKey** e **ServicePrincipal**.
    - **AccessKey:** per questo metodo di autenticazione, specificare la **chiave dell'account**.
    - **ServicePrincipal:** per questo metodo di autenticazione, specificare l'**ID applicazione**, la **chiave applicazione** e l'**ID tenant** per l'entità servizio.
      All'entità servizio deve essere assegnato il ruolo di **collaboratore dati BLOB del servizio di archiviazione** all'account di archiviazione.
      Per informazioni dettagliate, vedere [questa](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal) pagina.
- **Environment:** specifica l'ambiente cloud che ospita l'account di archiviazione.
