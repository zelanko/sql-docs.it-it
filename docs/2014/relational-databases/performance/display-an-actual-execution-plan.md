---
title: Visualizzare un piano di esecuzione effettivo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- displaying execution plans
- actual execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9403e6e2cf1c341780a06bbdff1c5f38685dd34a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63150974"
---
# <a name="display-an-actual-execution-plan"></a>Visualizzazione di un piano di esecuzione effettivo
  In questo argomento viene descritto come generare piani di esecuzione grafici effettivi utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Alla generazione di piani di esecuzione effettivi vengono eseguite le query o i batch di comandi [!INCLUDE[tsql](../../includes/tsql-md.md)] . Il piano di esecuzione generato visualizza il piano di esecuzione query effettivo utilizzato da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] per eseguire le query.  
  
 Per utilizzare questa funzionalità, gli utenti devono disporre delle autorizzazioni appropriate per eseguire le query [!INCLUDE[tsql](../../includes/tsql-md.md)] per le quali viene generato un piano di esecuzione grafico e dell'autorizzazione SHOWPLAN per tutti i database a cui fa riferimento la query.  
  
### <a name="to-include-an-execution-plan-for-a-query-during-execution"></a>Per includere un piano di esecuzione per una query durante l'esecuzione  
  
1.  Scegliere [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Query del motore di database **nella barra degli strumenti**. Per aprire una query esistente e visualizzare il piano di esecuzione stimato, è inoltre possibile fare clic sul pulsante **Apri file** della barra degli strumenti e individuare la query.  
  
2.  Immettere la query per quale si desidera visualizzare il piano di esecuzione effettivo.  
  
3.  Scegliere **Includi piano di esecuzione effettivo** dal menu **Query** oppure fare clic sul pulsante della barra degli strumenti **Includi piano di esecuzione effettivo**  
  
4.  Fare clic sul pulsante della barra degli strumenti **Esegui** per eseguire la query. Il piano usato da Query Optimizer viene visualizzato nella scheda **Piano di esecuzione** del riquadro dei risultati. Posizionando il puntatore del mouse sugli operatori logici e fisici è possibile visualizzare una descrizione comando contenente la descrizione e le proprietà degli operatori.  
  
     In alternativa, è possibile visualizzare le proprietà dell'operatore nella finestra Proprietà. Se la finestra Proprietà non è visibile, fare clic con il pulsante destro del mouse su un operatore e scegliere **Proprietà**. Selezionare un operatore e visualizzare le relative proprietà.  
  
5.  È possibile modificare la visualizzazione del piano di esecuzione facendo clic con il pulsante destro del mouse sul piano di esecuzione e scegliendo **Zoom avanti**, **Zoom indietro**, **Personalizza zoom**oppure **Adatta alla finestra**. Le opzioni**Zoom avanti** e **Zoom indietro** consentono rispettivamente di ingrandire e rimpicciolire il piano di esecuzione, mentre **Personalizza zoom** consente di definire un fattore di zoom personalizzato, ad esempio 80 percento. **Adatta alla finestra** consente di ingrandire il piano di esecuzione per adattarlo al riquadro Risultati.  
  
  
