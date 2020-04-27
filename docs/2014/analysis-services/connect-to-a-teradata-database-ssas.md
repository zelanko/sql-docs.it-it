---
title: Connettersi a un database Teradata (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connterradb.f1
ms.assetid: 875ad4a3-a2b3-4b68-8c1c-6507e9f25b4d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc6712598452b1957857509e6b3ff6f659a16c4b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087192"
---
# <a name="connect-to-a-teradata-database-ssas"></a>Connessione a un database di Teradata (SSAS)
  Questa pagina dell' **Importazione guidata tabella** consente di specificare le impostazioni per connettersi a un database Teradata. Per accedere alla procedura guidata da [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], dal menu **Modello** selezionare **Importa da origine dati**.  
  
 Per connettersi a un'origine dati, è necessario che nel computer sia installato il provider appropriato.  
  
> [!NOTE]  
>  Le credenziali dell'utente corrente vengono utilizzate in caso di selezione di un database in questa pagina. Tuttavia, l'importazione non verrà completata se l'utente specificato nella pagina Impostazioni di rappresentazione non dispone di privilegi sufficienti per leggere dal database selezionato.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Nome descrittivo connessione**  
 Digitare un nome univoco per questa connessione all'origine dati. Questo campo è obbligatorio.  
  
 **Nome server**  
 Digitare o selezionare il nome dell'istanza del server a cui connettersi.  
  
 **Nome utente**  
 Specificare un nome utente per la connessione al database.  
  
 Questo nome utente viene utilizzato quando si crea la stringa di connessione per l'origine dati. Queste credenziali vengono utilizzate anche in caso di visualizzazione in anteprima e filtro dei dati nella finestra Proprietà tabella e nell'Importazione guidata. Tali credenziali non vengono utilizzate per importare o aggiornare dati; in tal caso vengono infatti utilizzate le credenziali di Windows specificate nella pagina Impostazioni di rappresentazione.  
  
 **Password**  
 Specificare una password per la connessione al database.  
  
 **Salva password**  
 Specificare se la password immessa nella casella **Password** è deve essere archiviata.  
  
 **Avanzate**  
 Per impostare ulteriori proprietà della connessione, utilizzare la finestra di dialogo **Imposta proprietà avanzate** . Per altre informazioni, vedere [Impostazione delle proprietà avanzate &#40;SSAS&#41;](set-advanced-properties-ssas.md).  
  
 **Test connessione**  
 Provare a stabilire una connessione all'origine dati utilizzando le impostazioni correnti. Viene visualizzato un messaggio che indica se la connessione è stata stabilita.  
  
  
