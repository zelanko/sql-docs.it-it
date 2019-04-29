---
title: ODBC Destination Editor (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.connection.f1
ms.assetid: f6d9c6c2-e4c4-468b-9e0d-af7b9609614d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bc651d10df7433bdb0217414f251d16ed6abdf70
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62890638"
---
# <a name="odbc-destination-editor-connection-manager-page"></a>Editor destinazione ODBC (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** della finestra di dialogo **ODBC Destination Editor** per selezionare la gestione connessione ODBC per la destinazione. Tramite questa pagina è inoltre possibile selezionare una tabella o una vista del database  
  
 Per ulteriori informazioni sulla destinazione ODBC, vedere [ODBC Destination](data-flow/odbc-destination.md).  
  
 **Per aprire ODBC Destination Editor (pagina Gestione connessione)**  
  
## <a name="task-list"></a>Elenco attività  
  
-   In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], aprire il pacchetto [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] con la destinazione ODBC.  
  
-   Nella scheda **Flusso di dati** fare doppio clic sulla destinazione ODBC.  
  
-   In **ODBC Destination Editor**, fare clic su **Gestione connessione**.  
  
## <a name="options"></a>Opzioni  
  
### <a name="connection-manager"></a>Gestione connessione  
 Consente di selezionare una gestione connessione ODBC esistente nell'elenco o di creare una nuova connessione facendo clic su Nuova. La connessione può essere a qualsiasi database supportato da ODBC.  
  
### <a name="new"></a>Nuovo  
 Fare clic su **Nuovo**. Viene visualizzata la finestra di dialogo **Configura gestione connessione ODBC** in cui è possibile creare una nuova gestione connessione.  
  
### <a name="data-access-mode"></a>Modalità di accesso ai dati  
 Consente di selezionare il metodo di caricamento dei dati nella destinazione. Le opzioni disponibili vengono visualizzate nella tabella seguente.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Nome tabella - Batch|Selezionare questa opzione per configurare la destinazione ODBC per l'utilizzo della modalità batch. Se si seleziona questa opzione, sono disponibili le opzioni seguenti.|  
||**Nome tabella o vista**: selezionare una tabella o vista disponibile nell'elenco.<br /><br /> Questo elenco contiene solo le prime 1000 tabelle. Se il database contiene più di 1000 tabelle, è possibile digitare l'inizio di un nome di tabella o usare il carattere jolly (\*) per immettere qualsiasi parte del nome e visualizzare la tabella o le tabelle che si vuole usare.<br /><br /> **Dimensioni batch**: tipo di dimensioni del batch per il caricamento bulk. Si tratta del numero di righe caricato come un batch|  
|Nome tabella - Riga per riga|Selezionare questa opzione per configurare la destinazione ODBC per l'inserimento di una riga per volta nella tabella di destinazione. Se si seleziona questa opzione, è disponibile l'opzione seguente.|  
||**Nome tabella o vista**: selezionare una tabella o vista disponibile dal database nell'elenco.<br /><br /> Questo elenco contiene solo le prime 1000 tabelle. Se il database contiene più di 1000 tabelle, è possibile digitare l'inizio di un nome di tabella o utilizzare il carattere jolly (*) per immettere qualsiasi parte del nome e visualizzare la tabella o le tabelle che si desidera utilizzare.|  
  
### <a name="preview"></a>Anteprima  
 Fare clic su **Anteprima** per visualizzare fino a 200 dati per la tabella selezionata.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà personalizzate della destinazione ODBC](data-flow/odbc-destination-custom-properties.md)   
 [Editor destinazione ODBC &#40;pagina Mapping&#41;](../../2014/integration-services/odbc-destination-editor-mappings-page.md)   
 [Editor destinazione ODBC &#40;pagina Output degli errori&#41;](../../2014/integration-services/odbc-destination-editor-error-output-page.md)  
  
  
