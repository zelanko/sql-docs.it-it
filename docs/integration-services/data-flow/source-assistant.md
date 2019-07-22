---
title: Assistente origine | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sourceassistant.f1
- sql13.dts.designer.addNewSource.f1
ms.assetid: 5ca9d821-7d61-4727-9133-5f9cb485c7f3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 493d5a0d7ab5e9971747abe022fa46edbf615ae4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096658"
---
# <a name="source-assistant"></a>Assistente origine

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Il componente Assistente origine consente di creare un componente di origine e una gestione connessione. Il componente si trova nella sezione **Preferiti** della casella degli strumenti di SSIS.  
  
> [!NOTE]  
>  Assistente origine sostituisce il progetto Connessioni in Integration Services e la procedura guidata corrispondente.  
  
## <a name="add-a-source-with-source-assistant"></a>Aggiungere un'origine tramite Assistente origine
Questa sezione illustra i passaggi necessari per aggiungere una nuova origine usando Assistente origine ed elenca le opzioni disponibili nella finestra di dialogo **Aggiungi nuova origine** che viene visualizzata quando si trascina Assistente origine in Progettazione SSIS.  

1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a cui si vuole aggiungere un componente di origine.  
  
2.  Trascinare il componente **Assistente origine** dalla casella degli strumenti di SSIS alla scheda **Flusso di dati** . Verrà visualizzata la finestra di dialogo **Aggiungi nuova origine** . Nella sezione successiva vengono forniti i dettagli relativi alle opzioni disponibili nella finestra di dialogo.  
  
3.  Selezionare il tipo della destinazione nell'elenco **Tipi**.  
  
4.  Selezionare una gestione connessione esistente nell'elenco **Gestioni connessioni** oppure selezionare **\<Nuova>** per creare una nuova gestione connessione.  
  
5.  Se si seleziona una gestione connessione esistente, fare clic su **OK** per chiudere la finestra di dialogo **Aggiungi nuova destinazione**. La destinazione e le gestioni connessioni verranno aggiunte al flusso di dati.  
  
6.  Se si fa clic su **\<Nuova>** per creare una nuova gestione connessione, viene visualizzata la finestra di dialogo **Gestione connessione** in cui è possibile specificare i parametri per la connessione. Dopo avere completato la creazione della nuova gestione connessione, la destinazione e la gestione connessione saranno visibili in Progettazione SSIS.  

## <a name="add-new-source-dialog-box"></a>Finestra di dialogo Aggiungi nuova origine
La tabella seguente elenca le opzioni disponibili nella finestra di dialogo **Aggiungi nuova origine**.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Tipi|Selezionare il tipo di origine a cui si desidera connettersi.|  
|Gestioni connessioni|Selezionare una gestione connessione esistente oppure fare clic su **\<Nuova>** per creare una nuova gestione connessione.|  
|Mostra solo installati|Consente di specificare se visualizzare solo le origini installate.|  
|OK|Fare clic per salvare le modifiche e aprire eventuali finestre di dialogo successive per configurare opzioni aggiuntive.| 
  
