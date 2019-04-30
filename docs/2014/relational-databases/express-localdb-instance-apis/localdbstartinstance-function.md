---
title: Funzione LocalDBStartInstance | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBStartInstance
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: cb325f5d-10ee-4a56-ba28-db0074ab3926
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ad86f5989fe9ff90132637d062b708423f23eef1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63131497"
---
# <a name="localdbstartinstance-function"></a>Funzione LocalDBStartInstance
  Avvia l'istanza specificata del database locale di SQL Server Express.  
  
 **File di intestazione:** SQLNCLI. h  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT LocalDBStartInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           LPWSTR wszSqlConnection,   
           LPDWORD lpcchSqlConnection   
);  
```  
  
## <a name="parameters"></a>Parametri  
 *pInstanceName*  
 [Input] Nome dell'istanza del database locale da avviare.  
  
 *dwFlags*  
 [Input] Riservato per utilizzi futuri. Deve essere impostato attualmente su 0.  
  
 *wszSqlConnection*  
 [Output] Buffer per archiviare la stringa di connessione nell'istanza del database locale.  
  
 *lpcchSqlConnection*  
 [Input/Output] Contiene la dimensione di input il *wszSqlConnection* buffer in caratteri, inclusi gli spazi vuoti finali. In fase di output, se le dimensioni del buffer specificate sono troppo piccole, nel parametro sono contenute le dimensioni del buffer richieste in caratteri, inclusi gli spazi vuoti finali.  
  
## <a name="returns"></a>Valori di codice restituiti  
 S_OK  
 Funzione completata.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 Database locale di SQL Server Express non installato nel computer.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o più parametri di input specificati non validi.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 Nome dell'stanza specificata non valido.  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../express-localdb-error-messages/localdb-error-unknown-instance.md)  
 Istanza inesistente.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 Il buffer specificato *wszSqlConnection* è troppo piccolo.  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../express-localdb-error-messages/localdb-error-wait-timeout.md)  
 Timeout durante il tentativo di acquisizione dei blocchi di sincronizzazione.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 Percorso di archiviazione richiesto per l'istanza più lungo di MAX_PATH.  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 Impossibile recuperare una cartella del profilo utente.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 Impossibile accedere alla cartella di un'istanza.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 Impossibile accedere al Registro di sistema di un'istanza.  
  
 [LOCALDB_ERROR_CANNOT_MODIFY_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-modify-instance-registry.md)  
 Impossibile modificare il Registro di sistema di un'istanza.  
  
 [LOCALDB_ERROR_CANNOT_CREATE_SQL_PROCESS](../express-localdb-error-messages/localdb-error-cannot-create-sql-process.md)  
 Impossibile creare un processo per SQL Server.  
  
 [LOCALDB_ERROR_SQL_SERVER_STARTUP_FAILED](../express-localdb-error-messages/localdb-error-sql-server-startup-failed.md)  
 Avviato processo di SQL Server ma tale operazione non è stata completata.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 Configurazione di un'istanza danneggiata.  
  
 [LOCALDB_ERROR_AUTO_INSTANCE_CREATE_FAILED](../express-localdb-error-messages/localdb-error-auto-instance-create-failed.md)  
 Impossibile creare un'istanza automatica. Per informazioni sugli errori, vedere il registro eventi applicazioni di Windows.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 Errore imprevisto. Per informazioni, vedere il registro eventi.  
  
## <a name="details"></a>Dettagli  
 Sia l'argomento di buffer di connessione (*wszSqlConnection*) e l'argomento di dimensione del buffer di connessione (*lpcchSqlConnection*) sono facoltativi. Nella tabella seguente vengono mostrate le opzioni per l'utilizzo di questi argomenti e dei relativi risultati.  
  
|Buffer|Dimensioni del buffer|Spiegazione|Azione|  
|------------|-----------------|---------------|------------|  
|NULL|NULL|Utente desidera avviare l'istanza e non è necessaria una pipe nome.|Viene avviata un'istanza. Non viene restituita alcuna pipe né le dimensioni del buffer richieste.|  
|NULL|Presente|L'utente richiede le dimensioni del buffer di output. Nella chiamata successiva probabilmente l'utente richiederà un avvio effettivo.|Vengono restituite le dimensioni del buffer richieste (nessun avvio né restituzione di pipe). Il risultato è S_OK.|  
|Presente|NULL|Non consentito. Input non corretto.|Il risultato restituito è LOCALDB_ERROR_INVALID_PARAMETER.|  
|Presente|Presente|L'utente desidera avviare l'istanza e necessita del nome della pipe per la connessione a quest'ultima dopo il relativo avvio.|Vengono controllate le dimensioni del buffer, viene avviata l'istanza e viene restituito il nome della pipe nel buffer. <br />L'argomento di dimensione buffer restituisce la lunghezza di "server =" stringa, senza includere valori null di terminazione.|  
  
 Per un esempio di codice che utilizza l'API LocalDB, vedere [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulla versione e intestazione di SQL Server Express LocalDB](sql-server-express-localdb-header-and-version-information.md)  
  
  
