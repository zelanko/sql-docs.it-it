---
title: Installazione di SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
author: MightyPen
ms.author: genemi
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 677450c306cdd85f3fec34b09ab8da9b45181844
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73788452"
---
# <a name="installing-sql-server-native-client"></a>Installazione di SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]


  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 viene installato con [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]. 
 
 Non esiste SQL Server 2016 Native Client. Per ulteriori informazioni, vedere [SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client.md). 
 
È anche possibile ottenere sqlncli.msi dalla pagina Web di SQL Server 2012 Feature Pack. Per scaricare la versione più recente del SQL Server Native Client, passare a [Microsoft® SQL Server® 2012 Feature Pack](https://www.microsoft.com/download/confirmation.aspx?id=29065). Se nel computer è installata [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anche una versione precedente di Native Client precedente a SQL Server 2012, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11,0 verrà installato side-by-side con la versione precedente.  
  
 I file di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli11.dll, sqlnclir11.rll e s11ch_sqlncli.chm) vengono installati nel percorso seguente:  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  Tutte le impostazioni del Registro di sistema appropriate per il provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client vengono definite nel corso del processo di installazione.  
  
 I file di intestazione e di libreria di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h e sqlncli11.lib) vengono installati nel percorso seguente:  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 Oltre a installare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client durante l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è disponibile un programma di installazione ridistribuibile denominato sqlncli.msi contenuto nel disco di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel percorso seguente: `%CD%\Setup\`.  
  
 È possibile distribuire [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client tramite sqlncli.msi. Potrebbe essere necessario installare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client quando si distribuisce un'applicazione. Un modo per installare più pacchetti in un'installazione che all'utente può sembrare singola consiste nell'usare la tecnologia del chainer e del programma di avvio automatico. Per altre informazioni, vedere [creazione di un pacchetto di programma di avvio automatico personalizzato per Visual Studio 2005](https://go.microsoft.com/fwlink/?LinkId=115667) e [aggiunta di prerequisiti personalizzati](https://go.microsoft.com/fwlink/?LinkId=115668).  
  
 Le versioni x64 e Itanium di sqlncli.msi installano anche la versione a 32 bit di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Se l'applicazione è destinata a una piattaforma diversa da quella su cui è stata sviluppata, è possibile scaricare versioni di sqlncli.msi per x64, Itanium e x86 dall'Area download Microsoft.  
  
 Quando si richiama sqlncli.msi, solo i componenti client vengono installati per impostazione predefinita. I componenti client sono file che supportano l'esecuzione di un'applicazione sviluppata utilizzando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Per installare i componenti SDK, specificare `ADDLOCAL=All` sulla riga di comando. Ad esempio:  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>Installazione invisibile all'utente  
 Se si utilizza l'opzione /passive, /qn, /qb o /qr con msiexec, è necessario specificare anche IACCEPTSQLNCLILICENSETERMS=YES per indicare in modo esplicito l'accettazione delle condizioni di licenza dell'utente finale. È necessario specificare questa opzione in lettere maiuscole.  
  
## <a name="uninstalling-sql-server-native-client"></a>Disinstallazione di SQL Server Native Client  
 Poiché le applicazioni come [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] server e gli [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] strumenti dipendono [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da Native client, è importante non disinstallare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client finché tutte le applicazioni dipendenti non vengono disinstallate. Per consentire agli utenti di eseguire il provider con un avviso che [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] l'applicazione dipende da Native client, usare l'opzione di installazione APPGUID nell'identità del servizio gestito, come indicato di seguito:  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 Il valore passato a APPGUID è il codice prodotto specifico. Quando si utilizza Microsoft Installer per aggregare il programma di installazione dell'applicazione, è necessario creare un codice prodotto.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)   
 [Procedure per l'installazione](https://msdn.microsoft.com/library/59de41e7-557f-462a-8914-53ec35496baa)  
  
  
