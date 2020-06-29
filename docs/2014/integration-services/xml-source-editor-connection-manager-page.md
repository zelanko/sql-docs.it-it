---
title: Editor origine XML (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmlsourceadapter.connectionmanager.f1
helpviewer_keywords:
- XML Source Editor
ms.assetid: e6507403-a3ce-4b6f-91fc-a7de9f7b6283
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ead9ad63b6dfc7d144c0d9e748ad01b847774d85
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85419728"
---
# <a name="xml-source-editor-connection-manager-page"></a>Editor origine XML (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** di **Editor origine XML** per specificare un file XML e il file XSD che trasforma i dati XML.  
  
 Per ulteriori informazioni sull'origine XML, vedere [XML Source](data-flow/xml-source.md).  
  
## <a name="static-options"></a>Opzioni statiche  
 **Modalità di accesso ai dati**  
 Consente di specificare il metodo per la selezione dei dati dall'origine.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|Percorso file XML|Consente di recuperare i dati da un file XML.|  
|File XML da variabile|Consente di specificare il nome del file XML in una variabile.<br /><br /> **Informazioni correlate**: [Utilizzo di variabili nei pacchetti](../../2014/integration-services/use-variables-in-packages.md)|  
|Dati XML da variabile|Consente di recuperare i dati XML da una variabile.|  
  
 **Usa schema inline**  
 Consente di specificare se i dati di origine XML contengono lo schema XSD che ne definisce e ne convalida la struttura e i dati.  
  
 **Percorso XSD**  
 Consente di digitare il percorso e il nome del file dello schema XSD o di individuare il file selezionando **Sfoglia**.  
  
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per individuare il file di schema XSD.  
  
 **Genera XSD**  
 Usare la finestra di dialogo **Salva con nome** per selezionare un percorso per il file di schema XSD creato automaticamente. L'editor deduce lo schema dalla struttura dei dati XML.  
  
## <a name="data-access-mode-dynamic-options"></a>Opzioni dinamiche relative alla modalità di accesso ai dati  
  
### <a name="data-access-mode--xml-file-location"></a>Modalità di accesso ai dati = Percorso file XML  
 **Percorso XML**  
 Consente di digitare il percorso e il nome del file di dati XML o di individuare il file scegliendo **Sfoglia**.  
  
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per individuare il file di dati XML.  
  
### <a name="data-access-mode--xml-file-from-variable"></a>Modalità di accesso ai dati = File XML da variabile  
 **Nome variabile**  
 Consente di selezionare la variabile contenente il percorso e il nome del file XML.  
  
### <a name="data-access-mode--xml-data-from-variable"></a>Modalità di accesso ai dati = Dati XML da variabile  
 **Nome variabile**  
 Consente di selezionare la variabile contenente i dati XML.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor origine XML &#40;pagina colonne&#41;](../../2014/integration-services/xml-source-editor-columns-page.md)   
 [Editor origine XML &#40;pagina output degli errori&#41;](../../2014/integration-services/xml-source-editor-error-output-page.md)   
 [Estrazione dei dati tramite l'origine XML](data-flow/extract-data-by-using-the-xml-source.md)  
  
  
