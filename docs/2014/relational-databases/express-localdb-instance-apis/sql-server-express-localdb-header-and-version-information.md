---
title: Informazioni sulla versione e l'intestazione del database locale SQL Server Express | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_location:
- sqluserinstance.dll
ms.assetid: 506b5161-b902-4894-b87b-9192d7b1664a
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6e390430115daf394c5e94267dad30a87851375d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63128691"
---
# <a name="sql-server-express-localdb-header-and-version-information"></a>Informazioni sulla versione e intestazione del database locale di SQL Server Express
  Non esiste alcun file di intestazione separato per l'API dell'istanza del database locale di SQL Server Express. Le firme e i codici di errore della funzione del database locale sono definiti nel file di intestazione (sqlncli.h) di SQL Server Native Client. Per utilizzare l'API dell'istanza del database locale, è necessario includere il file di intestazione sqlncli.h nel progetto.  
  
## <a name="localdb-versioning"></a>Controllo delle versioni del database locale  
 Per l'installazione del database locale viene utilizzato un solo set di file binari per la versione di SQL Server principale. Queste versioni del database locale sono gestite e installate con patch in modo indipendente. Pertanto, l'utente deve specificare quale versione di base (ovvero, versione di SQL Server principale) del database locale utilizzerà. La versione è specificata nel formato della versione standard definito dalla classe .NET Framework **System. Version** :  
  
 *Major. minor [. Build [. Revisione]]*  
  
 I primi due numeri nella stringa di versione (*principale* e *secondaria*) sono obbligatori. Gli ultimi due numeri nella stringa di versione (*compilazione* e *Revisione*) sono facoltativi e il valore predefinito è zero se l'utente li lascia fuori. Ciò significa che se l'utente specifica solo "12,2" come numero di versione del database locale, verrà considerato come se l'utente avesse specificato "12.2.0.0".  
  
 La versione per l'installazione del database locale è definita nella chiave del Registro di sistema MSSQLServer\CurrentVersion sotto la chiave del Registro di sistema dell'istanza di SQL Server, ad esempio:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12E.LOCALDB\ MSSQLServer\CurrentVersion: "CurrentVersion"="12.0.2531.0"  
```  
  
 È supportata la modalità side-by-side di più versioni del database locale sulla stessa workstation. Tuttavia, il codice utente utilizza sempre la dll **SQLUserInstance** disponibile più recente nel computer locale per la connessione alle istanze del database locale.  
  
## <a name="locating-the-sqluserinstance-dll"></a>Individuazione della DLL SQLUserInstance  
 Per individuare la dll **SQLUserInstance** , il provider client utilizza la seguente chiave del registro di sistema:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions]  
```  
  
 In questa chiave è disponibile un elenco di chiavi, una per ogni versione del database locale installata nel computer. Ognuna di queste chiavi è denominata con il numero di versione del database locale nel formato * \<principale-versione>*. versione secondaria>(ad esempio, la chiave per [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] è denominata 12,0). * \<* In ogni chiave della versione è disponibile una coppia nome/valore di `InstanceAPIPath` che consente di definire il percorso completo al file SQLUserInstance.dll installato con tale versione. Nell'esempio seguente vengono mostrate le voci del Registro di sistema per un computer in cui sono installate le versioni 11.0 e 12.0 del database locale:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"]  
```  
  
 Il provider client deve trovare la versione più recente tra tutte le versioni installate e caricare il file dll **SQLUserInstance** dal `InstanceAPIPath` valore associato.  
  
### <a name="wow64-mode-on-64-bit-windows"></a>Modalità WOW64 in Windows a 64 bit  
 Le installazioni a 64 bit del database locale disporranno di un set aggiuntivo di chiavi del Registro di sistema per consentire applicazioni a 32 bit in esecuzione in modalità WOW64 (Windows-32-on-Windows-64) per l'utilizzo del database locale. In particolare, in Windows a 64 bit il file MSI del database locale consentirà la creazione delle chiavi del Registro di sistema seguenti:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"]  
  
```  
  
 i programmi a 64 bit che `Installed Versions` leggono la chiave vedranno i valori che puntano a versioni a 64 bit della dll **SQLUserInstance** , mentre i `Wow6432Node` programmi a 32 bit (in esecuzione in Windows a 64 bit in modalità WOW64) verranno `Installed Versions` reindirizzati automaticamente a una chiave che si trova in hive. Questa chiave contiene valori che puntano a versioni a 32 bit della dll **SQLUserInstance** .  
  
## <a name="using-localdb_define_proxy_functions"></a>Utilizzo di LOCALDB_DEFINE_PROXY_FUNCTIONS  
 L'API dell'istanza del database locale definisce una costante denominata LOCALDB_DEFINE_PROXY_FUNCTIONS che automatizza l'individuazione e il caricamento della dll **SQLUserInstance** .  
  
 La sezione di codice abilitata da questa costante fornisce un'implementazione di proxy per ognuna delle API del database locale. Le implementazioni del proxy usano una funzione comune per l'associazione ai punti di ingresso nella dll **SQLUserInstance** installata più recente e quindi le inviano.  
  
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
  
  
