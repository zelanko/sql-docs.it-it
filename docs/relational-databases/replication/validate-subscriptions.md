---
title: Convalida sottoscrizioni | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.subscriptions.f1
helpviewer_keywords:
- Validate Subscriptions dialog box
ms.assetid: 0ca39a35-f22c-46c5-82a4-342e34bf5d1b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 8cdff5889849596c0e83d84daf3c7fae73fd4f41
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920357"
---
# <a name="validate-subscriptions"></a>Convalida sottoscrizioni
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  Utilizzare la finestra di dialogo **Convalida sottoscrizioni** per specificare che è necessario convalidare le sottoscrizioni di una pubblicazione transazionale alla successiva esecuzione dell'agente di distribuzione per ogni sottoscrizione. I risultati della convalida vengono visualizzati in Monitoraggio replica. Per altre informazioni, vedere [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>Opzioni  
 **Convalida tutte le sottoscrizioni SQL Server**  
 Selezionare questa opzione per convalidare i dati di tutte le sottoscrizioni SQL Server della pubblicazione specificata.  
  
 **Convalida le sottoscrizioni seguenti**  
 Selezionare questa opzione se non si desidera convalidare tutte le sottoscrizioni nell'apposito elenco.  
  
 **Opzioni di convalida**  
 Fare clic su questo pulsante per accedere alla finestra di dialogo **Opzioni di convalida delle sottoscrizioni** nella quale è possibile specificare se utilizzare la convalida mediante il conteggio delle righe oppure la convalida mediante checksum binario.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare i dati replicati](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
