---
title: 'Attività 1: Creazione di una Knowledge Base e domini | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: eeaebadd43fe1969ae1c728f8e2f8284ddf7f7ac
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011102"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>Attività 1: Creazione di una Knowledge Base e dei domini
  In questa attività si crea il **Suppliers** della knowledge base e i domini che viene usato per la corrispondenza dei dati e pulizia dei dati per rimuovere i duplicati.  
  
1.  Avvio veloce **Client Data Quality**. Fare clic su **avviare**, scegliere **tutti i programmi**, fare clic su **Microsoft SQL Server 2012**, fare clic su **Data Quality Services**, quindi fare clic su  **Client Data Quality**.  
  
2.  Nel **Connetti al Server** finestra di dialogo, selezionare l'istanza di server di database in cui è installato DQS e fare clic su **Connect**.  
  
     ![Connettersi al Server Dialog Box](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "connettersi alla finestra di dialogo Server")  
  
3.  In Data Quality Client home page di **Gestione Knowledge Base** riquadro, fare clic su **nuova Knowledge Base**.  
  
     ![Gestione Knowledge Base - nuova KB](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "Gestione Knowledge Base - nuova KB")  
  
4.  Immettere **Suppliers** per **nome** della knowledge base.  
  
     ![Nuova Knowledge Base - Gestione dominio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "nuova Knowledge Base - Gestione dominio")  
  
5.  Verificare che **crea Knowledge Base da** campo è impostato su **None** poiché si sta creando il **Suppliers** della knowledge base da zero.  
  
6.  Verificare che **Gestione dominio** sia selezionata per il **attività** e fare clic su **Next**. L'attività Gestione dominio consente di creare e gestire domini nella Knowledge Base.  
  
7.  Nel **Gestione dominio** finestra, fare clic su **creare un dominio** pulsante della barra degli strumenti per creare un dominio.  
  
     ![Pulsante Crea dominio sulla barra degli strumenti](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "pulsante Crea dominio sulla barra degli strumenti")  
  
8.  Nel **crea dominio** finestra di dialogo, digitare **Supplier ID** per il **nome di dominio**, fare clic su **OK**.  
  
     ![Dialogo Crea dominio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "dialogo Crea dominio")  
  
9. Ripetere il passaggio precedente per creare i seguenti domini con tutte le impostazioni predefinite. Per mantenere semplice l'esercitazione, si imposta la **tipo di dati** di tutti i domini come **stringa**. Gli altri tipi di dati consentiti sono: Integer, Decimal e Date. Quando la **utilizza valori iniziali** opzione è selezionata (impostazione predefinita), tutti i sinonimi vengono sostituiti con il valore iniziale del gruppo di sinonimi nell'output. L'impostazione **Normalizza stringa** opzione (predefinito) Rimuove i caratteri speciali nei valori di dominio. Il **formato Output in** opzione consente di selezionare la formattazione che viene applicato quando i valori dei dati nel dominio. Selezionare **Abilita correttore ortografico** (predefinito) per eseguire correttore ortografico su tutti i valori stringa durante l'inserimento nel dominio. Il **Language** impostazione consente di specificare la versione di lingua le **correttore ortografico** da applicare. Selezionare **Disabilita algoritmi di errore di sintassi** per popolare il dominio senza verificare i valori di stringa per gli errori di sintassi. Visualizzare [creare un dominio](https://msdn.microsoft.com/library/hh510401.aspx) argomento in MSDN library per altri dettagli.  
  
    -   Supplier Name  
  
    -   Contact Email  
  
    -   Riga indirizzo  
  
    -   Città  
  
    -   State  
  
    -   Country  
  
    -   CAP  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 2: Aggiunta manuale di valori di dominio](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
