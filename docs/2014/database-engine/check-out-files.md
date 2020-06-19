---
title: Estrai file | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- Visual Studio.SourceControl.CheckOutDialog
helpviewer_keywords:
- checking out files
ms.assetid: cc033727-51bb-4b58-a12b-8977ce61ff56
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 10c076f7bee35e0e466fc22aec9ad9f6984bac6a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936032"
---
# <a name="check-out-files"></a>Estrazione di file
  Se l'ambiente [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] non è stato configurato per consentire la modifica dei file archiviati, è necessario eseguire l'estrazione di un file prima di poterlo modificare. Quando si estrae un file, una copia della sua versione viene salvata sul disco locale e l'attributo di sola lettura del file viene rimosso.  
  
 È possibile estrarre i file in modalità esclusiva o condivisa. Quando si estrae un file in modalità esclusiva, il file non può essere estratto da altri utenti finché non viene archiviato. Se un file viene estratto in modalità condivisa, può essere estratto e modificato da altri utenti. Al momento dell'archiviazione potrebbe essere quindi necessario unire le versioni create dai diversi utenti.  
  
 Usare il comando **Estrai** per estrarre i file e i progetti inclusi nel controllo del codice sorgente. Se si usa questo comando per estrarre una soluzione o un progetto, vengono estratti anche tutti i file inclusi nella soluzione o nel progetto. Tuttavia, l'estrazione di un singolo file di codice sorgente non comporta l'estrazione del progetto o della soluzione a cui appartiene.  
  
> [!NOTE]  
>  Se il [!INCLUDE[msCoName](../includes/msconame-md.md)] database di Visual SourceSafe per il progetto è configurato per consentire più estrazioni e si desidera estrarre un file esclusivamente, è necessario deselezionare l'opzione **Consenti più estrazioni** nella finestra di dialogo **Opzioni di estrazione avanzata** prima di estrarre il file. Per rendere effettiva questa impostazione è necessario riavviare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
### <a name="to-check-out-a-file"></a>Per estrarre un file  
  
1.  In Esplora soluzioni selezionare il progetto o il file desiderato.  
  
2.  Scegliere **controllo del codice sorgente**dal menu **file** e quindi fare clic su **Estrai per la modifica**.  
  
3.  Se viene visualizzata la finestra **di dialogo Estrai per la modifica** , selezionare gli elementi desiderati e fare clic su **Estrai**. Se l'ambiente non è stato configurato [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] per visualizzare la finestra di dialogo **Estrai** , gli elementi selezionati in Esplora soluzioni e gli eventuali elementi figlio che potrebbero avere sono estratti immediatamente.  
  
     **Estrai**  
     Consente di estrarre tutti gli elementi selezionati.  
  
     **Colonne**  
     Consente di specificare le colonne da visualizzare e il relativo ordine.  
  
     **Commenti**  
     Consente di digitare un commento da associare all'operazione di estrazione.  
  
     **Non visualizzare la finestra di dialogo Estrai durante l'estrazione degli elementi**  
     Consente di impedire la visualizzazione della finestra di dialogo durante le operazioni di estrazione.  
  
     **Visualizzazione semplice**  
     Consente di visualizzare gli elementi che si stanno estraendo in elenchi semplici con la rispettiva connessione del controllo del codice sorgente.  
  
     **Modifica**  
     Modificare un elemento senza estrarlo. Il pulsante **modifica** viene visualizzato solo se è stato [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] configurato per supportare la modifica dei file archiviati.  
  
     **Nome**  
     Visualizza i nomi degli elementi che è possibile estrarre. Accanto a ogni elemento selezionato è disponibile una casella di controllo. Deselezionare tale casella se non si desidera estrarre l'elemento corrispondente.  
  
     **Opzioni**  
     Consente di visualizzare le opzioni di estrazione specifiche del plug-in del controllo del codice sorgente quando si fa clic sulla freccia a destra del pulsante.  
  
     **Ordina**  
     Consente di scegliere l'ordine delle colonne visualizzate.  
  
     **Visualizzazione albero**  
     Consente di visualizzare la gerarchia di file e cartelle relativa all'elemento che si desidera estrarre.  
  
## <a name="see-also"></a>Vedere anche  
 [Modifica file archiviati](../../2014/database-engine/edit-checked-in-files.md)   
 [Estrai automaticamente i file al momento della modifica](../../2014/database-engine/automatically-check-out-files-upon-edit.md)   
 [Annulla estrazioni](../../2014/database-engine/undo-checkouts.md)   
 [Gestione delle estrazioni](../../2014/database-engine/manage-checkouts.md)  
  
  
