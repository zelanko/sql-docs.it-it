---
title: Connettersi a un database di Microsoft SQL Server (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlserverdb.f1
ms.assetid: 6ebfe029-dbba-4f0d-a556-328e79ef629f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc3530c7bc316c0dbdc3271d456d4f7adf05038a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087222"
---
# <a name="connect-to-a-microsoft-sql-server-database-ssas"></a>Connessione a un database di Microsoft SQL Server (SSAS)
  Questa pagina dell' **Importazione guidata tabella** consente di specificare le impostazioni per connettersi a un database di Microsoft SQL Server. Per accedere alla procedura guidata da [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], dal menu **Modello** selezionare **Importa da origine dati**.  
  
 Per connettersi a un'origine dati, è necessario che nel computer sia installato il provider appropriato.  
  
> [!NOTE]  
>  Le credenziali dell'utente corrente vengono utilizzate in caso di selezione di un database in questa pagina. Tuttavia, l'importazione non verrà completata se l'utente specificato nella pagina Impostazioni di rappresentazione non dispone di privilegi sufficienti per leggere dal database selezionato.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Nome descrittivo connessione**  
 Digitare un nome univoco per questa connessione all'origine dati. Questo campo è obbligatorio.  
  
 **Nome server**  
 Selezionare il nome o digitare il nome o l'indirizzo IP dell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a cui connettersi.  
  
 Per specificare il server locale, è possibile digitare un punto (.), (locale) o localhost.  
  
 **Usa autenticazione di Windows**  
 Specificare se usare l'autenticazione di Windows per connettersi a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 L'autenticazione di Windows consente a un utente di connettersi tramite un account utente di Windows. Se possibile, è consigliabile utilizzare l'autenticazione di Windows.  
  
 Quando viene utilizzato questo tipo di autenticazione, le credenziali dell'utente corrente vengono utilizzate in caso di visualizzazione in anteprima e filtro dei dati nella finestra Proprietà tabella e nell'Importazione guidata. Tali credenziali non vengono utilizzate per importare o aggiornare dati; in tal caso vengono infatti utilizzate le credenziali di Windows specificate nella pagina Impostazioni di rappresentazione.  
  
 **Usa autenticazione SQL Server**  
 Specificare se usare l'autenticazione di SQL Server per connettersi a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Con questo tipo di autenticazione, in SQL Server l'autenticazione viene eseguita verificando che sia stato impostato un account di accesso di SQL Server e che la password specificata corrisponda a quella registrata in precedenza.  
  
 L'autenticazione di SQL Server viene utilizzata quando si crea la stringa di connessione per l'origine dati. Queste credenziali vengono utilizzate anche in caso di visualizzazione in anteprima e filtro dei dati nella finestra Proprietà tabella e nell'Importazione guidata. Non vengono utilizzate per importare o aggiornare dati; in tal caso vengono infatti utilizzate le credenziali di Windows specificate nella pagina Impostazioni di rappresentazione.  
  
 **Nome utente**  
 Specificare un nome utente per la connessione al database. Questa opzione è disponibile solo se è stata selezionata l'autenticazione di SQL Server per la connessione.  
  
 **Password**  
 Specificare una password per la connessione al database. Questa opzione è modificabile solo se è stata selezionata l'autenticazione di SQL Server per la connessione.  
  
 **Salva password**  
 Specificare se archiviare la password immessa nella casella **Password** . Questa opzione è disponibile solo se è stata selezionata l'autenticazione di SQL Server per la connessione.  
  
 **Nome database**  
 Selezionare un database dall'elenco di database.  
  
 **Funzionalità avanzate**  
 Per impostare ulteriori proprietà della connessione, utilizzare la finestra di dialogo **Imposta proprietà avanzate** . Per altre informazioni, vedere [Impostazione delle proprietà avanzate &#40;SSAS&#41;](set-advanced-properties-ssas.md).  
  
 **Test connessione**  
 Provare a stabilire una connessione all'origine dati utilizzando le impostazioni correnti. Viene visualizzato un messaggio che indica se la connessione è stata stabilita.  
  
  
