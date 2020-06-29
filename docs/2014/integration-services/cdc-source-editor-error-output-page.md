---
title: Editor origine CDC (pagina output degli errori) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.errorhandling.f1
ms.assetid: 8a4c2cb8-fd2f-4c45-824f-b93473a8981e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e4e44aea5cfd2cee5a4da920687d0f063df11460
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438968"
---
# <a name="cdc-source-editor-error-output-page"></a>Editor origine CDC (pagina Output degli errori)
  Usare la pagina **Output degli errori** della finestra di dialogo **Editor origine CDC** per selezionare le opzioni di gestione degli errori.  
  
 Per ulteriori informazioni sull'origine CDC, vedere [CDC Source](data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Elenco attività  
 **Per aprire CDC Source Editor (pagina Output degli errori)**  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], aprire il pacchetto [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] che contiene l'origine CDC.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine CDC.  
  
3.  In **Editor origine CDC**fare clic su **Output degli errori**.  
  
## <a name="options"></a>Opzioni  
 **Input/Output**  
 Consente di visualizzare il nome dell'origine dei dati.  
  
 **Colonna**  
 Consente di visualizzare le colonne esterne (di origine) selezionate nella pagina **Gestione connessione** della finestra di dialogo **Editor origine CDC** .  
  
 **Errore**  
 Consente di selezionare il modo in cui l'origine CDC deve gestire gli errori in un flusso: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Troncamento**  
 Consente di selezionare il modo in cui l'origine CDC deve gestire il troncamento in un flusso: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Descrizione**  
 Non usato.  
  
 **Imposta questo valore nelle celle selezionate**  
 Consente di selezionare il modo in cui l'origine CDC gestisce tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Applica**  
 Consente di applicare le opzioni di gestione degli errori alle celle selezionate.  
  
## <a name="error-handling-options"></a>Opzioni di gestione degli errori  
 Utilizzare le opzioni seguenti per configurare il modo in cui l'origine CDC gestisce errori e troncamenti.  
  
 **Interrompi componente**  
 Quando si verifica un errore o un troncamento l'attività Flusso di dati viene interrotta. Questo è il comportamento predefinito.  
  
 **Ignora errore**  
 L'errore o il troncamento viene ignorato e la riga di dati viene indirizzata all'output dell'origine CDC.  
  
 **Reindirizza flusso**  
 La riga di dati contenente l'errore o il troncamento viene indirizzata all'output degli errori dell'origine CDC. In questo caso, viene utilizzata la gestione degli errori dell'origine CDC. Per altre informazioni, vedere [Origine CDC](data-flow/cdc-source.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine CDC &#40;pagina Gestione connessione&#41;](../../2014/integration-services/cdc-source-editor-connection-manager-page.md)   
 [Editor origine CDC &#40;pagina Colonne&#41;](../../2014/integration-services/cdc-source-editor-columns-page.md)  
  
  
