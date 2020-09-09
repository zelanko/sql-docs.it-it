---
description: Funzione LocalDBFormatMessage
title: Funzione LocalDBFormatMessage | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBFormatMessage
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a7be5ebfad2430b1161d5af8c1a61697aacd568c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544061"
---
# <a name="localdbformatmessage-function"></a>Funzione LocalDBFormatMessage
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Viene restituita la descrizione testuale localizzata per l'errore del database locale di SQL Server Express specificato.  
  
 **File di intestazione:** sqlncli. h  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT LocalDBFormatMessage(  
           HRESULT hrLocalDB,  
           DWORD dwFlags,   
           DWORD dwLanguageId,   
           LPWSTR wszMessage,   
           LPDWORD lpcchMessage   
);  
```  
  
## <a name="parameters"></a>Parametri  
 *hrLocalDB*  
 [Input] Codice di errore del database locale.  
  
 *dwFlags*  
 [Input] Flag che specificano il comportamento di questa funzione.  
  
 Flag disponibili:  
  
 LOCALDB_TRUNCATE_ERR_MESSAGE  
 Se il buffer di input è troppo corto, il messaggio di errore sarà troncato in base al buffer.  
  
 *dwLanguageId*  
 [Input] Lingua desiderata (LANGID) o 0. In tal caso viene utilizzato l'ordine della lingua FormatMessage di Win32.  
  
 *wszMessage*  
 [Output] Buffer per archiviare il messaggio di errore del database locale.  
  
 *lpcchMessage*  
 [Input/output] In input contiene la dimensione del buffer *wszMessage* in caratteri. In fase di output, se le dimensioni del buffer specificate sono troppo piccole, nel parametro sono contenute le dimensioni del buffer richieste in caratteri, inclusi gli spazi vuoti finali. Se la funzione viene completata, in essa è contenuto il numero di caratteri nel messaggio, esclusi gli spazi vuoti finali.  
  
## <a name="returns"></a>Restituisce  
 S_OK  
 Funzione completata.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 Database locale di SQL Server Express non installato nel computer.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o più parametri di input specificati non validi.  
  
 [LOCALDB_ERROR_UNKNOWN_ERROR_CODE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-error-code.md)  
 Messaggio richiesto inesistente.  
  
 [LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-language-id.md)  
 Messaggio non disponibile nella lingua richiesta.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../../relational-databases/express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 Il buffer di input *wszMessage* è troppo breve e il troncamento non è richiesto.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Si è verificato un errore imprevisto. Per informazioni, vedere il registro eventi.  
  
## <a name="remarks"></a>Osservazioni  
 Per un esempio di codice in cui viene utilizzata l'API del database locale, vedere [SQL Server Express riferimento al database locale](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulla versione e intestazione di SQL Server Express LocalDB](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
