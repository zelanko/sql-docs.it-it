---
title: Funzione LocalDBGetVersionInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBGetVersionInfo
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7030f26cb95b78a3cd2dde8520876f13acc4bc46
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68091199"
---
# <a name="localdbgetversioninfo-function"></a>Funzione LocalDBGetVersionInfo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Vengono restituite le informazioni per la versione del database locale di SQL Server Express specificata, se esistente, e il numero completo della versione del database locale, ovvero con i numeri di compilazione e della versione inclusi.  
  
 Le informazioni vengono restituite sotto forma di uno **struct** denominato **LocalDBVersionInfostruct**, che presenta la definizione seguente.  
  
```  
typedef struct _LocalDBVersionInfo  
{  
      // Contains the size of the LocalDBVersionInfo struct  
      DWORD  cbLocalDBVersionInfoSize;  
  
      // Holds the version name  
      TLocalDBVersionwszVersion;  
  
      // TRUE if the instance files exist on disk, FALSE otherwise  
      BOOL   bExists;  
  
      // Holds the LocalDB version for the instance in the format: major.minor.build.revision  
      DWORD  dwMajor;  
      DWORD  dwMinor;  
      DWORD  dwBuild;  
      DWORD  dwRevision;  
} LocalDBVersionInfo;  
  
```  
  
 **File di intestazione:** sqlncli. h  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT LocalDBGetVersionInfo(  
           PCWSTR wszVersionName,           PLocalDBVersionInfo pVersionInfo,           DWORD dwVersionInfoSize);  
```  
  
## <a name="parameters"></a>Parametri  
 *wszVersionName*  
 [Input] Nome della versione del database locale.  
  
 *pVersionInfo*  
 [Output] Buffer per archiviare le informazioni sulla versione del database locale.  
  
 *dwVersionInfoSize*  
 Input Include le dimensioni del buffer *VERSIONINFO* .  
  
## <a name="returns"></a>Valori di codice restituiti  
 S_OK  
 Funzione completata.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 Database locale di SQL Server Express non installato nel computer.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o più parametri di input specificati non validi.  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-version.md)  
 La versione del database locale specificata non esiste.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Si è verificato un errore imprevisto. Per informazioni, vedere il registro eventi.  
  
## <a name="details"></a>Dettagli  
 La logica alla base dell'introduzione dell'argomento di dimensioni **struct** (*lpVersionInfoSize*) consiste nell'abilitare l'API per la restituzione di versioni diverse di **LocalDBVersionInfostruct**, abilitando in modo efficace la compatibilità con le versioni precedenti e precedenti.  
  
 Se l'argomento di dimensione della **struct** (*lpVersionInfoSize*) corrisponde alle dimensioni di una versione nota di **LocalDBVersionInfostruct**, viene restituita tale versione dello **struct** . In caso contrario, viene restituito LOCALDB_ERROR_INVALID_PARAMETER.  
  
 Un esempio tipico di utilizzo dell'API **LocalDBGetVersionInfo** è simile al seguente:  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L"11.0", &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>Osservazioni  
 Per un esempio di codice in cui viene utilizzata l'API del database locale, vedere [SQL Server Express riferimento al database locale](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulla versione e intestazione di SQL Server Express LocalDB](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
