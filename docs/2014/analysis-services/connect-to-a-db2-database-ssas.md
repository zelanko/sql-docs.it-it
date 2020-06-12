---
title: Connettersi a un database DB2 (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.conndb2db.f1
ms.assetid: eeef3697-a4fd-4263-ba7e-f86afa1f46cc
author: minewiskan
ms.author: owend
ms.openlocfilehash: 03c98f3ab44a4a9f3aac91be36f3d704a3f796ab
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527217"
---
# <a name="connect-to-a-db2-database-ssas"></a>Connettersi a un database di DB2 (SSAS)
  Questa pagina dell' **Importazione guidata tabella** consente di specificare le impostazioni per connettersi a un database di DB2. Per accedere alla procedura guidata da [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], dal menu **Modello** selezionare **Importa da origine dati**.  
  
 Per connettersi a un'origine dati, è necessario che nel computer sia installato il provider appropriato.  
  
> [!NOTE]  
>  In caso di selezione di un database in questa pagina, vengono utilizzate le credenziali dell'utente specificate. Tuttavia, l'importazione non verrà completata se l'utente specificato nella pagina Impostazioni di rappresentazione non dispone di privilegi sufficienti per leggere dal database selezionato.  
  
## <a name="ui-element-list"></a>Elenco elementi dell'interfaccia utente  
 **Nome descrittivo connessione**  
 Digitare un nome univoco per questa connessione all'origine dati. Questo campo è obbligatorio.  
  
 **Nome server**  
 Digitare o selezionare l'istanza del server a cui connettersi.  
  
 **Nome utente**  
 Specificare un nome utente per la connessione al database.  
  
 Questo nome utente viene utilizzato quando si crea la stringa di connessione per l'origine dati. Queste credenziali vengono utilizzate anche in caso di visualizzazione in anteprima e filtro dei dati nella finestra Proprietà tabella e nell'Importazione guidata. Non vengono utilizzate per importare o aggiornare dati; in tal caso vengono infatti utilizzate le credenziali di Windows specificate nella pagina Impostazioni di rappresentazione.  
  
 **Password**  
 Specificare una password per la connessione al database.  
  
 **Salva password**  
 Specificare se la password immessa nella casella **Password** è stata archiviata.  
  
 **Nome database**  
 Selezionare un database dall'elenco di database.  
  
 **Raccolta pacchetti**  
 Specificare il nome della raccolta per i pacchetti di DB2. Un provider utilizza i pacchetti per creare istruzioni SQL e chiamare stored procedure.  
  
 **Schema predefinito**  
 Specificare il nome dello schema predefinito per il database selezionato.  
  
 **Avanzate**  
 Impostare altre proprietà relative alla connessione tramite la finestra di dialogo **Impostazione delle proprietà avanzate** .  
  
 **Test connessione**  
 Provare a stabilire una connessione all'origine dati utilizzando le impostazioni correnti. Viene visualizzato un messaggio che indica se la connessione è stata stabilita.  
  
  
