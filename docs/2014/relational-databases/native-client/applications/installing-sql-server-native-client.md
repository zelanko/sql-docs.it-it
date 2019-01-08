---
title: Installazione di SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, uninstalling
- SQLNCLI, installing
- SQLNCLI, uninstalling
- Setup [SQL Server Native Client]
- uninstalling SQL Server Native Client
- data access [SQL Server Native Client], uninstalling SQL Server Native Client
- installing SQL Server Native Client
- SQL Server Native Client, installing
- data access [SQL Server Native Client], installing SQL Server Native Client
- removing SQL Server Native Client
ms.assetid: c6abeab2-0052-49c9-be79-cfbc50bff5c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71438a61dcaec201d0b3ae21eb7e27d979029204
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363023"
---
# <a name="installing-sql-server-native-client"></a>Installazione di SQL Server Native Client
  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 viene installato con [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. Non esistono versioni di [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client. Per altre informazioni, vedere [What ' s New in SQL Server Native Client](../sql-server-native-client.md). È anche possibile ottenere sqlncli.msi dalla pagina Web di SQL Server 2012 Feature Pack. Per scaricare la versione più recente di SQL Server Native Client, passare a [Microsoft? SQL Server? 2012 SP2 Feature Pack](https://www.microsoft.com/en-us/download/details.aspx?id=43339). Se nel computer è installata anche una versione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client precedente a SQL Server 2012, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 verrà installato side-by-side con la versione precedente.  
  
 I file di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli11.dll, sqlnclir11.rll e s11ch_sqlncli.chm) vengono installati nel percorso seguente:  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  Tutte le impostazioni del Registro di sistema appropriate per il provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client vengono definite nel corso del processo di installazione.  
  
 I file di intestazione e di libreria di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h e sqlncli11.lib) vengono installati nel percorso seguente:  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 Oltre a installare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client durante l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è disponibile un programma di installazione ridistribuibile denominato sqlncli.msi contenuto nel disco di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel percorso seguente: `%CD%\Setup\`.  
  
 È possibile distribuire [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client tramite sqlncli.msi. Potrebbe essere necessario installare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client quando si distribuisce un'applicazione. Un modo per installare più pacchetti in un'installazione che all'utente può sembrare singola consiste nell'usare la tecnologia del chainer e del programma di avvio automatico. Per ulteriori informazioni, vedere [Authoring a Custom Bootstrapper Package for Visual Studio 2005](https://go.microsoft.com/fwlink/?LinkId=115667) (informazioni in lingua inglese) e [Aggiunta di prerequisiti personalizzati](https://go.microsoft.com/fwlink/?LinkId=115668).  
  
 Le versioni x64 e Itanium di sqlncli.msi installano anche la versione a 32 bit di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Se l'applicazione è destinata a una piattaforma diversa da quella su cui è stata sviluppata, è possibile scaricare versioni di sqlncli.msi per x64, Itanium e x86 dall'Area download Microsoft.  
  
 Quando si richiama sqlncli.msi, solo i componenti client vengono installati per impostazione predefinita. I componenti client sono file che supportano l'esecuzione di un'applicazione sviluppata tramite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Per installare i componenti SDK, specificare `ADDLOCAL=All` sulla riga di comando. Ad esempio:  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>Installazione invisibile all'utente  
 Se si utilizza l'opzione /passive, /qn, /qb o /qr con msiexec, è necessario specificare anche IACCEPTSQLNCLILICENSETERMS=YES per indicare in modo esplicito l'accettazione delle condizioni di licenza dell'utente finale. È necessario specificare questa opzione in lettere maiuscole.  
  
## <a name="uninstalling-sql-server-native-client"></a>Disinstallazione di SQL Server Native Client  
 Poiché le applicazioni, ad esempio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] server e il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] strumenti dipendono [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, è importante non disinstallare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client finché tutte le applicazioni dipendenti vengono disinstallate. Per gli utenti del provider con un avviso indicante che l'applicazione dipende [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, utilizzare l'opzione di installazione APPGUID in MSI, come indicato di seguito:  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 Il valore passato a APPGUID è il codice prodotto specifico. Quando si utilizza Microsoft Installer per aggregare il programma di installazione dell'applicazione, è necessario creare un codice prodotto.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di applicazioni con SQL Server Native Client](installing-sql-server-native-client.md)   
 [Procedure per l'installazione](../../../sql-server/install/installation-how-to-topics.md)  
  
  
