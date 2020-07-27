---
title: Assistente destinazione | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.destinationassistant.f1
- sql13.DTS.DESIGNER.DESTINATIONASSIST.F1
ms.assetid: 10a40921-a2c2-4ac8-be28-311f8500fbf6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b36cd33f3d9cc0b18c0454abe393e8e68e96c644
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916721"
---
# <a name="destination-assistant"></a>Assistente destinazione

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Il componente Assistente destinazione consente di creare un componente di destinazione e una gestione connessione. Il componente si trova nella sezione **Preferiti** della casella degli strumenti di SSIS.  
  
> [!NOTE]  
>  Assistente destinazione sostituisce il progetto Connessioni in Integration Services e la procedura guidata corrispondente.  

## <a name="add-a-destination-with-destination-assistant"></a>Aggiungere una destinazione con Assistente destinazione
Questo argomento illustra i passaggi necessari per aggiungere una nuova destinazione usando Assistente destinazione ed elenca inoltre le opzioni disponibili nella finestra di dialogo **Aggiungi nuova destinazione** che viene visualizzata quando si trascina Assistente destinazione in Progettazione SSIS.  

1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a cui si desidera aggiungere un componente di destinazione.  
  
2.  Trascinare il componente **Assistente destinazione** dalla casella degli strumenti di SSIS alla scheda **Flusso di dati** . Verrà visualizzata la finestra di dialogo **Aggiungi nuova destinazione** . Nella sezione successiva vengono forniti i dettagli relativi alle opzioni disponibili nella finestra di dialogo.  
  
3.  Selezionare il tipo della destinazione nell'elenco **Tipi**.  
  
4.  Selezionare una gestione connessione esistente nell'elenco **Gestioni connessioni** oppure selezionare **\<New>** per creare una nuova gestione connessione.  
  
5.  Se si seleziona una gestione connessione esistente, fare clic su **OK** per chiudere la finestra di dialogo **Aggiungi nuova destinazione**. La destinazione e le gestioni connessioni verranno aggiunte al flusso di dati.  
  
6.  Se si fa clic su **\<New>** per creare una nuova gestione connessione, verrà visualizzata la finestra di dialogo **Gestione connessione** in cui specificare i parametri per la connessione. Dopo avere completato la creazione della nuova gestione connessione, la destinazione e la gestione connessione saranno visibili in Progettazione SSIS. 
  
## <a name="add-new-destination-dialog-box"></a>Finestra di dialogo Aggiungi nuova destinazione
La tabella seguente elenca le opzioni disponibili nella Finestra di dialogo **Aggiungi nuova destinazione**.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Tipi|Selezionare il tipo di destinazione a cui si desidera connettersi.|  
|Gestioni connessioni|Selezionare una gestione connessione esistente oppure fare clic su **\<New>** per creare una nuova gestione connessione.|  
|Mostra solo installati|Consente di specificare se visualizzare solo le destinazioni installate.|  
|OK|Fare clic per salvare le modifiche e aprire eventuali finestre di dialogo successive per configurare opzioni aggiuntive.|  
