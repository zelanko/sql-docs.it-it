---
title: Estrarre i file | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: bde4d7fa738bdc952abc936ea13caa7225887ad6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786746"
---
# <a name="check-out-files"></a>Estrazione di file
  Se l'ambiente [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] non è stato configurato per consentire la modifica dei file archiviati, è necessario eseguire l'estrazione di un file prima di poterlo modificare. Quando si estrae un file, una copia della sua versione viene salvata sul disco locale e l'attributo di sola lettura del file viene rimosso.  
  
 È possibile estrarre i file in modalità esclusiva o condivisa. Quando si estrae un file in modalità esclusiva, il file non può essere estratto da altri utenti finché non viene archiviato. Se un file viene estratto in modalità condivisa, può essere estratto e modificato da altri utenti. Al momento dell'archiviazione potrebbe essere quindi necessario unire le versioni create dai diversi utenti.  
  
 Usare la **Estrai** comando per estrarre i progetti di controllo del codice sorgente e file. Se si usa questo comando per estrarre una soluzione o progetto, tutti i file nella soluzione o progetto vengono anche estratti. Tuttavia, estrazione di un file di codice sorgente singoli non comporta l'estrazione del progetto o della soluzione a cui appartiene.  
  
> [!NOTE]  
>  Se il [!INCLUDE[msCoName](../includes/msconame-md.md)] database di Visual SourceSafe per il progetto è configurato per consentire più estrazioni e si desidera estrarre un file in modo esclusivo, è necessario cancellare il **Consenti più estrazioni** opzione il  **Controllare le opzioni avanzate** finestra di dialogo prima di estrarre il file. Per rendere effettiva questa impostazione è necessario riavviare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
### <a name="to-check-out-a-file"></a>Per estrarre un file  
  
1.  In Esplora soluzioni selezionare il progetto o il file desiderato.  
  
2.  Nel **File** dal menu **controllo del codice sorgente**, quindi fare clic su **Estrai per la modifica**.  
  
3.  Se il **Estrai per la modifica** verrà visualizzata la finestra di dialogo, selezionare le voci desiderate e fare clic su **Estrai**. Se è stata configurata la [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] ambiente non venga visualizzata la **Check Out** nella finestra di dialogo, gli elementi selezionati in Esplora soluzioni e possono contenere elementi figlio verranno estratti immediatamente.  
  
     **Check-Out**  
     Consente di estrarre tutti gli elementi selezionati.  
  
     **Colonne**  
     Consente di specificare le colonne da visualizzare e il relativo ordine.  
  
     **Commenti**  
     Consente di digitare un commento da associare all'operazione di estrazione.  
  
     **Non mostra la finestra Estrai durante l'estrazione di elementi**  
     Consente di impedire la visualizzazione della finestra di dialogo durante le operazioni di estrazione.  
  
     **Visualizzazione semplice**  
     Consente di visualizzare gli elementi che si stanno estraendo in elenchi semplici con la rispettiva connessione del controllo del codice sorgente.  
  
     **Modifica**  
     Modificare un elemento senza estrarlo. Il **Edit** pulsante viene visualizzato solo se hai [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] configurato per supportare la modifica dei file archiviati.  
  
     **Name**  
     Visualizza i nomi degli elementi che è possibile estrarre. Accanto a ogni elemento selezionato è disponibile una casella di controllo. Deselezionare tale casella se non si desidera estrarre l'elemento corrispondente.  
  
     **Opzioni**  
     Consente di visualizzare le opzioni di estrazione specifiche del plug-in del controllo del codice sorgente quando si fa clic sulla freccia a destra del pulsante.  
  
     **Sort**  
     Consente di scegliere l'ordine delle colonne visualizzate.  
  
     **Visualizzazione struttura ad albero**  
     Consente di visualizzare la gerarchia di file e cartelle relativa all'elemento che si desidera estrarre.  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare i file archiviati](../../2014/database-engine/edit-checked-in-files.md)   
 [Estrarre automaticamente i file al momento della modifica](../../2014/database-engine/automatically-check-out-files-upon-edit.md)   
 [Annullamento di estrazioni](../../2014/database-engine/undo-checkouts.md)   
 [Gestione delle estrazioni](../../2014/database-engine/manage-checkouts.md)  
  
  
