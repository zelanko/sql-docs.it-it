---
title: Effetti delle opzioni ISO | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 442900f22aa408d91175e0a58b9f5b7ca7aceaef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937268"
---
# <a name="effects-of-iso-options"></a>Effetti delle opzioni ISO
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Lo standard ODBC è molto simile allo standard ISO e le applicazioni ODBC presuppongono un comportamento standard da un driver ODBC. Per rendere tale comportamento più conforme a che definito nello standard ODBC, il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client utilizza sempre qualsiasi opzione ISO disponibile nella versione di SQL Server a cui si connette.  
  
 Quando la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client si connette a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], il server rileva che il client utilizza il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client e attiva diverse opzioni.  
  
 Il driver stesso genera queste istruzioni, senza alcuna richiesta da parte dell'applicazione ODBC. L'impostazione di queste opzioni rende più portabili le applicazioni ODBC che utilizzano il driver in quanto il comportamento del server corrisponde allo standard ISO.  
  
 Nelle applicazioni DB-Library in genere queste opzioni non vengono attivate. I siti che osservano diversi tra i client ODBC o DB-Library quando si esegue la stessa istruzione SQL non devono presupporre che questo comportamento indica un problema con il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client. Sono prima di tutto necessario rieseguire l'istruzione nell'ambiente DB-Library con le stesse opzioni SET come viene usata dal [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client.  
  
 Poiché le opzioni SET possono essere attivate e disattivate in qualsiasi momento da utenti e applicazioni, gli sviluppatori di stored procedure e trigger devono testare anche le stored procedure e i trigger con le opzioni SET sopra indicate attivate e disattivate per garantirne il corretto funzionamento indipendentemente dalle opzioni impostate da una connessione specifica quando il trigger o la stored procedure viene richiamata. Un trigger o una stored procedure in cui è necessario impostare una di queste opzioni in modo specifico deve generare un'istruzione SET all'inizio del trigger o della stored procedure stessa. Questa istruzione SET rimarrà attiva soltanto durante l'esecuzione del trigger o della stored procedure. Al completamento della stessa, verrà ripristinata l'impostazione originale.  
  
 Durante la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], viene attivata anche una quarta opzione SET, CONCAT_NULL_YIELDS_NULL. Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client non impostare queste opzioni se AnsiNPW = NO viene specificato nell'origine dati o su [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) oppure [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md).  
  
 Ad esempio le opzioni ISO indicate in precedenza, il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client non attiva l'opzione QUOTED_IDENTIFIER se QuotedID = NO viene specificato nell'origine dati o su **SQLDriverConnect** o  **SQLBrowseConnect**.  
  
 Per consentire al driver di conoscere lo stato corrente delle opzioni SET, le applicazioni ODBC non devono utilizzare l'istruzione SET [!INCLUDE[tsql](../../../includes/tsql-md.md)] per impostarle. Per eseguire questa operazione, infatti, devono utilizzare solo le opzioni dell'origine dati o della connessione. Se l'applicazione genera istruzioni SET, il driver può generare istruzioni SQL errate.  
  
## <a name="see-also"></a>Vedere anche  
 [L'esecuzione di istruzioni &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)   
 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
