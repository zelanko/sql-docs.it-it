---
title: SQL Server Express LocalDB intestazione e le informazioni sulla versione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apilocation:
- sqluserinstance.dll
ms.assetid: 506b5161-b902-4894-b87b-9192d7b1664a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b8a873fbc1b5031d6f26f0a3809675276c7806fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021996"
---
# <a name="sql-server-express-localdb-header-and-version-information"></a>Informazioni sulla versione e intestazione del database locale di SQL Server Express
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Non esiste alcun file di intestazione separato per l'API dell'istanza del database locale di SQL Server Express. Le firme e i codici di errore della funzione del database locale sono definiti nel file di intestazione (sqlncli.h) di SQL Server Native Client. Per utilizzare l'API dell'istanza del database locale, è necessario includere il file di intestazione sqlncli.h nel progetto.  
  
## <a name="localdb-versioning"></a>Controllo delle versioni del database locale  
 Per l'installazione del database locale viene utilizzato un solo set di file binari per la versione di SQL Server principale. Queste versioni del database locale sono gestite e installate con patch in modo indipendente. Pertanto, l'utente deve specificare quale versione di base (ovvero, versione di SQL Server principale) del database locale utilizzerà. La versione specificata nel formato della versione standard definito da .NET Framework **Version** classe:  
  
 *major.minor[.build[.revision]]*  
  
 I primi due numeri nella stringa di versione (*principali* e *secondaria*) sono obbligatori. Gli ultimi due numeri nella stringa di versione (*compilare* e *revisione*) sono facoltativi e predefinito su zero se l'utente li esclude. Ciò significa che se l'utente specifica solo "12.2" come il numero di versione di Local DB, verrà considerato come se l'utente avesse specificato "12.2.0.0".  
  
 La versione per l'installazione del database locale è definita nella chiave del Registro di sistema MSSQLServer\CurrentVersion sotto la chiave del Registro di sistema dell'istanza di SQL Server, ad esempio:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL13E.LOCALDB\ MSSQLServer\CurrentVersion: "CurrentVersion"="12.0.2531.0"  
```  
  
 È supportata la modalità side-by-side di più versioni del database locale sulla stessa workstation. Tuttavia, il codice utente Usa sempre la versione più recente disponibile **SQLUserInstance** DLL nel computer locale per connettersi alle istanze di Local DB.  
  
## <a name="locating-the-sqluserinstance-dll"></a>Individuazione della DLL SQLUserInstance  
 Per individuare il **SQLUserInstance** DLL, il provider client usa la chiave del Registro di sistema seguente:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions]  
```  
  
 In questa chiave è disponibile un elenco di chiavi, una per ogni versione del database locale installata nel computer. Ognuna di queste chiavi è denominata con il numero di versione di Local DB nel formato  *\<major-version >* . *\<minor-version >* (ad esempio, la chiave per [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] denominato 13.0). In ogni chiave della versione è disponibile una coppia nome/valore di `InstanceAPIPath` che consente di definire il percorso completo al file SQLUserInstance.dll installato con tale versione. Nell'esempio seguente mostra le voci del Registro di sistema per un computer dotato di Local DB versioni 11.0 e 13.0 installato:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
```  
  
 Il provider client deve trovare la versione più recente fra tutte le versioni installate e carico il **SQLUserInstance** file DLL da associato `InstanceAPIPath` valore.  
  
### <a name="wow64-mode-on-64-bit-windows"></a>Modalità WOW64 in Windows a 64 bit  
 Le installazioni a 64 bit del database locale disporranno di un set aggiuntivo di chiavi del Registro di sistema per consentire applicazioni a 32 bit in esecuzione in modalità WOW64 (Windows-32-on-Windows-64) per l'utilizzo del database locale. In particolare, in Windows a 64 bit il file MSI del database locale consentirà la creazione delle chiavi del Registro di sistema seguenti:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
  
```  
  
 programmi a 64 bit che leggono il `Installed Versions` chiave verrà visualizzati valori che puntano alle versioni a 64 bit del **SQLUserInstance** DLL, mentre programmi a 32 bit (in esecuzione su Windows a 64 bit in modalità WOW64) verranno reindirizzati automaticamente a un `Installed Versions` chiave che si trova sotto il `Wow6432Node` hive. Questa chiave contiene valori che puntano alle versioni a 32 bit del **SQLUserInstance** DLL.  
  
## <a name="using-localdbdefineproxyfunctions"></a>Utilizzo di LOCALDB_DEFINE_PROXY_FUNCTIONS  
 L'API dell'istanza di Local DB definisce una costante denominata LOCALDB_DEFINE_PROXY_FUNCTIONS che consente di automatizzare l'individuazione e il caricamento del **SqlUserInstance** DLL.  
  
 La sezione di codice abilitata da questa costante fornisce un'implementazione di proxy per ognuna delle API del database locale. Le implementazioni di proxy usano una funzione comune da associare ai punti di ingresso in quella più recente installata **SqlUserInstance** DLL e quindi di inoltrare le richieste.  
  
 Le funzioni del proxy sono abilitate solo se la costante LOCALDB_DEFINE_PROXY_FUNCTIONS è definita nel codice utente prima di includere il file sqlncli.h. La costante deve essere definita in un unico modulo di origine (file con estensione cpp) in quanto consente di definire nomi di funzioni esterni per tutti i punti di ingresso dell'API. Inoltre, tale costante fornisce un'implementazione di proxy per ognuna delle API del database locale.  
  
 Nell'esempio di codice seguente viene mostrato come utilizzare la macro dal codice C++ nativo:  
  
```  
// Define the LOCALDB_DEFINE_PROXY_FUNCTIONS constant to enable the LocalDB proxy functions   
// The #define has to take place BEFORE the API header file (sqlncli.h) is included  
#define LOCALDB_DEFINE_PROXY_FUNCTIONS  
#include <sqlncli.h>  
...  
HRESULT hr = S_OK;  
  
// Create LocalDB instance by calling the create API proxy function included by macro  
if (FAILED(hr = LocalDBCreateInstance( L"12.0", L"name", 0)))  
{  
...  
}  
...  
  
```  
  
  
