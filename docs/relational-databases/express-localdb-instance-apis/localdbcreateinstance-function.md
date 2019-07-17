---
title: Funzione LocalDBCreateInstance | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBCreateInstance
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 3eebb485-8a53-4a79-82a9-57b8de9f8e84
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 297dd5ca109e7b35d8d74d5daf1f8b1c7fd06703
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126936"
---
# <a name="localdbcreateinstance-function"></a>Funzione LocalDBCreateInstance
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Viene creata un'istanza del database locale di SQL Server Express.  
  
 **File di intestazione:** SQLNCLI. h  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT LocalDBCreateInstance(  
           PCWSTR wszVersion,  
           PCWSTR pInstanceName,   
           DWORD dwFlags   
);  
```  
  
## <a name="parameters"></a>Parametri  
 *wszVersion*  
 [Input] Versione del database locale, ad esempio 11.0 o 11.0.1094.2.  
  
 *pInstanceName*  
 [Input] Nome dell'istanza del database locale da creare.  
  
 *dwFlags*  
 [Input] Riservato per utilizzi futuri. Deve essere impostato attualmente su 0.  
  
## <a name="returns"></a>Valori di codice restituiti  
 S_OK  
 Funzione completata.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 Database locale di SQL Server Express non installato nel computer.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o più parametri di input specificati non validi.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 Nome dell'stanza specificata non valido.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 Percorso di archiviazione richiesto per l'istanza più lungo di MAX_PATH.  
  
 [LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-instance-exists-with-lower-version.md)  
 Istanza specificata già esistente ma con relativa versione meno recente di quella richiesta.  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-version.md)  
 Versione specificata non disponibile.  
  
 [LOCALDB_ERROR_VERSION_REQUESTED_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-version-requested-not-installed.md)  
 Livello di patch specificato non installato.  
  
 [LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-create-instance-folder.md)  
 Impossibile creare una cartella in %profiloutente%.  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 Impossibile recuperare una cartella del profilo utente.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 Impossibile accedere alla cartella di un'istanza.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 Impossibile accedere al Registro di sistema di un'istanza.  
  
 [LOCALDB_ERROR_CANNOT_MODIFY_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-modify-instance-registry.md)  
 Impossibile modificare il Registro di sistema di un'istanza.  
  
 [LOCALDB_ERROR_SQL_SERVER_STARTUP_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-sql-server-startup-failed.md)  
 Avviato processo di SQL Server ma tale operazione non è stata completata.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 Configurazione di un'istanza danneggiata.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Errore imprevisto. Per informazioni, vedere il registro eventi.  
  
## <a name="remarks"></a>Note  
 Se un'istanza del database locale completamente funzionale con il nome specificato già esiste e la versione è uguale o successiva rispetto a quella richiesta, il risultato è S_OK.  
  
 Nei casi in cui un'istanza esistente è danneggiate, le chiamate successive per la **LocalDBCreateInstance** metodo API avrà esito negativo. Le istanze danneggiate devono essere corrette manualmente o eliminate in modo esplicito prima che possano essere utilizzate di nuovo.  
  
 Per un esempio di codice che utilizza l'API LocalDB, vedere [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulla versione e intestazione di SQL Server Express LocalDB](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
