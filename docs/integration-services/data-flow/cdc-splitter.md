---
title: Barra di divisione CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.cdcsplitter.f1
ms.assetid: 167bc5c6-fa36-439d-987c-b20acd1a77e2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 38a72f9628e621f5ed960a125800451badd180e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727137"
---
# <a name="cdc-splitter"></a>CDC Splitter

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La barra di divisione CDC suddivide un singolo flusso di righe delle modifiche da un flusso di dati dell'origine CDC in diversi flussi di dati per operazioni di inserimento, aggiornamento ed eliminazione. Il flusso di dati viene suddiviso in base alla colonna obbligatoria `__$operation` e ai relativi valori standard nelle tabelle delle modifiche di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
|Valore dell'operazione|Output|Descrizione|  
|------------------------|------------|-----------------|  
|1|DELETE|Riga eliminata|  
|2|Insert|Riga inserita (non disponibile quando si usa la modalità CDC **Net with Merge** (Rete con unione))|  
|3|Update|Riga prima dell'aggiornamento (disponibile solo quando si usa la modalità CDC **All with Old Values** (Tutto con valori precedenti))|  
|4|Update|Riga dopo l'aggiornamento (segue l'operazione prima dell'aggiornamento)|  
|5|Update|Unione della riga (disponibile solo quando si usa la modalità CDC **Net with Merge** (Rete con unione))|  
|Altro|Errore||  
  
 È possibile utilizzare la barra di divisione per connettersi ad output INSERT, DELETE e UPDATE predefiniti per l'ulteriore elaborazione.  
  
 La trasformazione CDC Splitter include un input normale e un output degli errori.  
  
## <a name="error-handling"></a>Gestione degli errori  
 La trasformazione CDC Splitter include un output degli errori. Le righe di input con un valore non valido della colonna $operation vengono considerate errate e vengono gestite in base alla proprietà **ErrorRowDisposition** dell'input.  
  
 L'output degli errori del componente include le colonne di output seguenti:  
  
-   **Error Code** (Codice errore): impostare su 1.  
  
-   **Error Column**(Colonna errore): colonna di origine che causa l'errore (per gli errori di conversione).  
  
-   **Error Row Columns** (Colonne riga errore): colonne di input della riga che ha provocato l'errore.  
  
## <a name="configuring-the-cdc-splitter"></a>Configurazione della barra di divisione CDC  
 Non sono disponibili proprietà configurabili per la barra di divisione CDC.  
  
 Per ulteriori informazioni sull'utilizzo della barra di divisione CDC, vedere Componenti CDC per Microsoft SQL Server Integration Services.  
  
 La finestra di dialogo **Editor avanzato** contiene le proprietà che è possibile impostare a livello di codice.  
  
 Per aprire la finestra di dialogo **Editor avanzato** :  
  
-   Nella schermata **Flusso di dati** del progetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] fare clic con il pulsante destro del mouse sulla barra di divisione CDC e scegliere **Visualizza editor avanzato**.  
  
## <a name="see-also"></a>Vedere anche  
 [Indirizzare il flusso CDC in base al tipo di modifica](../../integration-services/data-flow/direct-the-cdc-stream-according-to-the-type-of-change.md)  
  
  
