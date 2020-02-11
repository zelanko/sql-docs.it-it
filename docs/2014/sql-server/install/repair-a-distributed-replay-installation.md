---
title: Ripristinare un'installazione di Riesecuzione distribuita | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092962"
---
# <a name="repair-a-distributed-replay-installation"></a>Ripristinare un'installazione di Riesecuzione distribuita
  Il ripristino di un componente Riesecuzione distribuita (controller o client) comporta le operazioni seguenti:  
  
1.  Installare tutti i file associati sul disco e sostituire tutti i file esistenti.  
  
2.  Ricreare l'account del servizio Windows se l'account corrispondente è stato rimosso.  
  
 Non è possibile utilizzare l'operazione Ripristina per aggiungere o rimuovere componenti. Per aggiungere o rimuovere componenti, selezionare o deselezionare il componente corrispondente nell'albero delle funzionalità nella pagina **Selezione funzionalità** del programma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installazione.  
  
### <a name="to-repair-a-failed-installation-of-distributed-replay"></a>Per ripristinare un'installazione con errori di Riesecuzione distribuita  
  
1.  Dal menu **Start** scegliere **Pannello di controllo**e quindi fare doppio clic su **Installazione applicazioni**.  
  
2.  Selezionare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nella finestra **Disinstalla o modifica programma** , quindi nella finestra di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dialogo fare clic su **Ripristina**.  
  
3.  Seguire i passaggi della [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] procedura guidata e nella pagina **Selezione funzionalità** Selezionare i componenti riesecuzione distribuita che si desidera ripristinare, quindi fare clic su **Avanti.**  
  
4.  Completare l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per ripristinare le funzionalità di Riesecuzione distribuita selezionate.  
  
  
