---
title: Effettuare la connessione a Utilità SQL Server.
description: Informazioni su come connettersi a Utilità SQL Server in modo che sia possibile gestire l'integrità delle risorse di SQL Server. La connessione può essere eseguita attraverso SQL Server Management Studio (SSMS).
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fb961ccd1a1ec3013e186c7b45a54004ff400e07
ms.sourcegitcommit: e08d28530e0ee93c78a4eaaee8800fd687babfcc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2020
ms.locfileid: "86301790"
---
# <a name="connect-to-a-sql-server-utility"></a>Effettuare la connessione a Utilità SQL Server.

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Prima di connettersi a Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario creare un punto di controllo dell'utilità. Per altre informazioni, vedere [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  

Per visualizzare e gestire l'integrità delle risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) per connettersi a Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

Per connettersi a Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite SSMS:  

1. Avviare SSMS.

2. In SSMS connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

3. Selezionare **Visualizza** e quindi **Esplora utilità**.

4. Nel riquadro di spostamento di Esplora utilità selezionare :::image type="icon" source="media/connect-to-utility.gif" border="false"::: **Connetti a utilità**.

5. Nella finestra di dialogo **Connetti al server** specificare il nome dell'istanza del punto di controllo dell'utilità, quindi selezionare **Connetti**.

6. Visualizzare il riquadro di spostamento di Esplora utilità per passare a una visualizzazione albero delle risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel punto di controllo dell'utilità.

La creazione di un nuovo punto di controllo dell'utilità consente anche di connettersi a Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Creare un punto di controllo dell'Utilità SQL Server &#40;Utilità SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md).

## <a name="see-also"></a>Vedere anche

- [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)
- [Visualizzare i risultati dei criteri di integrità delle risorse &#40;SQL Server Utility&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)