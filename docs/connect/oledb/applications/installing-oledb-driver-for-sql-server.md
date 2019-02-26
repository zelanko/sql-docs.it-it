---
title: Installazione del driver OLE DB per SQL Server| Microsoft Docs
description: Installazione e la disinstallazione del Driver OLE DB per SQL Server
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, uninstalling
- MSOLEDBSQL, installing
- MSOLEDBSQL, uninstalling
- Setup [OLE DB Driver for SQL Server]
- uninstalling OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], uninstalling OLE DB Driver for SQL Server
- installing OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, installing
- data access [OLE DB Driver for SQL Server], installing OLE DB Driver for SQL Server
- removing OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 288b81c508eed681be190749b5d9618f1f5511ce
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744381"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>Installazione del driver OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Per installare il Driver OLE DB per SQL Server è necessario msoledbsql.msi programma di installazione.
Eseguire il programma di installazione ed effettuare la scelta preferita. Il Driver OLE DB per SQL Server può essere installata side-by-side con versioni precedenti di provider Microsoft OLE DB.

Il Driver OLE DB per i file di SQL Server (msoledbsql.dll, msoledbsqlr.rll) vengono installati `%SYSTEMROOT%\system32\` . Inoltre, x64 msoledbsql.msi installa i file binari a 32 bit in `%SYSTEMROOT%\SysWOW64\`.

> [!NOTE]  
> Tutte le impostazioni del Registro di sistema appropriati per il Driver OLE DB per SQL Server vengono eseguite come parte del processo di installazione.  

Il Driver OLE DB per SQL Server libreria di file di intestazione e (msoledbsql.h e msoledbsql.lib) vengono installati `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`. Inoltre, x64 msoledbsql.msi installa i file stesso in `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`.  

È possibile distribuire il Driver OLE DB per SQL Server con msoledbsql.msi. Potrebbe essere necessario installare i Driver OLE DB per SQL Server quando si distribuisce un'applicazione. Un modo per installare più pacchetti in un'installazione che all'utente può sembrare singola consiste nell'usare la tecnologia del chainer e del programma di avvio automatico. Per ulteriori informazioni, vedere [Authoring a Custom Bootstrapper Package for Visual Studio 2005](https://go.microsoft.com/fwlink/?LinkId=115667) (informazioni in lingua inglese) e [Aggiunta di prerequisiti personalizzati](https://go.microsoft.com/fwlink/?LinkId=115668).  
  
X64 msoledbsql.msi installa anche la versione a 32 bit del Driver OLE DB per SQL Server. Se l'applicazione è destinata a una piattaforma diversa da quella che in cui è stata sviluppata, è possibile scaricare le versioni di msoledbsql.msi per x64 e x86.

Quando si richiama msoledbsql.msi, solo i componenti client vengono installati per impostazione predefinita. I componenti client sono file che supportano l'esecuzione di un'applicazione sviluppata tramite il driver OLE DB per SQL Server. Per installare i componenti SDK, specificare `ADDLOCAL=All` sulla riga di comando. Ad esempio  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>Installazione invisibile all'utente  
 Se si utilizza l'opzione /passive, /qn, /qb o /qr con msiexec, è necessario specificare anche IACCEPTMSOLEDBSQLLICENSETERMS=YES per indicare in modo esplicito l'accettazione delle condizioni di licenza dell'utente finale. È necessario specificare questa opzione in lettere maiuscole.  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>Installazione Driver OLE DB per SQL Server come dipendenza  
È importante non disinstallare il Driver OLE DB per SQL Server fino a quando tutte le applicazioni dipendenti vengono disinstallate. Per fornire agli utenti con un avviso che l'applicazione dipende dal Driver OLE DB per SQL Server, usare l'opzione di installazione APPGUID in MSI, come indicato di seguito:  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

Il valore passato a APPGUID è il codice prodotto specifico. Quando si utilizza Microsoft Installer per aggregare il programma di installazione dell'applicazione, è necessario creare un codice prodotto.
L'opzione APPGUID richiede l'esecuzione del programma di installazione da un prompt dei comandi con privilegi elevati.

## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con il driver OLE DB per SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
