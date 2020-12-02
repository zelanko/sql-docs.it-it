---
description: Definisci filtri
title: Definisci filtri | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replconflictviewer.definefilters.f1
helpviewer_keywords:
- Define Filters dialog box
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e4834e78ec82a681faba9f6c0fa780d78f890def
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96121317"
---
# <a name="define-filters"></a>Definisci filtri
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La finestra di dialogo **Definisci filtri** consente di definire i filtri da applicare ai conflitti dei dati per visualizzare un subset dei conflitti nella griglia. Per definire un filtro, scegliere un operatore nell'elenco a discesa **Operatore** e quindi digitare un valore. Ad esempio, per visualizzare soltanto i conflitti in cui la riga in conflitto ignorata è il server **ReplTest1**, selezionare l'operatore **Uguale a** nell'elenco a discesa **Operatore** e immettere **ReplTest1** nella prima colonna **Valore** .  
  
## <a name="options"></a>Opzioni  
 **Operatore**  
 Consente di selezionare un operatore per il filtro, ad esempio **Minore o uguale a**.
  
 **Valore**  
 Consente di digitare un valore per il filtro. Per la maggior parte degli operatori è necessario specificare soltanto un valore nella prima colonna **Valore** , tuttavia, gli operatori **Compreso tra** e **Non compreso tra** richiedono un valore in entrambe le colonne **Valore** .  
  
 **Cancella**  
 Fare clic su questo pulsante per cancellare tutti i filtri definiti in precedenza.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzatore conflitti di replica Microsoft &#40;replica di tipo merge&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Visualizzatore conflitti di replica Microsoft &#40;replica di tipo transazionale&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  
