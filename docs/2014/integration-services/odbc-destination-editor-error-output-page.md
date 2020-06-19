---
title: Editor destinazione ODBC (pagina output degli errori) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 82853123767237314edac1e301723724628439d9
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965041"
---
# <a name="odbc-destination-editor-error-output-page"></a>Editor destinazione ODBC (pagina Output errori)
  Utilizzare la pagina **Output degli errori** della finestra di dialogo **ODBC Destination Editor** per selezionare le opzioni di gestione degli errori.  
  
 Per ulteriori informazioni sulla destinazione ODBC, vedere [ODBC Destination](data-flow/odbc-destination.md).  
  
 **Per aprire ODBC Destination Editor (pagina Output degli errori)**  
  
## <a name="task-list"></a>Elenco attività  
  
-   In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], aprire il pacchetto [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] con la destinazione ODBC.  
  
-   Nella scheda **Flusso di dati** fare doppio clic sulla destinazione ODBC.  
  
-   In **ODBC Destination Editor**, fare clic su **Output degli errori**.  
  
## <a name="options"></a>Opzioni  
  
### <a name="inputoutput"></a>Input/Output  
 Consente di visualizzare il nome dell'origine dei dati.  
  
### <a name="column"></a>Colonna  
 Non usato.  
  
### <a name="error"></a>Errore  
 Consente di selezionare il modo in cui la destinazione ODBC deve gestire gli errori in un flusso: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
### <a name="truncation"></a>Troncamento  
 Consente di selezionare il modo in cui la destinazione ODBC deve gestire il troncamento in un flusso: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
### <a name="description"></a>Description  
 Consente di visualizzare una descrizione dell'errore.  
  
### <a name="set-this-value-to-selected-cells"></a>Imposta questo valore nelle celle selezionate  
 Consente di selezionare il modo in cui la destinazione ODBC gestisce tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
### <a name="apply"></a>Applica  
 Consente di applicare le opzioni di gestione degli errori alle celle selezionate.  
  
## <a name="error-handling-options"></a>Opzioni di gestione degli errori  
 Utilizzare le opzioni seguenti per configurare il modo in cui la destinazione ODBC gestisce errori e troncamenti.  
  
### <a name="fail-component"></a>Interrompi componente  
 Quando si verifica un errore o un troncamento l'attività Flusso di dati viene interrotta. Questo è il comportamento predefinito.  
  
### <a name="ignore-failure"></a>Ignora errore  
 L'errore o il troncamento vengono ignorati.  
  
### <a name="redirect-flow"></a>Reindirizza flusso  
 La riga che determina l'errore o il troncamento viene inviata all'output degli errori della destinazione ODBC. Per ulteriori informazioni, vedere Destinazione ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor destinazione ODBC &#40;pagina Gestione connessione&#41;](../../2014/integration-services/odbc-destination-editor-connection-manager-page.md)   
 [ODBC Destination Editor &#40;pagina Mapping&#41;](../../2014/integration-services/odbc-destination-editor-mappings-page.md)  
  
  
