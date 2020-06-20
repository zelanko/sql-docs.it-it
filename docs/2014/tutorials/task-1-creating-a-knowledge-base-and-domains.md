---
title: 'Attività 1: creazione di una Knowledge base e di domini | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f7ad3b085178c0d0cfe3ece010a571992e7fdb99
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064863"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>Attività 1: Creazione di una Knowledge Base e dei domini
  In questa attività verrà creata la Knowledge base **Suppliers** e verranno creati i domini utilizzati per la pulizia dei dati e la corrispondenza dei dati per rimuovere i duplicati.  
  
1.  Avviare **Data Quality Client**. Fare clic sul pulsante **Start**, scegliere **tutti i programmi**, **Microsoft SQL Server 2012**, fare clic su **Data Quality Services**, quindi su **Data Quality Client**.  
  
2.  Nella finestra di dialogo **Connetti al server** selezionare l'istanza del server di database in cui è installato DQS, quindi fare clic su **Connetti**.  
  
     ![Finestra di dialogo Connetti al server](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "Finestra di dialogo Connetti al server")  
  
3.  Nella home page Data Quality Client, nel riquadro **Gestione Knowledge base** , fare clic su **nuova Knowledge base**.  
  
     ![Gestione Knowledge Base - Nuova KB](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "Gestione Knowledge Base - Nuova KB")  
  
4.  Immettere **Suppliers** per **nome** della Knowledge base.  
  
     ![Nuova Knowledge Base - Gestione dominio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "Nuova Knowledge Base - Gestione dominio")  
  
5.  Verificare che il campo **Crea Knowledge base da** sia impostato su **nessuno** perché la Knowledge base **Suppliers** viene creata da zero.  
  
6.  Verificare che sia selezionata l'opzione **Gestione dominio** per l' **attività** e fare clic su **Avanti**. L'attività Gestione dominio consente di creare e gestire domini nella Knowledge Base.  
  
7.  Nella finestra **Gestione dominio** fare clic sul pulsante della barra degli strumenti **Crea un dominio** per creare un dominio.  
  
     ![Pulsante della barra degli strumenti Crea dominio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "Pulsante della barra degli strumenti Crea dominio")  
  
8.  Nella finestra di dialogo **Crea dominio** digitare **Supplier ID** per il **nome di dominio**e fare clic su **OK**.  
  
     ![Finestra di dialogo Crea dominio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "Finestra di dialogo Crea dominio")  
  
9. Ripetere il passaggio precedente per creare i seguenti domini con tutte le impostazioni predefinite. Per semplificare l'esercitazione, impostare il tipo di **dati** di tutti i domini come **stringa**. Gli altri tipi di dati consentiti sono Integer, Decimal e Data. Quando si seleziona l'opzione **Usa valori iniziali** (impostazione predefinita), tutti i sinonimi vengono sostituiti con il valore principale del gruppo di sinonimi nell'output. L'impostazione dell'opzione **Normalizza stringa** (impostazione predefinita) consente di rimuovere tutti i caratteri speciali nei valori di dominio. L'opzione **Format output to** consente di selezionare la formattazione applicata quando vengono restituiti i valori dei dati nel dominio. Selezionare **Abilita correttore ortografico** (impostazione predefinita) per eseguire il correttore ortografico su tutti i valori stringa durante il popolamento del dominio. L'impostazione della **lingua** specifica la versione della lingua del **correttore ortografico** che si desidera applicare. Selezionare **Disabilita algoritmi di errore sintassi** per popolare il dominio senza verificare la presenza di errori di sintassi nei valori stringa. Per ulteriori informazioni, vedere l'argomento relativo alla [creazione di un dominio](https://msdn.microsoft.com/library/hh510401.aspx) in MSDN Library.  
  
    -   Supplier Name  
  
    -   Indirizzo di posta elettronica del contatto  
  
    -   Riga indirizzo  
  
    -   city  
  
    -   State  
  
    -   Country  
  
    -   Zip  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 2: Aggiunta manuale di valori di dominio](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
