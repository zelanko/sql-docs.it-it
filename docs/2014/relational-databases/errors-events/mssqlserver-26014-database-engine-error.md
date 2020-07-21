---
title: MSSQLSERVER_26014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 26014 (Database Engine error)
ms.assetid: e2b0dfc7-0681-4e5d-8875-1d5f63534086
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2c2f74c91293e624e7b66cbdd1238fd1cca450ff
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551876"
---
# <a name="mssqlserver_26014"></a>MSSQLSERVER_26014
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|26014|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SNI_SSL_USER_CERT_FAILURE|  
|Testo del messaggio|Impossibile caricare il certificato specificato dall'utente [Cert Hash(sha1) "%hs"]. Il server non accetterà la connessione. Verificare che il certificato sia installato in modo corretto. Vedere la sezione relativa alla configurazione dei certificati per l'utilizzo con SSL nella documentazione online.|  
  
## <a name="explanation"></a>Spiegazione  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato eseguito un tentativo di caricare il certificato indicato nel messaggio, ma l'operazione non è riuscita. Prima che in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia possibile utilizzare questo certificato, è necessario risolvere il problema.  
  
 Alcune cause possibili dell'errore sono le seguenti:  
  
-   È possibile che il certificato sia stato spostato o eliminato.  
  
-   Se l'account di accesso utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato modificato, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbero non essere disponibili le autorizzazioni per accedere al certificato.  
  
-   Il certificato potrebbe essere scaduto.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare che certificato indicato nel messaggio esista nel sistema, che sia accessibile e che sia valido per l'utilizzo.  
  
  
