---
title: Editor destinazione file non elaborato (pagina colonne) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfiledestinationcolumns.f1
ms.assetid: 37f61d0b-1269-42ee-94ab-011cbaac63e9
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 444689420ad7f83568fc584257329f5133497f38
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964641"
---
# <a name="raw-file-destination-editor-columns-page"></a>Editor destinazione file non elaborato (pagina Colonne)
  Utilizzare l'Editor destinazione file non elaborato per configurare la destinazione file non elaborato in modo da scrivere dati non elaborati in un file.  
  
 **Per saperne di più**  
  
-   [Aprire l'Editor destinazione file non elaborato](#open)  
  
-   [Impostare le opzioni nella scheda Gestione connessione](#connection)  
  
-   [Impostare le opzioni nella scheda Colonne](#mapping)  
  
##  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a> Aprire l'Editor destinazione file non elaborato  
  
1.  Aggiungere la destinazione file non elaborato in un pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sul componente e quindi scegliere **Modifica**.  
  
##  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> Impostare le opzioni nella scheda Gestione connessione  
 **Modalità di accesso**  
 Selezionare come il nome file viene specificato. Selezionare **Nome file** per immettere direttamente il nome file e il percorso o **Nome file da variabile** per specificare una variabile che contiene il nome file.  
  
 **Nome file** o **Nome variabile**  
 Immettere il nome e il percorso del file non elaborato o selezionare la variabile contenente il nome file.  
  
 **Opzione scrittura**  
 Selezionare il metodo utilizzato per creare e scrivere nel file.  
  
 **Generare file non elaborato iniziale**  
 Fare clic sul pulsante per generare un file non elaborato vuoto contenente solo le colonne (file di soli metadati) senza dover eseguire il pacchetto. È possibile puntare l'origine file non elaborato al file di soli metadati.  
  
 Quando si fa clic sul pulsante, viene visualizzato un elenco delle colonne. È possibile fare clic su Annulla e modificare le colonne o fare clic su OK per procedere con la creazione del file.  
  
##  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a>Impostare le opzioni nella scheda colonne  
 **Colonne di input disponibili**  
 Selezionare uno o più colonne di input per scrivere nel file non elaborato.  
  
 **Colonna di input**  
 Una colonna di input viene aggiunta automaticamente a questa tabella quando la si seleziona in **Colonne di input disponibili**o è possibile selezionare direttamente la colonna di input in questa tabella.  
  
 **Alias di output**  
 Specificare un nome alternativo da utilizzare per la colonna di output.  
  
## <a name="see-also"></a>Vedere anche  
 [Destinazione file non elaborato](data-flow/raw-file-destination.md)  
  
  
