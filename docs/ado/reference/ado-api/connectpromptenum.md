---
description: ConnectPromptEnum
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
author: rothja
ms.author: jroth
ms.openlocfilehash: 171cc7706cc00b48c3373a0e40d5de221d4d00ce
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974682"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
Specifica se deve essere visualizzata una finestra di dialogo per richiedere parametri mancanti quando si apre una connessione a un'origine dati.  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|Richiede sempre.|  
|**adPromptComplete**|2|Richiede se sono necessarie altre informazioni.|  
|**adPromptCompleteRequired**|3|Richiede se sono necessarie altre informazioni ma non sono consentiti parametri facoltativi.|  
|**adPromptNever**|4|Non richiede mai.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. ConnectPrompt. ALWAYs|  
|AdoEnums. ConnectPrompt. COMPLETE|  
|AdoEnums. ConnectPrompt. COMPLETEREQUIRED|  
|AdoEnums. ConnectPrompt. NEVER|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà dinamica Prompt (ADO)](./prompt-property-dynamic-ado.md)