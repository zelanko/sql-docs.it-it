---
title: Impostare il periodo di memorizzazione per la distribuzione
description: Impostare il periodo di memorizzazione dei dati all'interno del database di distribuzione in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: d699eb502d99818926e92ff07a8fc16248aeee3d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287208"
---
# <a name="set-distribution-retention-period-for-transactional-publications"></a>Impostare il periodo di memorizzazione per la distribuzione per le pubblicazioni transazionali
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  È possibile specificare i periodi minimo e massimo di memorizzazione per la distribuzione nella finestra di dialogo **Proprietà database di distribuzione - \<DatabaseDistribuzione>** , a cui è possibile accedere dalla pagina **Generale** della finestra di dialogo **Proprietà database di distribuzione - \<ServerDistribuzione>** . Per altre informazioni sull'accesso a questa finestra di dialogo, vedere [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-specify-the-distribution-retention-period"></a>Per specificare il periodo di memorizzazione per la distribuzione  
  
1.  Nella pagina **Generale** della finestra di dialogo **Proprietà database di distribuzione - \<DatabaseDistribuzione>** fare clic sul pulsante delle proprietà ( **...** ) relativo al database di distribuzione.  
  
2.  Per specificare il periodo minimo di memorizzazione per la distribuzione, immettere un valore nella casella **per almeno** . Per specificare il periodo massimo di memorizzazione per la distribuzione, immettere un valore nella casella **non oltre** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="see-also"></a>Vedere anche  
 [Configura distribuzione](../../relational-databases/replication/configure-distribution.md)   
 [Scadenza e disattivazione delle sottoscrizioni](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
