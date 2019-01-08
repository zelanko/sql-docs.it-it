---
title: Funzione LocalDBGetInstances | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBGetInstances
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: f95a9980-8bc0-426c-8aa1-e2660b6784cf
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 92aa65bd2d3aad71f2467efaa7a09f75f20d8f63
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52795034"
---
# <a name="localdbgetinstances-function"></a>Funzione LocalDBGetInstances
  Vengono restituite tutte le istanze del database locale di SQL Server Express con la versione specificata.  
  
 **File di intestazione:** SQLNCLI. h  
  
## <a name="syntax"></a>Sintassi  
  
```  
#define MAX_LOCALDB_INSTANCE_NAME_LENGTH 128typedef WCHAR TLocalDBInstanceName[MAX_LOCALDB_INSTANCE_NAME_LENGTH + 1];typedef TLocalDBInstanceName* PTLocalDBInstanceName;  
HRESULT LocalDBGetInstances(  
           PTLocalDBInstanceName pInstanceNames,  
           LPDWORD lpdwNumberOfInstances  
);  
```  
  
## <a name="parameters"></a>Parametri  
 *pInstanceNames*  
 [Output] Quando questa funzione viene restituito, contiene i nomi di entrambi denominato e predefinito di istanze del database locale nella workstation dell'utente.  
  
 *lpdwNumberOfInstances*  
 [Input/Output] Per l'input, contiene il numero di slot per i nomi delle istanze nel *pInstanceNames* buffer. Nell'output contiene il numero di istanze di database locale trovate nella workstation dell'utente.  
  
## <a name="returns"></a>Valori di codice restituiti  
 S_OK  
 Funzione completata.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 Database locale di SQL Server Express non installato nel computer.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o più parametri di input specificati non validi.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 Buffer di input troppo corto. Troncamento non necessario.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 Percorso di archiviazione richiesto per l'istanza più lungo di MAX_PATH.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 Impossibile accedere al Registro di sistema di un'istanza.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 Configurazione di un'istanza danneggiata.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 Errore imprevisto. Per informazioni, vedere il registro eventi.  
  
## <a name="remarks"></a>Note  
 Per un esempio di codice che utilizza l'API LocalDB, vedere [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulla versione e intestazione di SQL Server Express LocalDB](sql-server-express-localdb-header-and-version-information.md)  
  
  
