---
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
ms.openlocfilehash: 4ae37ea5fd27ae6309eaa5cf879b562e254c1786
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063075"
---
# <a name="define-filters"></a>Definisci filtri
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La finestra di dialogo **Definisci filtri** consente di definire i filtri da applicare ai conflitti dei dati per visualizzare un subset dei conflitti nella griglia. Per definire un filtro, scegliere un operatore nell'elenco a discesa **Operatore** e quindi digitare un valore. Ad esempio, per visualizzare soltanto i conflitti in cui la riga in conflitto ignorata è il server **ReplTest1**, selezionare l'operatore **Uguale a** nell'elenco a discesa **Operatore** e immettere **ReplTest1** nella prima colonna **Valore** .  
  
## <a name="options"></a>Opzioni  
 **Operatore**  
 Consente di selezionare un operatore per il filtro, ad esempio **Minore o uguale a**.  
  
 **Value**  
 Consente di digitare un valore per il filtro. Per la maggior parte degli operatori è necessario specificare soltanto un valore nella prima colonna **Valore** , tuttavia, gli operatori **Compreso tra** e **Non compreso tra** richiedono un valore in entrambe le colonne **Valore** .  
  
 **Clear**  
 Fare clic su questo pulsante per cancellare tutti i filtri definiti in precedenza.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzatore conflitti di replica Microsoft &#40;replica di tipo merge&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Visualizzatore conflitti di replica Microsoft &#40;replica di tipo transazionale&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  
