---
title: Opzioni (editor di testo-XML-pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 46a9f913-d0b9-40ff-b382-9bbdec7461a6
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b32dcfc95c5fc6929454add71ff4452e00fdda6e
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83001044"
---
# <a name="options-text-editor---xml---general-page"></a>Opzioni (Editor di testo - XML - pagina Generale)
  Utilizzare questa finestra di dialogo per cambiare il comportamento di modifica generale dell'editor XML utilizzato per modificare i documenti XML. Per visualizzare le impostazioni scegliere **Opzioni** dal menu **Strumenti** , espandere la sottocartella **XML** e quindi fare clic su **Generale**.  
  
## <a name="setting-options-in-multiple-locations"></a>Opzioni di impostazione in più posizioni  
 Le opzioni per l'editor XML possono essere impostate anche nella finestra di dialogo **Tutti i linguaggi - Generale** . Se si utilizzano le finestre di dialogo **tutti i linguaggi** per impostare opzioni diverse per gli altri [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] Editor, ad esempio DMX o MDX, è necessario reimpostare le opzioni dell'editor XML tramite questa finestra di dialogo.  
  
## <a name="statement-completion"></a>Completamento istruzioni  
 **Elenco automatico membri**  
 Quando questa casella di controllo è selezionata, durante la digitazione nell'editor viene visualizzato un elenco di membri, proprietà, valori o metodi disponibili. Scegliere l'elemento desiderato nell'elenco popup per inserirlo nel codice.  
  
 **Nascondi membri avanzati**  
 Questa casella di controllo non è disponibile.  
  
 **Informazioni sui parametri**  
 Se questa casella di controllo è selezionata, la sintassi completa della procedura o dichiarazione corrente viene visualizzata a sinistra del punto di inserimento nell'editor, insieme a tutti i relativi parametri disponibili. Il parametro successivo che può essere assegnato è evidenziato in grassetto.  
  
## <a name="settings"></a>Impostazioni  
 **Abilita spazio virtuale**  
 Se questa casella di testo è selezionata, alla fine di ogni riga del codice verranno inseriti alcuni spazi. Selezionare la casella di controllo per inserire i commenti sempre nel medesimo punto accanto al codice.  
  
 **A capo automatico**  
 Se questa casella di controllo è selezionata, le parti di una riga che si estendono orizzontalmente oltre l'area visibile dell'editor vengono visualizzate automaticamente nella riga successiva. Se si seleziona questa casella di controllo, viene abilitata automaticamente la casella di controllo **Mostra glifi per ritorno a capo automatico** .  
  
 **Mostra icone per ritorno a capo automatico**  
 Se questa casella di controllo è selezionata, viene visualizzato un simbolo di ritorno a capo nel punto in cui una riga lunga va a capo sulla riga successiva. Per non visualizzare questi indicatori, deselezionare la casella di controllo.  
  
> [!NOTE]  
>  I simboli di ritorno a capo non vengono aggiunti al codice, né stampati. Si tratta esclusivamente di elementi di riferimento.  
  
 **Applica comandi Taglia o Copia a righe vuote in assenza di selezione**  
 Questa casella di controllo consente di impostare il comportamento dell'editor nei casi in cui si posiziona il punto di inserimento in una riga vuota senza selezionare alcun elemento e quindi si fa clic su **Copia** o **Taglia**.  
  
 Se la casella di controllo è selezionata, la riga vuota viene copiata o incollata. Se quindi si fa clic su **Incolla**, viene inserita una nuova riga vuota.  
  
 Se la casella di testo è deselezionata, non viene copiato o tagliato alcun elemento. Se quindi si fa clic su **Incolla**, viene incollato il contenuto copiato più di recente. Se non è stata eseguita alcuna operazione di copia, non viene incollato alcun elemento.  
  
 Questa impostazione non ha alcun effetto sui comandi **Copia** o **Taglia** applicati a righe non vuote. Se non è selezionato alcun elemento, viene copiata o tagliata la riga intera. Se quindi si fa clic su **Incolla**, vengono incollati la riga intera e il relativo carattere di ritorno a capo.  
  
## <a name="display"></a>Schermo  
 **Numeri di riga**  
 Se questa casella di controllo è selezionata, accanto a ogni riga del codice viene visualizzato un numero.  
  
> [!NOTE]  
>  I numeri di riga non vengono aggiunti al codice, né stampati. Si tratta esclusivamente di elementi di riferimento.  
  
 **Consenti navigazione URL con clic singolo**  
 Se questa casella di controllo è selezionata, il cursore si trasforma in un puntatore a forma di mano quando viene posizionato su un URL nell'editor. È possibile fare clic sull'URL per visualizzare nel browser la pagina indicata.  
  
 **Barra di navigazione**  
 Questa casella di controllo non è disponibile.  
  
  
