---
title: Nuove funzionalità GUI in SSMA per MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0e59e2dc-1e4a-47c0-a5c3-ae7b5f5e469c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c138f76b3c34a378418bb2ba655fa7a2bb5af739
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908817"
---
# <a name="new-gui-features-in-ssma-for-mysql-mysqltosql"></a>Nuove funzionalità dell'interfaccia utente grafica in SSMA per MySQL (MySQLToSQL)
In questo capitolo vengono descritte nuove funzionalità dell'interfaccia utente di SSMA  
  
## <a name="layouts"></a>Layout  
Questa funzionalità consente di scegliere una delle due finestre predefiniti layout o si creare layout personalizzati. Per accedere a sottomenu di layout, puntare ai layout del menu Visualizza. Che consente di scegliere uno dei layout esistente, aggiungere layout corrente o gestire i layout.  
  
### <a name="add-current-layout"></a>Aggiungi Layout corrente  
Per salvare i layout di windows corrente, nel menu Visualizza layout, quindi aggiungere Layout corrente.  
  
### <a name="choose-predefined-layout"></a>Scegliere il layout predefinito  
Per scegliere uno dei layout predefinito, nel menu Visualizza layout, quindi il Layout predefinito o senza finestre di esplorazione. È inoltre possibile utilizzare tasti di scelta rapida Ctrl + Alt + 1 o Ctrl + Alt + 2 per il layout predefinito rispettivamente.  
  
### <a name="choose-user-defined-layout"></a>Scegliere il layout definito dall'utente  
Per scegliere il layout definito dall'utente, puntare ai layout del menu Visualizza, quindi fare clic su uno dei layout definite dall'utente. È anche possibile usare tasti di scelta rapida definiti per il layout.  
  
### <a name="manage-layouts"></a>Gestisci layout  
Per aprire Gestisci layout finestra di dialogo, dal menu Visualizza puntare a layout e fare clic su Gestisci layout. Nella finestra di dialogo Gestisci layout troverai un elenco dei layout esistente sul lato sinistro della finestra di dialogo. Non esiste è possibile selezionare il layout per modificare le relative impostazioni. È anche possibile modificare l'ordine di layout nell'elenco o eliminare il layout usando i pulsanti nella parte superiore nell'elenco. Sul lato destro della finestra di dialogo è possibile modificare le impostazioni di layout seguenti:  
  
-   Nome layout  
  
-   Sincronizzazione degli strumenti di esplorazione di metadati  
  
-   Visibilità e la larghezza delle utilità di origine e destinazione metadati esplorazione  
  
-   Visibilità delle finestre di origine o destinazione e le relative dimensioni  
  
-   Visibilità e l'altezza di windows ausiliario  
  
## <a name="bookmarks"></a>Segnalibri  
Questa funzionalità consente di impostare uno o più segnalibri nell'origine o codice di destinazione, veloce trovare un segnalibro utilizzando i tasti di scelta rapida, gestire i segnalibri con una finestra di dialogo descrittivo.  
  
### <a name="toggle-bookmark"></a>Attiva/Disattiva segnalibro  
È possibile impostare/rimuovere un segnalibro nei modi seguenti:  
  
-   Usare pulsante Attiva/Disattiva segnalibro in primo piano finestra SQL di origine o destinazione  
  
-   Fare clic sull'area grigia a sinistra della finestra di SQL  
  
-   Usare Ctrl + Maiusc +&lt;0..9&gt; per impostare un segnalibro numerato  
  
### <a name="bookmark-navigation"></a>Spostamento di segnalibro  
È possibile eseguire attraverso i segnalibri nei modi seguenti:  
  
-   Usare i pulsanti segnalibro successivo segnalibro precedente nella parte superiore della finestra di SQL  
  
-   Usare Ctrl +&lt;0..9&gt; trovare segnalibro numerato  
  
-   Usare i pulsanti Vai a visualizzazione origine o nella finestra di dialogo di gestire i segnalibri  
  
### <a name="removing-bookmark"></a>Rimozione di segnalibro  
È possibile rimuovere un segnalibro nei modi seguenti:  
  
-   Utilizzare pulsante chiaro nella parte superiore della finestra di SQL per rimuovere tutti i segnalibri nel documento corrente  
  
-   Usare i pulsanti Rimuovi oppure su Rimuovi tutto nella finestra di dialogo di gestire i segnalibri  
  
### <a name="manage-bookmarks"></a>Gestire i segnalibri  
Per aprire la finestra di gestire i segnalibri, dal menu Modifica fare clic su Gestisci segnalibri. Nella finestra di dialogo verrà visualizzato un elenco dei propri segnalibri esistenti. È possibile usare i pulsanti sul lato destro della finestra di dialogo per gestire i segnalibri.  
  
## <a name="object-history"></a>Cronologia dell'oggetto  
La cronologia dell'oggetto interfaccia utente grafica consente i seguenti vantaggi quando si passa gli oggetti:  
  
-   È possibile utilizzare i pulsanti Indietro e Avanti per spostarsi tra gli oggetti che già visitato  
  
-   Quando esegue il backup per l'oggetto, si esegue il stessa scheda che rimasta  
  
-   Quando si torna all'oggetto e la scheda è SQL, eseguire il backup nella stessa posizione del cursore che hanno lasciato  
  
## <a name="advanced-search-capabilities"></a>Funzionalità di ricerca avanzate  
Funzionalità di ricerca avanzate forniscono le funzionalità di ricerca potente e flessibile e consentono di trovare dichiarazione dell'oggetto, ottenere le informazioni sull'oggetto, eseguire una ricerca rapida, eseguire la ricerca in categorie in base a modelli e così via avanzata di oggetti.  
  
### <a name="get-quick-information"></a>Ottenere informazioni rapide  
È possibile ottenere informazioni rapide dell'oggetto in corrispondenza della posizione del cursore nei modi seguenti:  
  
-   Fare clic sul pulsante informazioni rapide nella parte superiore della finestra di SQL  
  
-   Selezionare le informazioni rapide del menu a comparsa del pulsante destro del mouse  
  
-   Premere Ctrl + Maiusc + barra spaziatrice  
  
### <a name="find-declaration"></a>Trovare dichiarazione  
È possibile passare alla dichiarazione dell'oggetto nella posizione del cursore nei modi seguenti:  
  
-   Fare clic sul pulsante Vai a dichiarazione sopra la finestra SQL  
  
-   Selezionare il menu di scelta rapida Vai a dichiarazione  
  
-   Premere F12  
  
### <a name="quick-search"></a>Ricerca rapida  
È possibile eseguire la ricerca veloce usando le funzionalità seguenti:  
  
-   È possibile avviare la ricerca tramite Ctrl + F scelta rapida  
  
-   È possibile ripetere l'ultima ricerca in avanti usando F3  
  
-   È possibile ripetere l'ultima ricerca con le versioni precedenti tramite MAIUSC+F3  
  
-   È possibile trovare l'occorrenza successiva della parola nella posizione del cursore utilizzando Ctrl + F3  
  
-   È possibile trovare l'occorrenza precedente della parola nella posizione del cursore utilizzando Ctrl + MAIUSC + F3  
  
-   È anche possibile eseguire tutte queste azioni con voci di menu.  
  
### <a name="advanced-search"></a>Ricerca avanzata  
Per aprire ricerca avanzata della finestra di dialogo Trova punto menu Modifica, quindi fare clic su ricerca avanzata. Nella finestra di dialogo sarà in grado di trovare qualsiasi oggetto tramite modello. Nella parte superiore della finestra di dialogo è possibile scegliere le categorie di area e l'oggetto di ricerca.  
  
