---
title: Comando SET COLLATE Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a9c1dfd59c00ad0ac0b7bd8b8f1cdfccc84d9b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300891"
---
# <a name="set-collate-command"></a>SET COLLATE (comando)
Specifica una sequenza di confronto per i campi di caratteri nelle successive operazioni di indicizzazione e ordinamento.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>Argomenti  
 *cSequenceName (NomeSequenza)*  
 Specifica una sequenza di confronto. Le opzioni della sequenza di confronto disponibili sono descritte nella tabella seguente.  
  
|Opzioni|Linguaggio|  
|-------------|--------------|  
|Olandese|Olandese|  
|GENERAL|Inglese, francese, tedesco, spagnolo moderno, portoghese e altre lingue dell'Europa occidentale|  
|Tedesco|Ordine rubrica telefonica tedesco (DIN)|  
|Islanda|Islandese|  
|Macchina|Computer (sequenza di confronto predefinita per le versioni precedenti di FoxPro)|  
|NORDAN|Norvegese, Danese|  
|Spagnolo|Spagnolo tradizionale|  
|SWEFIN|Svedese, Finlandese|  
|UNIQWT|Peso unico|  
  
> [!NOTE]  
>  Quando si specifica l'opzione SPAN , *ch* è una singola lettera che ordina tra *c* e *d*e *ll* esegue l'ordinamento compreso tra *l* e *m*.  
  
 Se si specifica un'opzione della sequenza di confronto come stringa di caratteri letterale, assicurarsi di racchiudere l'opzione tra virgolette:  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MACHINE è l'opzione predefinita della sequenza di confronto ed è la sequenza con cui gli utenti di Xbase hanno familiarità. I caratteri vengono ordinati come vengono visualizzati nella tabella codici corrente.  
  
 GENERALE può essere preferibile per gli utenti statunitensi ed europei occidentali. I caratteri vengono ordinati come vengono visualizzati nella tabella codici corrente. Nelle versioni di FoxPro precedenti alla 2.5, gli indici potrebbero essere stati creati utilizzando le funzioni **MAIUSC**( ) o **LOWER**( ) per convertire i campi di tipo carattere in un caso coerente. Nelle versioni di FoxPro successive alla 2.5, è invece possibile specificare l'opzione della sequenza di confronto GENERAL e omettere la conversione **UPPER**( ).  
  
 Se si specifica un'opzione della sequenza di confronto diversa da MACHINE e si crea un file idx, viene sempre creato un file idx compatto.  
  
 Utilizzare SET("COLLATE") per restituire la sequenza di confronto corrente.  
  
 È possibile specificare una sequenza di confronto per un'origine dati utilizzando la finestra di [dialogo ODBC Di](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) installazione di Visual FoxPro o la parola chiave Collate nella stringa di connessione con [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md). Questo è identico all'emissione del seguente comando:  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>Osservazioni  
 SET COLLATE consente di ordinare tabelle contenenti caratteri accentati per una qualsiasi delle lingue supportate. La modifica dell'impostazione di SET COLLATE non influisce sulla sequenza di confronto degli indici aperti in precedenza. Visual FoxPro mantiene automaticamente gli indici esistenti, fornendo la flessibilità di creare molti tipi diversi di indici, anche per lo stesso campo.  
  
 Ad esempio, se viene creato un indice con SET COLLATE impostato su GENERAL e l'impostazione SET COLLATE viene successivamente modificata in SPANISH, l'indice mantiene la sequenza di confronto GENERAL.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo di configurazione ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
