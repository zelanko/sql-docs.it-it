---
title: Funzione LocalDBStopInstance | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBStopInstance
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 4bd73187-0aac-4f03-ac54-2b78e41917e5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 89db6e2a85e502b675db2006a682ff6b35fb4491
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68022065"
---
# <a name="localdbstopinstance-function"></a>Funzione LocalDBStopInstance
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Viene arrestata l'esecuzione dell'istanza del database locale di SQL Server Express specificata.  
  
 **File di intestazione:** sqlncli. h  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT LocalDBStopInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           ULONG ulTimeout   
);  
```  
  
## <a name="parameters"></a>Parametri  
 *pInstanceName*  
 [Input] Nome dell'istanza del database locale da arrestare.  
  
 *dwFlags*  
 [Input] Uno o una combinazione di valori per i flag che specificano la modalità di arresto dell'istanza.  
  
 Flag disponibili:  
  
 LOCALDB_SHUTDOWN_KILL_PROCESS  
 Arrestare immediatamente l'utilizzo del comando del sistema operativo relativo al processo di terminazione.  
  
 LOCALDB_SHUTDOWN_WITH_NOWAIT  
 Arrestare l'utilizzo del comando Transact-SQL dell'opzione NOWAIT.  
  
 Se non è impostato nessuno dei flag, l'istanza del database verrà arrestata tramite il comando Transact-SQL SHUTDOWN. Se sono impostati entrambi i flag, ha la precedenza il flag LOCALDB_SHUTDOWN_KILL_PROCESS.  
  
 *ulTimeout*  
 [Input] Ora in secondi di attesa per il completamento di questa operazione. Se questo valore è 0, verrà restituito immediatamente un valore senza attendere l'arresto dell'istanza del database locale.  
  
## <a name="returns"></a>Valori di codice restituiti  
 S_OK  
 Funzione completata.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 Database locale di SQL Server Express non installato nel computer.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o più parametri di input specificati non validi.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 Nome dell'stanza specificata non valido.  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-instance.md)  
 Istanza inesistente.  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../../relational-databases/express-localdb-error-messages/localdb-error-wait-timeout.md)  
 Timeout durante il tentativo di acquisizione dei blocchi di sincronizzazione.  
  
 [LOCALDB_ERROR_INSTANCE_STOP_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-instance-stop-failed.md)  
 Errore durante il completamento dell'operazione di arresto entro l'ora specificata.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 Percorso di archiviazione richiesto per l'istanza più lungo di MAX_PATH.  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 Impossibile recuperare una cartella del profilo utente.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 Impossibile accedere alla cartella di un'istanza.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 Impossibile accedere al Registro di sistema di un'istanza.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 Configurazione di un'istanza danneggiata.  
  
 [LOCALDB_ERROR_CALLER_IS_NOT_OWNER](../../relational-databases/express-localdb-error-messages/localdb-error-caller-is-not-owner.md)  
 Il chiamante API non è il proprietario dell'istanza del database locale.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Si è verificato un errore imprevisto. Per informazioni, vedere il registro eventi.  
  
## <a name="remarks"></a>Osservazioni  
 Per un esempio di codice in cui viene utilizzata l'API del database locale, vedere [SQL Server Express riferimento al database locale](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulla versione e intestazione di SQL Server Express LocalDB](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
