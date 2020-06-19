---
title: Modificare il controllo del codice sorgente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- IDD_SCC_CONNECTION_DIALOG
helpviewer_keywords:
- Change Source Control dialog box
ms.assetid: e6a5d83c-5809-4c56-907a-73d0c7ccdd7a
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9a615e26ac966fcf0c2af580825019c344889a5d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936052"
---
# <a name="change-source-control"></a>Modificare il controllo del codice sorgente
  Consente di creare e gestire le connessioni e le associazioni che collegano una soluzione o un progetto salvato localmente a una cartella del database del controllo del codice sorgente.  
  
## <a name="dialog-box-access"></a>Accesso alla finestra di dialogo  
 In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] selezionare un elemento in Esplora soluzioni. Scegliere **controllo del codice sorgente**dal menu **file** , quindi **modificare il controllo del codice sorgente**.  
  
> [!NOTE]  
>  Per accedere a questa finestra di dialogo, è inoltre possibile fare clic con il pulsante destro del mouse sull'elemento in Esplora soluzioni.  
  
## <a name="options"></a>Opzioni  
 **Associare**  
 Consente di associare gli elementi selezionati a un determinato percorso del server del controllo del codice sorgente. È ad esempio possibile utilizzare questo pulsante per eseguire l'associazione all'ultima cartella e all'ultimo database noti del server del controllo del codice sorgente. Se non è possibile individuare una cartella o un database recente del server, verrà chiesto di specificarne un altro.  
  
 **Sfoglia**  
 Consente di selezionare un nuovo percorso del server del controllo del codice sorgente per l'elemento specificato.  
  
 **Colonne**  
 Consente di identificare le colonne da visualizzare e il relativo ordine di visualizzazione.  
  
 **Connettere**  
 Consente di creare una connessione tra gli elementi selezionati e il server del controllo del codice sorgente.  
  
 **Connesso**  
 Consente di visualizzare lo stato di connessione di una soluzione o di un progetto selezionato.  
  
 **Disconnetti**  
 Consente di disconnettere la copia locale di una soluzione o di un progetto archiviata nel computer dalla corrispondente copia master memorizzata nel database. Utilizzare questo comando prima di disconnettere il computer dal server di controllo del codice sorgente, ad esempio durante una sessione di lavoro sul portatile in modalità offline.  
  
 **OK**  
 Consente di accettare le modifiche eseguite in questa finestra di dialogo.  
  
 **Provider**  
 Consente di visualizzare il nome del plug-in del controllo del codice sorgente.  
  
 **Refresh** (Aggiornamento)  
 Consente di aggiornare le informazioni sulla connessione di tutti i progetti elencati in questa finestra di dialogo.  
  
 **Associazione server**  
 Indica l'associazione dell'elemento a un server del controllo del codice sorgente.  
  
 **Nome del server**  
 Consente di visualizzare il nome del server del controllo del codice sorgente a cui è associato il progetto o la soluzione corrispondente.  
  
 **Soluzione/Progetto**  
 Consente di visualizzare il nome di ogni soluzione e progetto presente nella selezione corrente.  
  
 **Ordina**  
 Consente di eseguire l'ordinamento delle colonne visualizzate.  
  
 **Status**  
 Consente di identificare lo stato di associazione e di connessione di un elemento. Le opzioni possibili sono:  
  
|**Opzione**|**Descrizione**|  
|----------------|---------------------|  
|Valido|L'elemento è correttamente associato e connesso alla cartella del server di appartenenza.|  
|Non valido|L'elemento è associato in modo non corretto o è disconnesso dalla cartella di appartenenza. Usare il comando **Aggiungi al controllo del codice sorgente** anziché **associa** per questo elemento.|  
|Sconosciuto|Lo stato dell'elemento incluso nel controllo del codice sorgente non è ancora stato determinato.|  
|Non incluso nel controllo del codice sorgente|L'elemento non è inserito nel controllo del codice sorgente.|  
  
 **Separa**  
 Consente di visualizzare la finestra di dialogo **controllo del codice sorgente** che consente di rimuovere gli elementi selezionati dal controllo del codice sorgente e di annullare in modo definitivo gli elementi delle cartelle presenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Controllo del codice sorgente di Esplora soluzioni](../../2014/database-engine/solution-explorer-source-control.md)  
  
  
