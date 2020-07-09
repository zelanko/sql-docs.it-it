---
title: Finestra di dialogo Opzioni di convalida delle sottoscrizioni (sottoscrizioni transazionali)
description: Viene descritta la finestra di dialogo "Opzioni di convalida delle sottoscrizioni" per la replica transazionale in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.options.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: fd66ad1f-df01-4240-9e89-8f41bff12c1e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 390f82aeb965e6031682b524544e12c613518af7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729308"
---
# <a name="subscription-validation-options-transactional-subscriptions"></a>Opzioni di convalida delle sottoscrizioni (sottoscrizioni transazionali)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/applies-to-version/sql-asdb.md)]
  La finestra di dialogo **Opzioni di convalida delle sottoscrizioni** consente di specificare se la convalida deve utilizzare solo un conteggio di righe o un conteggio di righe e un checksum binario. 

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>Opzioni  
 **Verificare che il Sottoscrittore includa lo stesso numero di righe di dati replicati del server di pubblicazione**  
 Consente di selezionare il tipo di convalida del conteggio di righe da eseguire. Per le pubblicazioni Oracle, l'unica opzione disponibile è **Esegui il conteggio di righe effettivo tramite una query diretta nelle tabelle**.  
  
 **Confronta i valori di checksum per la verifica dei dati delle righe**  
 Oltre al conteggio delle righe nel server di pubblicazione e nel Sottoscrittore, viene calcolato un checksum di tutti i dati utilizzando l'algoritmo di checksum binario. In caso di esito negativo durante il conteggio delle righe il checksum non viene eseguito.  
  
 **Arresta l'agente di distribuzione al termine della convalida**  
 Per impostazione predefinita, l'agente di distribuzione viene eseguito in modo continuativo. Selezionare questa opzione per arrestare l'agente dopo l'esecuzione della convalida. In tal modo è possibile controllare se la convalida è riuscita prima di continuare la replica dei dati nel Sottoscrittore.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare i dati nel Sottoscrittore](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [Convalidare i dati replicati](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
