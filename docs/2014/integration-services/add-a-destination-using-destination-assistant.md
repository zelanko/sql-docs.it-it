---
title: Aggiungere una destinazione utilizzando Assistente destinazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 747a0de0-3c2f-4d31-a692-7111fc0911d8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2eb1df7896cb93e72c80251786170e0a03b46a0a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376729"
---
# <a name="add-a-destination-using-destination-assistant"></a>Aggiunta di una destinazione tramite Assistente destinazione
  Questo argomento illustra i passaggi necessari per aggiungere una nuova destinazione usando Assistente destinazione ed elenca inoltre le opzioni disponibili nella finestra di dialogo **Aggiungi nuova destinazione** che viene visualizzata quando si trascina Assistente destinazione in Progettazione SSIS.  
  
### <a name="to-use-destination-assistant-to-add-a-destination"></a>Per utilizzare Assistente destinazione per aggiungere una destinazione  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a cui si desidera aggiungere un componente di destinazione.  
  
2.  Trascinare il componente **Assistente destinazione** dalla casella degli strumenti di SSIS alla scheda **Flusso di dati** . Verrà visualizzata la finestra di dialogo **Aggiungi nuova destinazione** . Nella sezione successiva vengono forniti i dettagli relativi alle opzioni disponibili nella finestra di dialogo.  
  
3.  Selezionare il tipo della destinazione nell'elenco **Tipi**.  
  
4.  Selezionare una gestione connessione esistente nell'elenco **Gestioni connessioni** oppure selezionare **\<Nuova>** per creare una nuova gestione connessione.  
  
5.  Se si seleziona una gestione connessione esistente, fare clic su **OK** per chiudere la finestra di dialogo **Aggiungi nuova destinazione**. La destinazione e le gestioni connessioni verranno aggiunte al flusso di dati.  
  
6.  Se si fa clic su **\<Nuova>** per creare una nuova gestione connessione, viene visualizzata la finestra di dialogo **Gestione connessione** in cui è possibile specificare i parametri per la connessione. Dopo avere completato la creazione della nuova gestione connessione, la destinazione e la gestione connessione saranno visibili in Progettazione SSIS.  
  
  
