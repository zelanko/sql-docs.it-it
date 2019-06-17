---
title: Ripristinare un'installazione di Distributed Replay | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6fcd8ca8-1ceb-457d-9545-096c74e274d7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca42f1dda184bf5cd99cad7d34f5ae9fce79478b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092962"
---
# <a name="repair-a-distributed-replay-installation"></a>Ripristinare un'installazione di Riesecuzione distribuita
  Il ripristino di un componente Riesecuzione distribuita (controller o client) comporta le operazioni seguenti:  
  
1.  Installare tutti i file associati sul disco e sostituire tutti i file esistenti.  
  
2.  Ricreare l'account del servizio Windows se l'account corrispondente è stato rimosso.  
  
 Non è possibile utilizzare l'operazione Ripristina per aggiungere o rimuovere componenti. Per aggiungere o rimuovere componenti, selezionare o deselezionare il componente corrispondente nell'albero delle funzionalità nella **selezione delle caratteristiche** nella pagina [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il programma di installazione.  
  
### <a name="to-repair-a-failed-installation-of-distributed-replay"></a>Per ripristinare un'installazione con errori di Riesecuzione distribuita  
  
1.  Dal menu **Start** scegliere **Pannello di controllo**e quindi fare doppio clic su **Installazione applicazioni**.  
  
2.  Selezionare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nella **Disinstalla o modifica programma** finestra e quindi il [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nella finestra di dialogo fare clic su **Repair**.  
  
3.  Seguire i passaggi nel [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] procedura guidata e nella **Selezione funzionalità** pagina, selezionare i componenti riesecuzione distribuita si vuole ripristinare e quindi fare clic su **successivo.** .  
  
4.  Completare l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per ripristinare le funzionalità di Riesecuzione distribuita selezionate.  
  
  
