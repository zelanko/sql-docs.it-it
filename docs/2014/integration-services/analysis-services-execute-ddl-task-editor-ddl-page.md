---
title: Analysis Services Execute DDL Task Editor (pagina DDL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL Task Editor
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2b57ad76be3811352bbfb8774fb56c748efa1ac8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66061612"
---
# <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Editor attività Esegui DDL Analysis Services (pagina DDL)
  La pagina **DDL** della finestra di dialogo **Editor attività Esegui DDL Analysis Services** consente di specificare una connessione a un progetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o a un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per offrire informazioni sull'origine delle istruzioni DDL (Data Definition Language).  
  
 Per altre informazioni su questa attività, vedere [Attività Esegui DDL Analysis Services](control-flow/analysis-services-execute-ddl-task.md).  
  
## <a name="static-options"></a>Opzioni statiche  
 **Connessione**  
 Selezionare un progetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o una gestione connessione [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dall'elenco oppure fare clic su <\<**Nuova connessione**> e usare la finestra di dialogo **Aggiungi gestione connessione Analysis Services** per creare una nuova connessione.  
  
 **Argomenti correlati:** [Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Gestione connessione Analysis Services](connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 Consente di specificare il tipo di origine delle istruzioni DDL. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Direct Input**|Consente di impostare l'origine sull'istruzione DDL archiviata nella casella di testo **SourceDirect** . Quando si seleziona questo valore vengono visualizzate le opzioni dinamiche illustrate nella sezione seguente.|  
|**File Connection**|Consente di impostare l'origine su un file contenente l'istruzione DDL. Quando si seleziona questo valore vengono visualizzate le opzioni dinamiche illustrate nella sezione seguente.|  
|**Variabile**|Consente di impostare l'origine su una variabile. Quando si seleziona questo valore vengono visualizzate le opzioni dinamiche illustrate nella sezione seguente.|  
  
## <a name="dynamic-options"></a>Opzioni dinamiche  
  
### <a name="sourcetype--direct-input"></a>SourceType = Direct Input  
 **Origine**  
 Digitare le istruzioni DDL o fare clic sul pulsante con i puntini di sospensione **(...)** e quindi digitare le istruzioni nella finestra di dialogo **Istruzioni DDL**.  
  
### <a name="sourcetype--file-connection"></a>SourceType = File Connection  
 **Origine**  
 Selezionare una connessione file dall'elenco oppure fare clic su \<**Nuova connessione...**> e usare la finestra di dialogo **Gestione connessione file** per creare una nuova connessione.  
  
 **Argomenti correlati:** [Gestione connessione file](connection-manager/file-connection-manager.md)  
  
### <a name="sourcetype--variable"></a>SourceType = Variable  
 **Origine**  
 Selezionare una variabile dall'elenco oppure fare clic su \<**Nuova variabile**> e usare la finestra di dialogo **Aggiungi variabile** per creare una nuova variabile.  
  
 **Argomenti correlati:** [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Esegui DDL Analysis Services &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Pagina Espressioni](expressions/expressions-page.md)   
 [Flusso di controllo](control-flow/control-flow.md)   
 [Analysis Services Scripting Language &#40;ASSL&#41; riferimento](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Guida di riferimento a XML for Analysis &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)  
  
  
