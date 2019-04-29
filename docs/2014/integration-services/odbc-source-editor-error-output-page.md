---
title: Editor origine ODBC (pagina Output degli errori) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: b2f6866c-db07-4cb3-9f38-889f8d2b03e6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 804431fea189d0dbe8e236591453571a5546cd5c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62890578"
---
# <a name="odbc-source-editor-error-output-page"></a>Editor origine ODBC (pagina Output degli errori)
  Usare la pagina **Output degli errori** della finestra di dialogo **ODBC Source Editor** (Editor origine ODBC) per selezionare le opzioni di gestione degli errori.  
  
 Per sapere di più sull'origine ODBC, vedere [Origine CDC](data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Elenco attività  
 **Per aprire ODBC Source Editor (pagina Output degli errori)**  
  
-   In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], aprire il pacchetto [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] che contiene l'origine ODBC.  
  
-   Nella scheda **Flusso di dati** fare doppio clic sull'origine ODBC.  
  
-   In **ODBC Source Editor**(Editor origine ODBC) fare clic su **Output degli errori**.  
  
## <a name="options"></a>Opzioni  
  
### <a name="inputoutput"></a>Input/Output  
 Consente di visualizzare il nome dell'origine dei dati.  
  
### <a name="column"></a>colonna  
 Non usato.  
  
### <a name="error"></a>Errore  
 Consente di selezionare il modo in cui l'origine ODBC deve gestire gli errori in un flusso: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
### <a name="truncation"></a>Troncamento  
 Consente di selezionare il modo in cui l'origine ODBC deve gestire il troncamento in un flusso: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
### <a name="description"></a>Descrizione  
 Non usato.  
  
### <a name="set-this-value-to-selected-cells"></a>Imposta questo valore nelle celle selezionate  
 Consente di selezionare il modo in cui l'origine ODBC gestisce tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
### <a name="apply"></a>Applica  
 Consente di applicare le opzioni di gestione degli errori alle celle selezionate.  
  
## <a name="error-handling-options"></a>Opzioni di gestione degli errori  
 Utilizzare le opzioni seguenti per configurare il modo in cui l'origine ODBC gestisce errori e troncamenti.  
  
### <a name="fail-component"></a>Interrompi componente  
 Quando si verifica un errore o un troncamento l'attività Flusso di dati viene interrotta. Questo è il comportamento predefinito.  
  
### <a name="ignore-failure"></a>Ignora errore  
 L'errore o il troncamento vengono ignorati.  
  
### <a name="redirect-flow"></a>Reindirizza flusso  
 La riga che determina l'errore o il troncamento viene inviata all'output degli errori dell'origine ODBC. Per altre informazioni, vedere [Origine ODBC](data-flow/odbc-source.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine ODBC &#40;pagina Gestione connessione&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [Editor origine ODBC &#40;pagina Colonne&#41;](../../2014/integration-services/odbc-source-editor-columns-page.md)  
  
  
