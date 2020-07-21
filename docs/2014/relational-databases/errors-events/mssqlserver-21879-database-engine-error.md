---
title: MSSQLSERVER_21879 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21879 (Database Engine error)
ms.assetid: fcfab735-05ca-423a-89f1-fdee7e2ed8c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e0d25394694fae10b2ff6faeb13d0087eb87d7b0
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553466"
---
# <a name="mssqlserver_21879"></a>MSSQLSERVER_21879
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21879|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLErrorNum21879|  
|Testo del messaggio|Impossibile eseguire una query nel server reindirizzato '%s' per il server di pubblicazione originale '%s' e il server di pubblicazione '%s' per determinare il nome del server remoto; errore %d, messaggio di errore '%s.'|  
  
## <a name="explanation"></a>Spiegazione  
 `sp_validate_redirected_publisher` utilizza un server collegato temporaneo creato per connettersi al server di pubblicazione reindirizzato per individuare il nome del server remoto. L'errore 21879 viene restituito in caso di errore della query del server collegato. La chiamata per richiedere il nome del server remoto è in genere il primo utilizzo del server collegato temporaneo, pertanto, se ci sono problemi di connettività, è probabile che si presentino prima con questa chiamata. Questa chiamata remota esegue semplicemente select `@@servername` sul server remoto.  
  
 Il server collegato utilizzato per eseguire la query sul server di pubblicazione reindirizzato utilizza la modalità di sicurezza, l'account di accesso e la password forniti quando viene richiamato `sp_adddistpublisher` per il server di pubblicazione originale.  
  
-   Se l'autenticazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stata utilizzata (modalità di sicurezza 0), l'account di accesso e password specificati vengono utilizzati per connettersi al server remoto.  
  
-   Se è stata utilizzata l'autenticazione di Windows (modalità di sicurezza 1), viene utilizzata una connessione trusted per la connessione.  
  
    -   Se `sp_validate_redirected_publisher` viene chiamato in modo esplicito da un utente, l'account di accesso di Windows con cui è in esecuzione l'utente viene utilizzato per la connessione.  
  
    -   Se il server di pubblicazione `sp_validate_redirected_`viene chiamato da un agente di replica di `sp_get_redirected_publisher`, viene utilizzato l'account di accesso di Windows associato all'agente.  
  
 L'errore 21879 può indicare che `sp_validate_redirected_publisher` è stato chiamato utilizzando un account di accesso che non è conosciuto sul server di pubblicazione di destinazione reindirizzato.  
  
## <a name="user-action"></a>Azione dell'utente  
 Assicurarsi che l'account di accesso dell'autenticazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o l'account di accesso di autenticazione di Windows sia valido su tutte le repliche del gruppo di disponibilità e disponga di autorizzazioni sufficienti per accedere alle tabelle di metadati delle sottoscrizioni (syssubscriptions e sysmergesubscriptions) nel database del server di pubblicazione.  
  
 Vi sono considerazioni particolari da fare quando l'errore 21879 viene restituito da una chiamata a `sp_get_redirected_publisher` iniziato da un agente di replica in esecuzione su un nodo diverso dal database di distribuzione; ad esempio, un agente di merge in esecuzione su un sottoscrittore. Se l'autenticazione di Windows viene utilizzata per la connessione al server di pubblicazione reindirizzato, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere configurato per l'autenticazione Kerberos per stabilire la corretta connessione. Quando viene utilizzata l'autenticazione di Windows e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è configurato per l'autenticazione Kerberos, l'errore 18456 che indica il mancato accesso 'NT AUTHORITY\ANONYMOUS LOGON' viene ricevuto da un agente di merge in esecuzione su un sottoscrittore. Vi sono tre possibili modi di risoluzione di questo problema:  
  
-   Configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'autenticazione Kerberos. Vedere **Autenticazione Kerberos e SQL Server** nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilizzare `sp_changedistpublisher` per modificare la modalità di sicurezza associata al server di pubblicazione originale in MSdistpublishers, nonché per specificare un account di accesso e una password da utilizzare per la connessione.  
  
-   Specificare il parametro della riga di comando *BypassPublisherValidation* nella riga di comando dell'agente di merge per ignorare la convalida quando `sp_get_redirected_publisher` viene chiamato nel server di distribuzione.  
  
  
