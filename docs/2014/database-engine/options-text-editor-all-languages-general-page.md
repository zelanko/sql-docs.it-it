---
title: Opzioni (editor di testo-tutti i linguaggi-pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: bf18907c-94e2-4c09-9b2b-0925ac04c627
author: rothja
ms.author: jroth
ms.openlocfilehash: 721ebe6d235e1a8001403d4fb9bb993dba86dd13
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929966"
---
# <a name="options-text-editor---all-languages---general-page"></a>Opzioni (Editor di testo - Tutte le lingue - pagina Generale)
  Utilizzare questa finestra di dialogo per impostare le opzioni generali di modifica in tutti e cinque gli editor di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Per visualizzare le opzioni disponibili, scegliere **Opzioni** dal menu **Strumenti**. Selezionare la cartella **Editor di testo**, espandere la cartella **Tutti i linguaggi** e quindi fare clic su **Generale**.  
  
## <a name="option-settings-by-editor"></a>Impostazioni delle opzioni in base all'editor  
 Per impostare le opzioni per gli editor DMX, MDX e SQL Server Compact è necessario usare le finestre di dialogo **Tutti i linguaggi**. Le opzioni impostate in queste finestre vengono applicate anche agli editor di testo normale, Transact-SQL e XML, tuttavia, per tali editor, è possibile impostare separatamente le opzioni espandendo le sottocartelle per questi linguaggi e selezionando le relative pagine di opzioni.  
  
> [!CAUTION]  
>  Se si imposta un'opzione mediante questa finestra di dialogo, ma si desidera un'impostazione diversa per gli editor di testo normale, Transact-SQL o XML, le opzioni per questi editor devono essere impostate dopo l'applicazione delle selezioni nella finestra di dialogo **Tutti i linguaggi**.  
  
 Alcuni editor potrebbero non supportare tutte le opzioni elencate in questa pagina. Se nella pagina **Generale** della finestra di dialogo **Opzioni** un'opzione è selezionata solo per alcuni linguaggi di programmazione e non per altri, accanto all'opzione in questione verrà visualizzato un segno di spunta ombreggiato.  
  
## <a name="statement-completion"></a>Completamento istruzioni  
 **Elenco automatico membri**  
 Consente di visualizzare gli elenchi popup dei membri, delle proprietà e dei valori disponibili mentre si immettono i dati nell'editor. Scegliere un elemento dall'elenco popup per inserirlo nel codice. Se si seleziona questa casella di controllo, viene abilitata automaticamente l'opzione **Nascondi membri avanzati**.  
  
 **Nascondi membri avanzati**  
 Consente di ridurre gli elenchi popup relativi al completamento delle istruzioni visualizzando solo gli elementi utilizzati più di frequente. Gli altri elementi dell'elenco verranno filtrati. Se nessun elemento è contrassegnato come membro avanzato, l'opzione non è disponibile.  
  
 **Informazioni sui parametri**  
 Consente di visualizzare la sintassi completa della procedura o della dichiarazione corrente a sinistra del punto di inserimento nell'editor, insieme a tutti i parametri disponibili. Il parametro successivo che può essere assegnato è evidenziato in grassetto.  
  
## <a name="settings"></a>Impostazioni  
 **Abilita spazio virtuale**  
 Consente di inserire i commenti sempre nel medesimo punto accanto al codice. Quando questa casella di controllo è selezionata, è possibile posizionare il cursore oltre l'ultimo carattere nella riga. Durante l'immissione del testo, le tabulazioni e gli spazi vengono aggiunti automaticamente per completare la riga fino al punto di inserimento.  
  
 **A capo automatico**  
 Consente di visualizzare sulla riga successiva le parti di una riga che si estendono orizzontalmente oltre l'area visibile dell'editor. Se si seleziona questa casella di controllo, viene abilitata automaticamente l'opzione **Mostra icona per ritorno a capo automatico** .  
  
 **Mostra icone per ritorno a capo automatico**  
 Consente di visualizzare un simbolo di ritorno a capo nel punto in cui una riga lunga va a capo sulla riga successiva.  
  
> [!NOTE]  
>  I simboli di ritorno a capo non vengono aggiunti al codice, né stampati. Si tratta esclusivamente di elementi di riferimento. Questa caratteristica non è disponibile in tutti i tipi di editor.  
  
 **Applica comandi Taglia o Copia a righe vuote in assenza di selezione**  
 Consente di impostare il comportamento dell'editor nei casi in cui si posiziona il punto di inserimento in una riga vuota senza selezionare alcun elemento e quindi si fa clic su **Copia** o **Taglia**.  
  
 Se la casella di controllo è selezionata, la riga vuota viene copiata o incollata. Se quindi si fa clic su **Incolla**, viene inserita una nuova riga vuota.  
  
 Se la casella di testo è deselezionata, non viene copiato o tagliato alcun elemento. Se quindi si fa clic su **Incolla**, viene incollato il contenuto copiato più di recente. Se non è stata eseguita alcuna operazione di copia, non viene incollato alcun elemento.  
  
 Questa impostazione non ha alcun effetto sui comandi **Copia** o **Taglia** applicati a righe non vuote. Se non è selezionato alcun elemento, viene copiata o tagliata la riga intera. Se quindi si fa clic su **Incolla**, vengono incollati la riga intera e il relativo carattere di ritorno a capo.  
  
## <a name="display"></a>Schermo  
 **Numeri di riga**  
 Consente di visualizzare un numero di riga accanto a ogni riga di codice.  
  
> [!NOTE]  
>  I numeri di riga non vengono aggiunti al codice, né stampati. Si tratta esclusivamente di elementi di riferimento.  
  
 **Consenti navigazione URL con clic singolo**  
 Consente di trasformare il cursore nel simbolo di una mano quando si sofferma su un URL nell'editor. È possibile fare clic sull'URL per visualizzare nel browser la pagina indicata.  
  
 **Barra di navigazione**  
 Consente di visualizzare una barra di navigazione nella parte superiore dell'editor di codice. Usare gli elenchi a discesa **Oggetti** e **Procedure** per scegliere un determinato oggetto nel codice, selezionare una procedura e inserire un'istanza della procedura specificata. La barra di navigazione non è disponibile per tutti i tipi di codice.  
  
  
