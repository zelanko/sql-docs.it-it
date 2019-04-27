---
title: Impostazioni (sincronizzazione) (SybaseToSQL) del progetto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0a221d5c24606707ba9876e0980e6c28d2dacc67
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62667982"
---
# <a name="project-settings-synchronization-sybasetosql"></a>Impostazioni del progetto (sincronizzazione) (SybaseToSQL)
La pagina di sincronizzazione del **impostazioni del progetto** finestra di dialogo contiene impostazioni che consentono di personalizzare la modalità SSMA carica gli oggetti di database, ad esempio tabelle e stored procedure, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
È possibile accedere a due diverse pagine di sincronizzazione che contengono le stesse impostazioni:  
  
-   Se si desidera specificare le impostazioni per tutti i progetti SSMA futuri, nel **degli strumenti** dal menu **impostazioni di progetto predefinite**, selezionare il tipo di progetto di migrazione per cui sono richiesti da visualizzare o modificare le impostazioni dal **versione di destinazione della migrazione** elenco a discesa e quindi selezionare **sincronizzazione** nella parte inferiore del riquadro di sinistra.  
  
-   Per specificare le impostazioni per il progetto corrente, il **strumenti** dal menu **le impostazioni del progetto**e quindi selezionare **sincronizzazione** nella parte inferiore del riquadro di sinistra.  
  
## <a name="options"></a>Opzioni  
**Tentativi**  
Specifica il numero di tentativi di SSMA deve apportare durante il caricamento di oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Gli oggetti che non vengono caricati nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel tentativo di corrente verrà ritentata fino a quando non SSMA raggiunge il numero massimo di tentativi durante il processo di sincronizzazione corrente.  
  
## <a name="synchronization-for-sql-server"></a>Sincronizzazione per SQL Server  
**Aggiornare un oggetto locale in caso di modifica di oggetti locali e remoti**  
Specifica se SSMA necessario sostituire i metadati dell'oggetto locale con i metadati dell'oggetto remoto se entrambi gli oggetti locali e remoti vengono modificati.  
Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
Se si seleziona **scrivere Database**, SSMA aggiornerà gli oggetti del database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.   
Set di opzioni predefinito è **scrivere nel Database.**  
  
**Aggiornare un oggetto locale in caso di modifica oggetto locale**  
Specifica se SSMA necessario sostituire i metadati dell'oggetto locale con i metadati dell'oggetto remoto se viene modificato l'oggetto remoto.  
Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
Se si seleziona **scrivere Database**, SSMA aggiornerà l'oggetto nel database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.   
Set di opzioni predefinito è **scrivere Database**.  
  
**Aggiornare un oggetto locale in caso di modifica di oggetti remoti**  
Specifica se SSMA necessario sostituire i metadati dell'oggetto locale con i metadati dell'oggetto remoto se viene modificato l'oggetto remoto.  
Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
Se si seleziona **scrivere Database**, SSMA aggiornerà l'oggetto nel database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.   
Set di opzioni predefinito è **aggiornare dal Database**.  
  
**Aggiornamento quando i metadati degli oggetti locali sono mancanti**  
Specifica se SSMA deve creare i metadati locali se è presente un oggetto nel database di destinazione, ma non in locale.  
Se si seleziona **aggiornare dal Database**, SSMA consente di selezionare l'aggiornamento dall'opzione di Database quando viene soddisfatta la condizione.  
Se si seleziona **scrivere Database**, SSMA eliminerà l'oggetto dal database quando viene soddisfatta la condizione.  
Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.   
Set di opzioni predefinito è **aggiornare dal Database**.  
  
