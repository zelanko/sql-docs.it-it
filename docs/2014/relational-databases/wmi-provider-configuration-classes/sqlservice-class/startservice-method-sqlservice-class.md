---
title: Metodo StartService (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- StartService Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- StartService method
ms.assetid: 83dfb6bd-dbd5-45d8-aad2-a11926317f91
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d0a425bda3d32f19aca5be09dbb8ba4b7b6ac899
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357929"
---
# <a name="startservice-method-sqlservice-class"></a>Metodo StartService (classe SqlService)
  Esegue un tentativo di avvio del servizio.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object  
.StartService()  
  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlService](sqlservice-class.md) che rappresenta il servizio.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore uint32 che specifica uno dei seguenti stati di avvio.  
  
 0  
 Esito positivo. La richiesta è stata accettata.  
  
 1  
 Non supportato. La richiesta non è supportata.  
  
 2  
 Accesso negato. L'utente non dispone dei diritti di accesso appropriati.  
  
 3  
 Servizi dipendenti in esecuzione. Impossibile arrestare il servizio perché altri servizi in esecuzione dipendono dal servizio.  
  
 4  
 Controllo servizio non valido. Il codice di controllo richiesto non è valido o non è accettabile per il servizio.  
  
 5  
 Il servizio non accetta il controllo. Impossibile inviare il codice di controllo richiesto al servizio perché lo stato del servizio (Win32_BaseService:State) è uguale a 0, 1 o 2.  
  
 6  
 Servizio non attivo. Il servizio non è stato avviato.  
  
 7  
 Timeout richiesta servizio. Il servizio non ha risposto in tempo utile alla richiesta di avvio.  
  
 8  
 Errore sconosciuto. Errore sconosciuto durante l'avvio del servizio.  
  
 9  
 Percorso non trovato. Impossibile trovare il percorso di directory del file eseguibile del servizio.  
  
 10  
 Servizio già in esecuzione. Il servizio è già in esecuzione.  
  
 11  
 Database del servizio bloccato. Il database a cui aggiungere il nuovo servizio è bloccato.  
  
 12  
 Dipendenza del servizio eliminata. Il servizio si basa su una dipendenza che è stata rimossa dal sistema.  
  
 13  
 Errore di dipendenza del servizio. Impossibile trovare un servizio dipendente necessario.  
  
 14  
 Servizio disabilitato. Il servizio è stato disabilitato dal sistema.  
  
 15  
 Errore di accesso del servizio. Il servizio non dispone delle credenziali di autenticazione corrette per l'esecuzione nel sistema.  
  
 16  
 Servizio contrassegnato per l'eliminazione. Il servizio verrà rimosso dal sistema.  
  
 17  
 Nessun thread disponibile per il servizio. Nessun thread di esecuzione per il servizio.  
  
 18  
 Stato: dipendenza circolare. All'avvio del servizio sono state rilevate dipendenze circolari.  
  
 19  
 Stato: nome duplicato. È presente un servizio in esecuzione con lo stesso nome.  
  
 20  
 Stato: nome non valido. Il nome del servizio contiene caratteri non validi.  
  
 21  
 Stato: parametro non valido. Sono stati passati parametri non validi al servizio.  
  
 22  
 Stato: account di servizio non valido. L'account utilizzato per l'esecuzione del servizio non è valido o non dispone delle autorizzazioni necessarie per eseguire il servizio.  
  
 23  
 Stato: servizio già esistente. Il servizio esiste già nel database dei servizi disponibili dal sistema.  
  
 24  
 Servizio già sospeso. Il servizio è attualmente sospeso nel sistema.  
  
## <a name="remarks"></a>Note  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
