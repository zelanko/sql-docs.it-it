---
title: Creare un cubo mediante la creazione guidata cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], creating
ms.assetid: d46d659c-3a4e-4364-94ac-f5eb6ba0ec25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7ffd5880120184249d89c4d702b30c8d6e01e1f6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66076497"
---
# <a name="create-a-cube-using-the-cube-wizard"></a>Creare un cubo mediante la Creazione guidata cubo
  È possibile creare un nuovo cubo usando la Creazione guidata cubo in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="to-create-a-new-cube"></a>Per creare un nuovo cubo  
  
1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **Cubi**e quindi scegliere **Nuovo cubo**.  
  
2.  Nella pagina **Selezione metodo di creazione** della Creazione guidata cubo selezionare **Usa tabelle esistenti**e quindi fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  Si potrebbe dovere creare occasionalmente un cubo senza utilizzare le tabelle esistenti. Per creare un cubo vuoto, selezionare **Crea un cubo vuoto**. Per generare tabelle, selezionare **Genera tabelle nell'origine dati**.  
  
3.  Nella pagina **Selezione tabelle del gruppo di misure** eseguire le operazioni seguenti:  
  
    1.  Nell'elenco **Vista origine dati** selezionare una vista origine dati.  
  
    2.  Nell'elenco **Tabelle del gruppo di misure** selezionare le tabelle che verranno usate per creare gruppi di misure.  
  
    3.  Scegliere **Avanti**.  
  
4.  Nella pagina **Selezione misure** selezionare le misure da includere nel cubo e quindi fare clic su **Avanti**.  
  
     Facoltativamente è possibile modificare i nomi delle misure e dei gruppi di misure.  
  
5.  Nella pagina **Selezione dimensioni esistenti** selezionare le dimensioni esistenti da includere nel cubo e quindi fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  La pagina **Selezione dimensioni esistenti** viene visualizzata se per alcuni dei gruppi di misure selezionati esistono già dimensioni.  
  
6.  Nella pagina **Selezione nuove dimensioni** selezionare le nuove dimensioni da creare e quindi fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  La pagina **Selezione nuove dimensioni** viene visualizzata se una o più delle tabelle sono idonee per le tabelle delle dimensioni e non sono state già usate da dimensioni esistenti.  
  
7.  Nella pagina **Selezione chiavi della dimensione mancanti** selezionare una chiave per la dimensione e quindi fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  La pagina **Selezione chiavi della dimensione mancanti** viene visualizzata se per una o più delle tabelle delle dimensioni specificate non è stata definita alcuna chiave.  
  
8.  Nella pagina **Completamento procedura guidata** assegnare un nome al nuovo cubo e quindi esaminare la struttura del cubo. Per apportare modifiche, fare clic su **Indietro**. In caso contrario, fare clic su **Fine**.  
  
    > [!NOTE]  
    >  È possibile utilizzare Progettazione cubi al termine della procedura guidata per la configurazione dei cubi. È inoltre possibile utilizzare Progettazione dimensioni per aggiungere, rimuovere e configurare attributi e gerarchie nelle dimensioni create.  
  
  
