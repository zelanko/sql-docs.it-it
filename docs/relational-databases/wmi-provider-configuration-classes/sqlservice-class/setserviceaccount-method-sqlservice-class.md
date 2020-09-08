---
description: Metodo SetServiceAccount (classe SqlService)
title: Metodo SetServiceAccount (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetServiceAccount Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cbd892624ec888635439d19311d9ba823ee52c98
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89520031"
---
# <a name="setserviceaccount-method-sqlservice-class"></a>Metodo SetServiceAccount (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Tenta di modificare il nome utente e la password con cui è in esecuzione l'istanza del servizio.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SetServiceAccount(ServiceStartName , ServiceStartPassword)  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) che rappresenta il servizio.  
  
#### <a name="parameters"></a>Parametri  
 *ServiceStartName*  
 Valore string che specifica il nome dell'account con cui è in esecuzione il servizio. A seconda del tipo di servizio, il nome dell'account potrebbe essere nel formato NomeDominio\NomeUtente. Durante l'esecuzione il processo del servizio viene registrato utilizzando uno di due formati:  
  
-   Se l'account appartiene al dominio predefinito, è possibile specificare \Nomeutente.  
  
-   Se viene specificato NULL, il servizio verrà connesso come account **LocalSystem** .  
  
 Per i driver a livello di sistema o del kernel, *StartName* contiene il nome dell'oggetto del driver, \FileSystem\Rdr o \Driver\Xns, usato dal sistema di i/O per caricare il driver di dispositivo. Se viene specificato NULL, il driver viene eseguito con un nome dell'oggetto predefinito creato dal sistema I/O in base sul nome del servizio, ad esempio DWDOM\Admin.  
  
 *ServiceStartPassword*  
 Valore stringa che specifica la password per il nome dell'account nel parametro *StartName* . Specificare NULL se non si modifica la password. Specificare una stringa vuota se il servizio non dispone di password.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che è 0 se il servizio è stato modificato correttamente 0 1 se la richiesta non è supportata. Qualsiasi altro numero indica un errore.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
