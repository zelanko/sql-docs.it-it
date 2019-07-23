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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e1a458d4d2ad369a942e937d2270cb6e99d06e6c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115199"
---
# <a name="validate-subscriptions"></a>Convalida sottoscrizioni
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Utilizzare la finestra di dialogo **Convalida sottoscrizioni** per specificare che è necessario convalidare le sottoscrizioni di una pubblicazione transazionale alla successiva esecuzione dell'agente di distribuzione per ogni sottoscrizione. I risultati della convalida vengono visualizzati in Monitoraggio replica. Per altre informazioni, vedere [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
## <a name="options"></a>Opzioni  
 **Convalida tutte le sottoscrizioni SQL Server**  
 Selezionare questa opzione per convalidare i dati di tutte le sottoscrizioni SQL Server della pubblicazione specificata.  
  
 **Convalida le sottoscrizioni seguenti**  
 Selezionare questa opzione se non si desidera convalidare tutte le sottoscrizioni nell'apposito elenco.  
  
 **Opzioni di convalida**  
 Fare clic su questo pulsante per accedere alla finestra di dialogo **Opzioni di convalida delle sottoscrizioni** nella quale è possibile specificare se utilizzare la convalida mediante il conteggio delle righe oppure la convalida mediante checksum binario.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare i dati replicati](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
