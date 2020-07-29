---
title: Opzioni di convalida delle sottoscrizioni (sottoscrizioni merge)
description: Viene descritta la finestra di dialogo "Opzioni di convalida delle sottoscrizioni" in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.mergeoptions.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: 4958c4ab-2025-42ce-b836-6fb4e9e6f24d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 497282dbdc0710f732c10f9e06abbffc40d4d046
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111998"
---
# <a name="subscription-validation-options-merge-subscriptions"></a>Opzioni di convalida delle sottoscrizioni (sottoscrizioni di tipo merge)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Utilizzare la finestra di dialogo **Opzioni di convalida delle sottoscrizioni** per specificare se la convalida deve utilizzare solo il conteggio delle righe o deve utilizzare il conteggio delle righe e il checksum binario.  
  
## <a name="options"></a>Opzioni  
 **Verifica solo il conteggio delle righe**  
 Consente di verificare che la tabella nel Sottoscrittore abbia lo stesso numero di righe della tabella nel server di pubblicazione. Questa opzione non convalida la corrispondenza del contenuto delle righe. La convalida del conteggio delle righe è un controllo non approfondito che consente comunque di evidenziare eventuali problemi dei dati.  
  
 **Verifica il conteggio delle righe e confronta i valori di checksum per la verifica dei dati delle righe**  
 Oltre al conteggio delle righe nel server di pubblicazione e nel Sottoscrittore, viene calcolato un checksum di tutti i dati utilizzando l'algoritmo di checksum binario. In caso di esito negativo durante il conteggio delle righe il checksum non viene eseguito. Questa opzione non è valida per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare i dati nel Sottoscrittore](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [Convalidare i dati replicati](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
