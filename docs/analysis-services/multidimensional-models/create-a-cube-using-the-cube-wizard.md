---
title: Creare un cubo mediante la creazione guidata cubo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d682ada2175d94f7b077bfe06626885862d45e21
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209087"
---
# <a name="create-a-cube-using-the-cube-wizard"></a>Creare un cubo mediante la Creazione guidata cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  È possibile creare un nuovo cubo usando la Creazione guidata cubo in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="to-create-a-new-cube"></a>Per creare un nuovo cubo  
  
1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **Cubi**e quindi scegliere **Nuovo cubo**.  
  
2.  Nella pagina **Selezione metodo di creazione** della Creazione guidata cubo selezionare **Usa tabelle esistenti**e quindi fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  Si potrebbe dovere creare occasionalmente un cubo senza utilizzare le tabelle esistenti. Per creare un cubo vuoto, selezionare **Crea un cubo vuoto**. Per generare tabelle, selezionare **Genera tabelle nell'origine dati**.  
  
3.  Nella pagina **Selezione tabelle del gruppo di misure** eseguire le operazioni seguenti:  
  
    1.  Nell'elenco **Vista origine dati** selezionare una vista origine dati.  
  
    2.  Nell'elenco **Tabelle del gruppo di misure** selezionare le tabelle che verranno usate per creare gruppi di misure.  
  
    3.  Fare clic su **Avanti**.  
  
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
  
  
